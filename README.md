# keepalived
This repo demonstrates the core functionality of Keepalived using `docker-compose`.

## Prerequisite
* `docker version`:
```
Client:
 Version:           18.09.8
 API version:       1.39
 Go version:        go1.10.8
 Git commit:        0dd43dd87f
 Built:             Wed Jul 17 17:41:19 2019
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.8
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.8
  Git commit:       0dd43dd
  Built:            Wed Jul 17 17:07:25 2019
  OS/Arch:          linux/amd64
  Experimental:     false
```
* `docker-compose version`
```
docker-compose version 1.24.0, build 0aa59064
docker-py version: 3.7.2
CPython version: 3.6.8
OpenSSL version: OpenSSL 1.1.0j  20 Nov 2018
```

## Get Started
* `docker-compose up -d`
* `docker-compose logs m1`:
```
Attaching to keepalived_m1_1
m1_1  | Wed Dec  2 03:41:47 2020: Starting Keepalived v1.3.9 (10/21,2017)
m1_1  | Wed Dec  2 03:41:47 2020: Opening file '/etc/keepalived/keepalived.conf'.
m1_1  | Wed Dec  2 03:41:47 2020: Starting Healthcheck child process, pid=6
m1_1  | Wed Dec  2 03:41:47 2020: Starting VRRP child process, pid=7
m1_1  | Wed Dec  2 03:41:47 2020: Opening file '/etc/keepalived/keepalived.conf'.
m1_1  | Wed Dec  2 03:41:47 2020: Registering Kernel netlink reflector
m1_1  | Wed Dec  2 03:41:47 2020: Registering Kernel netlink command channel
m1_1  | Wed Dec  2 03:41:47 2020: Registering gratuitous ARP shared channel
m1_1  | Wed Dec  2 03:41:47 2020: Opening file '/etc/keepalived/keepalived.conf'.
m1_1  | Wed Dec  2 03:41:47 2020: Using LinkWatch kernel netlink reflector...
m1_1  | Wed Dec  2 03:41:48 2020: VRRP_Instance(VRRP1) Transition to MASTER STATE
m1_1  | Wed Dec  2 03:41:49 2020: VRRP_Instance(VRRP1) Entering MASTER STATE
```
* `docker-compose logs m2`:
```
Attaching to keepalived_m2_1
m2_1  | Wed Dec  2 03:41:46 2020: Starting Keepalived v1.3.9 (10/21,2017)
m2_1  | Wed Dec  2 03:41:46 2020: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Wed Dec  2 03:41:46 2020: Starting Healthcheck child process, pid=6
m2_1  | Wed Dec  2 03:41:46 2020: Starting VRRP child process, pid=7
m2_1  | Wed Dec  2 03:41:46 2020: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Wed Dec  2 03:41:46 2020: Registering Kernel netlink reflector
m2_1  | Wed Dec  2 03:41:46 2020: Registering Kernel netlink command channel
m2_1  | Wed Dec  2 03:41:46 2020: Registering gratuitous ARP shared channel
m2_1  | Wed Dec  2 03:41:46 2020: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Wed Dec  2 03:41:46 2020: Using LinkWatch kernel netlink reflector...
m2_1  | Wed Dec  2 03:41:46 2020: VRRP_Instance(VRRP1) Entering BACKUP STATE
```
* `docker-compose exec m1 ip address`:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
651: eth0@if652: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:1f:ee:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.31.238.2/24 brd 172.31.238.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet 172.31.238.100/24 scope global secondary eth0
       valid_lft forever preferred_lft forever
```
* `docker-compose exec m2 ip address`:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
653: eth0@if654: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:1f:ee:03 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.31.238.3/24 brd 172.31.238.255 scope global eth0
       valid_lft forever preferred_lft forever
```
* `docker-compose stop m1`:
```
Stopping keepalived_m1_1 ... done
```
* `docker-compose exec m2 ip address`:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
653: eth0@if654: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:1f:ee:03 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.31.238.3/24 brd 172.31.238.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet 172.31.238.100/24 scope global secondary eth0
       valid_lft forever preferred_lft forever
```
* `docker-compose logs m2`
```
Attaching to keepalived_m2_1
m2_1  | Wed Dec  2 03:41:46 2020: Starting Keepalived v1.3.9 (10/21,2017)
m2_1  | Wed Dec  2 03:41:46 2020: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Wed Dec  2 03:41:46 2020: Starting Healthcheck child process, pid=6
m2_1  | Wed Dec  2 03:41:46 2020: Starting VRRP child process, pid=7
m2_1  | Wed Dec  2 03:41:46 2020: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Wed Dec  2 03:41:46 2020: Registering Kernel netlink reflector
m2_1  | Wed Dec  2 03:41:46 2020: Registering Kernel netlink command channel
m2_1  | Wed Dec  2 03:41:46 2020: Registering gratuitous ARP shared channel
m2_1  | Wed Dec  2 03:41:46 2020: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Wed Dec  2 03:41:46 2020: Using LinkWatch kernel netlink reflector...
m2_1  | Wed Dec  2 03:41:46 2020: VRRP_Instance(VRRP1) Entering BACKUP STATE
m2_1  | Wed Dec  2 03:46:17 2020: VRRP_Instance(VRRP1) Transition to MASTER STATE
m2_1  | Wed Dec  2 03:46:18 2020: VRRP_Instance(VRRP1) Entering MASTER STATE
```

## References
* <http://manpages.ubuntu.com/manpages/xenial/man8/keepalived.8.html>
* <https://docs.oracle.com/cd/E37670_01/E41138/html/section_uxg_lzh_nr.html>: where I mainly copied the code.
* <https://www.redhat.com/sysadmin/advanced-keepalived>: It mention the directives `notify`, `notify_master`.
* <https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/load_balancer_administration/keepalived_install_example1>
* <http://manpages.ubuntu.com/manpages/xenial/man5/keepalived.conf.5.html>
* <https://blog.csdn.net/u013256816/article/details/49356689>
* <https://www.opencli.com/linux/ip-command>
* <https://manpages.debian.org/testing/keepalived/keepalived.conf.5.en.html>: a good reference manual.
