

# 네트워크 설정하기 (고정 아이피 설정)
1. IP Address
2. Subnet Mask
3. Gateway IP Address
4. DNS Server IP Address



###  3. Gateway IP Address
윈도우 cmd에서 게이트웨이 주소를 찾는다

```
기본 게이트웨이 . . . . . . : 192.168.200.254
```

```
C:\Users\SHK>ipconfig

Windows IP 구성

이더넷 어댑터 VirtualBox Host-Only Network:

   연결별 DNS 접미사. . . . :
   링크-로컬 IPv6 주소 . . . . : 
   IPv4 주소 . . . . . . . . . : 
   서브넷 마스크 . . . . . . . : 255.255.255.0
   기본 게이트웨이 . . . . . . :

이더넷 어댑터 이더넷:

   연결별 DNS 접미사. . . . :
   링크-로컬 IPv6 주소 . . . . : 
   IPv4 주소 . . . . . . . . . : 
   서브넷 마스크 . . . . . . . : 255.255.255.0
   기본 게이트웨이 . . . . . . : 192.168.200.254
```

###  1. IP Address
###  2. Subnet Mask
inet 192.168.200.200

```
inet 192.168.200.200  netmask 255.255.255.0 
```

```
[root@lx01 ~]# ifconfig
enp0s3: flags=<UP,BROADCAST,RUNNING,MULTICAST>  mtu 
        inet 192.168.200.200  netmask 255.255.255.0  broadcast 192.168.200.255
        inet6  prefixlen 64  scopeid 0x20<link>
        ether txqueuelen  (Ethernet)
        RX packets 4102  bytes 366771 (358.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2537  bytes 452540 (441.9 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=<UP,LOOPBACK,RUNNING>  mtu 
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 109  bytes 8990 (8.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 109  bytes 8990 (8.7 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### 위에서 적은 내용 사용

```
cd /etc/sysconfig/network-scrips/ifcfg-
[root@lx01 network-scripts]# vi ifcfg-enp0s3


TYPE=Ethernet
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
NAME=enp0s3
UUID=
DEVICE=enp0s3
ONBOOT=yes
PEERDNS=yes
PEERROUTES=yes
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_PRIVACY=no

IPADDR=192.168.200.200
NETMASK=255.255.255.0
GATEWAY=192.168.200.254

```

### 네트워크 다시시작 

```
systemctl restart network.service  
```


