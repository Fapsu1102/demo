def Test(String thread) {
    echo "Đây là luồng số ${thread}"
    
    def logFile = "logfile_${thread}.txt"
    
    // Tạo file rỗng
    writeFile(file: logFile, text: "")
    
    sleep(10)
    
    // Ghi "phase 1" vào file
    writeFile(file: logFile, text: "phase 1\n")
    
    sleep(5)
    
    // Thêm "phase 2" vào file
    appendToFile(file: logFile, text: "phase 2\n")
    
    // Đọc nội dung file
    def content = readFile(logFile)
    echo content
}
node("alpine_agent"){
    def input = ["1", "2", "3", "4"]
    def threadList = input

    def parallelStages = [:]

    threadList.each { thread ->
        parallelStages["Thread ${thread}"] = {
            Test(thread.trim())
        }
    }

    parallel parallelStages
}
