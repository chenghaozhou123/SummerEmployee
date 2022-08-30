free -th标准显示

ps -o lstart -p PID             #根据PID来查询

ps -o lstart,etime -p PID       #根据PID来查询,打印出启动时间和已经运行的时间

ps -eO lstart | grep PROCESS    #根据进程名字查询