### 在新 network namespace 执行 sleep 指令：

```sh
unshare -fn sleep 60

命令 "unshare -fn sleep" 的作用是在新的命名空间中运行 "sleep" 命令。
更具体地说，"unshare" 命令用于创建一个新的命名空间，它会隔离某些系统资源（例如进程、网络、文件系统等）。"-n" 参数表示只隔离网络命名空间。"-f" 参数表示在新的命名空间中运行一个新的进程。最后的 "sleep" 命令是在新的命名空间中运行的命令，它会让进程进入休眠状态，直到指定的时间结束。
因此，"unshare -fn sleep" 的作用是在新的网络命名空间中启动一个新的进程，并让该进程休眠，直到时间结束。
```

### 查看进程信息

```sh
ps -ef|grep sleep
root       32882    4935  0 10:00 pts/0    00:00:00 unshare -fn sleep 60
root       32883   32882  0 10:00 pts/0    00:00:00 sleep 60
```

### 查看网络 Namespace

```sh
lsns -t net
4026532508 net       2 32882 root unassigned                                unshare
```

### 进入改进程所在 Namespace 查看网络配置，与主机不一致

```sh
nsenter -t 32882 -n ip a
1: lo: <LOOPBACK> mtu 65536 qdisc noop state DOWN group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
```
