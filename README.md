

# make build

```
更改编译选项 Common.allports.mk
```

```
$ git clone https://github.com/lwip-tcpip/lwip.git
$ cd lwip
# 在 linux lwip默认使用 tap0 作为网络接口
$ sudo ./contrib/ports/unix/setup-tapif
$ cp ./contrib/examples/example_app/lwipcfg.h.example ./contrib/ports/unix/example_app/lwipcfg.h
$ cd ./contrib/ports/unix/example_app
$ vim lwipcfg.h # 去掉`#define USE_DHCP 0` 和`#define USE_AUTOIP 0`的注释，并将`LWIP_LWIPERF_APP`的宏定义为 1
$ mkdir build && cd build
$ cmake -DLWIP_DIR=/path/to/your/lwip/repo ..
$ make
$ sudo ./example_app
```

```
[root@centos7 build]# pwd
/root/programming/lwip/contrib/ports/unix/example_app/build
[root@centos7 build]# cmake -DLWIP_DIR=/root/programming/lwip/contrib/ports/unix/example_app/ ..
[root@centos7 example_app]# pwd
/root/programming/lwip/contrib/ports/unix/example_app
[root@centos7 example_app]#  make -j16
```

## 编译iperf2

***用iperf3 connect有问题***

```
git clone https://github.com/lynxis/iperf2.git
```

## run

***不需要网桥***

```
brctl delif lwipbridge  tap0
```

![image](pic/ping.png)

![image](pic/iperf.png)

```
[root@centos7 ~]# ping 192.168.1.200
PING 192.168.1.200 (192.168.1.200) 56(84) bytes of data.
64 bytes from 192.168.1.200: icmp_seq=1 ttl=255 time=0.122 ms
64 bytes from 192.168.1.200: icmp_seq=2 ttl=255 time=0.110 ms
64 bytes from 192.168.1.200: icmp_seq=3 ttl=255 time=0.034 ms
^C
--- 192.168.1.200 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2102ms
rtt min/avg/max/mdev = 0.034/0.088/0.122/0.040 ms
```