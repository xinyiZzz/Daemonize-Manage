## March 1 2016 11:14 AM

# Daemonize-Manage
Daemonize management base class, providing daemon creation and termination, logging, child process management/守护进程管理基类，提供守护进程创建及终止、日志记录、子进程管理

* * *


## function/系统功能

创建守护进程执行指定程序
在当前目录创建/log目录存储日志
对守护进程启动的子进程管理，避免出现僵尸进程


## examples/使用范例

- 接口：
    start_operation():    守护进程启动后运行，需重写为守护进程启动后执行的程序
    stop_operation():     守护进程结束前运行，需重写为守护进程结束前执行的程序
    write_process_pid():  守护进程启动子进程时，在子进程的run()函数开始时调用，将子进程的pid作为文件名创建到/engine_pids目录下，表明子进程开始
    remove_process_pid(): 子进程结束时调用，删除/engine_pids目录下该子进程pid命名的文件，表明子进程结束
    kill_child_process():  杀掉当前进程，若成功则删除该子进程在/engine_pids目录下文件
    
- log目录说明：
    engine_stdout.log：   进程正常输出的日志文件
    engine_stderr.log：   进程错误输出的日志文件
    engine_pids：         以子进程的pid作为文件名，存储守护进程所启动的每个子进程中对应任务，用于记录子进程存活状态
    
- 使用方法：
    启动方式：             python XXX.py start
    关闭方式：             python XXX.py stop
    重启方法：             python XXX.py restart
    查看守护进程状态命令： ps -ef | grep base.py |grep -v grep
    也可使用  kill -9 pid 关闭守护进程

>注：具体使用范例查看test_daemonize.py

## contact/联系方式


609610350@qq.com
