* 参数说明

-s以server模式启动，eg：iperf-s

-chost以client模式启动，host是server端地址，eg：iperf-c172.16.10.20

* 通用参数

-f\[kmKM\]分别表示以Kbits,Mbits,KBytes,MBytes显示报告，默认以Mbits为单位,eg：iperf-c172.16.10.20-fK

-isec以秒为单位显示报告间隔，eg：iperf-c172.16.10.20-i2

-l缓冲区大小，默认是8KB,eg：iperf-c172.16.10.20-l16

-m显示tcp最大mtu值

-o将报告和错误信息输出到文件eg：iperf-c172.16.10.20-ociperflog.txt

-p指定服务器端使用的端口或客户端所连接的端口eg：iperf-s-p9999;iperf-c172.16.10.20-p9999

-u使用udp协议

-w指定TCP窗口大小，默认是8KB

-B绑定一个主机地址或接口（当主机有多个地址或接口时使用该参数）

-C兼容旧版本（当server端和client端版本不一样时使用）

-M设定TCP数据包的最大mtu值

-N设定TCP不延时

-V传输ipv6数据包

* server专用参数

-D以服务方式运行iperf，eg：iperf-s-D

-R停止iperf服务，针对-D，eg：iperf-s-R

* client端专用参数

-d同时进行双向传输测试

-n指定传输的字节数，eg：iperf-c172.16.10.20-n100000

-r单独进行双向传输测试

-t测试时间，默认10秒,eg：iperf-c172.16.10.20-t5

-F指定需要传输的文件

-T指定ttl值

•应用实例

（1）使用服务端和客户端的默认设置进行测试

使用iperf-s命令将Iperf启动为server模式

`iperf–s`

`------------------------------------------------------------`

`ServerlisteningonTCPport5001`

`TCPwindowsize:8.00KByte(default)`

`------------------------------------------------------------`

在客户机上使用iperf-c启动client模式

`iperf-c192.168.1.19`

（2）服务器端和客户端的TCP窗口都开到300KB

`iperf-s-w300K`

`------------------------------------------------------------`

`ServerlisteningonTCPport5001`

`TCPwindowsize:300KByte`

`------------------------------------------------------------`

客户端设定报告间隔为2秒

`iperf-c192.168.1.19-fK-i2-w300K`

测试传输约1MB数据

`iperf-c192.168.1.19-fK-i2-w300K–n1000000`

测试持续36秒

`iperf-c192.168.1.19-fK-i2-w300K–t36`

测试双向的传输

`iperf-c192.168.1.19-fK-i2-w300K-n10400000–d`

UDP测试

`iperf-c192.168.1.19-fK-i2-w300K–u`

其中-i参数的含义是周期性报告的时间间隔（interval），单位为秒；在上面的例子中，表示每隔2秒报告一次带宽等信息。

•启动一个iperf服务器进程

首先要介绍的命令用来启动iperf服务器监听进程以便监听客户端连接

iperf.exe -s -P2 -i 5 -p 5999 -f k

启动iperf，-p设定监听5999端口\(默认端口是5001\)；-P设定iperf只允许两个连接；-i设定每5秒汇报一次连接情况；

连接限制参数\(-P参数\)非常重要，当两个连接建立后，服务器进程就会退出。如果这个参数设定为0，那么iperf进程将持续监听端口，并且不限制连接数量

•启动一个iperf客户端连接

iperf的另一半就是客户端，用来连接到服务器监听端口

iperf.exe-cs-network1.amcs.tld-P1-i5-p5999-fB-t60-T1

连接到一台地址为s-network1.amcs.tld的服务器，端口为5999，连接60秒并且每5秒显示一次状态，命令启动后，s-network1主机被用来进行网络性能检测



