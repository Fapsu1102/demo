def Test(String thread) {
    echo "Đang chạy trên agent: ${env.NODE_NAME}"
    echo "Workspace: ${env.WORKSPACE}"
    sh "whoami"
    echo "Đây là luồng số ${thread}"
    
    // Tạo file rỗng
    sh "touch logfile_${thread}.txt"
    sh "ls -al"
    sleep(10)
    
    // Ghi "phase 1" vào file
    sh "echo 'phase 1' > logfile_${thread}.txt"
    sh "cat logfile_${thread}.txt"
    
    sleep(5)
    
    // Thêm "phase 2" vào file
    sh "echo 'phase 2' >> logfile_${thread}.txt"
    
    // Đọc nội dung file
    sh "cat logfile_${thread}.txt"
}
node("alpine_agent") {
    def input = ["1", "2", "3", "4"]
    def threadList = input

    def parallelStages = [:]

    threadList.each { thread ->
        parallelStages["Thread ${thread}"] = {
            node("alpine_agent") {
                Test(thread.trim())
            }
        }
    }
    parallel parallelStages
}


