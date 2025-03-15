def Test(String thread) {
    echo "Đây là luồng số ${thread}"
    touch "logfile_${thread}.txt"
    sleep(10) 
    echo "phase 1" > "logfile_${thread}.txt"
    sleep(5) 
    echo "phase 2" >> "logfile_${thread}.txt"
    cat "logfile_${thread}.txt"
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
