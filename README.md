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
m1_1  | Mon Jan 11 03:48:32 2021: Starting Keepalived v2.0.19 (10/19,2019)
m1_1  | Keepalived[1]: Starting Keepalived v2.0.19 (10/19,2019)
m1_1  | Mon Jan 11 03:48:32 2021: WARNING - keepalived was build for newer Linux 5.4.18, running on Linux 4.15.0-122-generic #124-Ubuntu SMP Thu Oct 15 13:03:05 UTC 2020
m1_1  | Keepalived[1]: WARNING - keepalived was build for newer Linux 5.4.18, running on Linux 4.15.0-122-generic #124-Ubuntu SMP Thu Oct 15 13:03:05 UTC 2020
m1_1  | Mon Jan 11 03:48:32 2021: Command line: 'keepalived' '-l' '-n'
m1_1  | Keepalived[1]: Command line: 'keepalived' '-l' '-n'
m1_1  | Mon Jan 11 03:48:32 2021: Opening file '/etc/keepalived/keepalived.conf'.
m1_1  | Keepalived[1]: Opening file '/etc/keepalived/keepalived.conf'.
m1_1  | Mon Jan 11 03:48:32 2021: Starting VRRP child process, pid=8
m1_1  | Keepalived[1]: Starting VRRP child process, pid=8
m1_1  | Mon Jan 11 03:48:32 2021: Registering Kernel netlink reflector
m1_1  | Keepalived_vrrp[8]: Registering Kernel netlink reflector
m1_1  | Mon Jan 11 03:48:32 2021: Registering Kernel netlink command channel
m1_1  | Keepalived_vrrp[8]: Registering Kernel netlink command channel
m1_1  | Mon Jan 11 03:48:32 2021: Opening file '/etc/keepalived/keepalived.conf'.
m1_1  | Keepalived_vrrp[8]: Opening file '/etc/keepalived/keepalived.conf'.
m1_1  | Mon Jan 11 03:48:32 2021: Registering gratuitous ARP shared channel
m1_1  | Keepalived_vrrp[8]: Registering gratuitous ARP shared channel
m1_1  | Mon Jan 11 03:48:32 2021: (VRRP1) Entering BACKUP STATE (init)
m1_1  | Keepalived_vrrp[8]: (VRRP1) Entering BACKUP STATE (init)
m1_1  | Mon Jan 11 03:48:35 2021: (VRRP1) Entering MASTER STATE
m1_1  | Keepalived_vrrp[8]: (VRRP1) Entering MASTER STATE
```
* `docker-compose logs m2`:
```
Attaching to keepalived_m2_1
m2_1  | Mon Jan 11 03:48:36 2021: Starting Keepalived v2.0.19 (10/19,2019)
m2_1  | Mon Jan 11 03:48:36 2021: WARNING - keepalived was build for newer Linux 5.4.18, running on Linux 4.15.0-122-generic #124-Ubuntu SMP Thu Oct 15 13:03:05 UTC 2020
m2_1  | Mon Jan 11 03:48:36 2021: Command line: 'keepalived' '-l' '-n'
m2_1  | Mon Jan 11 03:48:36 2021: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Mon Jan 11 03:48:36 2021: Starting VRRP child process, pid=8
m2_1  | Mon Jan 11 03:48:36 2021: Registering Kernel netlink reflector
m2_1  | Mon Jan 11 03:48:36 2021: Registering Kernel netlink command channel
m2_1  | Mon Jan 11 03:48:36 2021: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Mon Jan 11 03:48:36 2021: Registering gratuitous ARP shared channel
m2_1  | Mon Jan 11 03:48:36 2021: (VRRP1) Entering BACKUP STATE (init)
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
* `docker-compose exec m1 ls -al I_am_master`:
```
-rw------- 1 root root 0 Jan 11 03:48 I_am_master
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
* `docker-compose exec m2 ls -al I_am_backup`
```
-rw------- 1 root root 0 Jan 11 03:48 I_am_backup
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
* `docker-compose exec m2 ls -al I_am_master`
```
-rw------- 1 root root 0 Jan 11 03:56 I_am_master
```
* `docker-compose logs m2`
```
Attaching to keepalived_m2_1
m2_1  | Mon Jan 11 03:48:36 2021: Starting Keepalived v2.0.19 (10/19,2019)
m2_1  | Mon Jan 11 03:48:36 2021: WARNING - keepalived was build for newer Linux 5.4.18, running on Linux 4.15.0-122-generic #124-Ubuntu SMP Thu Oct 15 13:03:05 UTC 2020
m2_1  | Mon Jan 11 03:48:36 2021: Command line: 'keepalived' '-l' '-n'
m2_1  | Mon Jan 11 03:48:36 2021: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Mon Jan 11 03:48:36 2021: Starting VRRP child process, pid=8
m2_1  | Mon Jan 11 03:48:36 2021: Registering Kernel netlink reflector
m2_1  | Mon Jan 11 03:48:36 2021: Registering Kernel netlink command channel
m2_1  | Mon Jan 11 03:48:36 2021: Opening file '/etc/keepalived/keepalived.conf'.
m2_1  | Mon Jan 11 03:48:36 2021: Registering gratuitous ARP shared channel
m2_1  | Mon Jan 11 03:48:36 2021: (VRRP1) Entering BACKUP STATE (init)
m2_1  | Mon Jan 11 03:56:18 2021: (VRRP1) Backup received priority 0 advertisement
m2_1  | Mon Jan 11 03:56:19 2021: (VRRP1) Entering MASTER STATE
```

## Troubleshooting
* I personally found that when using `ubuntu:18.04` default `keepalived` of version `v1.3.9`, sending `SIGTERM` to the top parent will not successfully forwards the `SIGTERM` signal to its children and grandchildren. After updating to `v2.0.19 `, it will behave as its manual specifys.
    * older version:
        ```
        keepalived --version
        Keepalived v1.3.9 (10/21,2017)

        Copyright(C) 2001-2017 Alexandre Cassen, <acassen@gmail.com>

        Build options:  PIPE2 IPV4_DEVCONF LIBNL3 RTA_ENCAP RTA_EXPIRES RTA_NEWDST RTA_PREF RTA_VIA FRA_OIFNAME FRA_SUPPRESS_PREFIXLEN FRA_SUPPRESS_IFGROUP FRA_TUN_ID RTAX_CC_ALGO RTAX_QUICKACK FRA_UID_RANGE LWTUNNEL_ENCAP_MPLS LWTUNNEL_ENCAP_ILA LIBIPTC LIBIPSET_DYNAMIC LVS LIBIPVS_NETLINK IPVS_DEST_ATTR_ADDR_FAMILY IPVS_SYNCD_ATTRIBUTES IPVS_64BIT_STATS VRRP VRRP_AUTH VRRP_VMAC SOCK_NONBLOCK SOCK_CLOEXEC GLOB_BRACE OLD_CHKSUM_COMPAT FIB_ROUTING INET6_ADDR_GEN_MODE SNMP_V3_FOR_V2 SNMP SNMP_KEEPALIVED SNMP_CHECKER SNMP_RFC SNMP_RFCV2 SNMP_RFCV3 DBUS SO_MARK
        ```
    * Newer version (after updating to `ubuntu:20.04`:
        ```
        keepalived --version
        Keepalived v2.0.19 (10/19,2019)

        Copyright(C) 2001-2019 Alexandre Cassen, <acassen@gmail.com>

        Built with kernel headers for Linux 5.4.18
        Running on Linux 4.15.0-122-generic #124-Ubuntu SMP Thu Oct 15 13:03:05 UTC 2020

        configure options: --build=x86_64-linux-gnu --prefix=/usr --includedir=${prefix}/include --mandir=${prefix}/share/man --infodir=${prefix}/share/info --sysconfdir=/etc --localstatedir=/var --disable-silent-rules --libdir=${prefix}/lib/x86_64-linux-gnu --runstatedir=/run --disable-maintainer-mode --disable-dependency-tracking --with-kernel-dir=debian/ --enable-snmp --enable-sha1 --enable-snmp-rfcv2 --enable-snmp-rfcv3 --enable-dbus --enable-json --enable-bfd --enable-regex build_alias=x86_64-linux-gnu CFLAGS=-g -O2 -fdebug-prefix-map=/build/keepalived-sJIe_4/keepalived-2.0.19=. -fstack-protector-strong -Wformat -Werror=format-security LDFLAGS=-Wl,-Bsymbolic-functions -Wl,-z,relro CPPFLAGS=-Wdate-time -D_FORTIFY_SOURCE=2

        Config options:  NFTABLES LVS REGEX VRRP VRRP_AUTH JSON BFD OLD_CHKSUM_COMPAT FIB_ROUTING SNMP_V3_FOR_V2 SNMP_VRRP SNMP_CHECKER SNMP_RFCV2 SNMP_RFCV3 DBUS

        System options:  PIPE2 SIGNALFD INOTIFY_INIT1 VSYSLOG EPOLL_CREATE1 IPV4_DEVCONF IPV6_ADVANCED_API LIBNL3 RTA_ENCAP RTA_EXPIRES RTA_NEWDST RTA_PREF FRA_SUPPRESS_PREFIXLEN FRA_SUPPRESS_IFGROUP FRA_TUN_ID RTAX_CC_ALGO RTAX_QUICKACK RTEXT_FILTER_SKIP_STATS FRA_L3MDEV FRA_UID_RANGE RTAX_FASTOPEN_NO_COOKIE RTA_VIA FRA_OIFNAME FRA_PROTOCOL FRA_IP_PROTO FRA_SPORT_RANGE FRA_DPORT_RANGE RTA_TTL_PROPAGATE IFA_FLAGS IP_MULTICAST_ALL LWTUNNEL_ENCAP_MPLS LWTUNNEL_ENCAP_ILA NET_LINUX_IF_H_COLLISION LIBIPVS_NETLINK IPVS_DEST_ATTR_ADDR_FAMILY IPVS_SYNCD_ATTRIBUTES IPVS_64BIT_STATS IPVS_TUN_TYPE IPVS_TUN_CSUM IPVS_TUN_GRE VRRP_VMAC VRRP_IPVLAN IFLA_LINK_NETNSID CN_PROC SOCK_NONBLOCK SOCK_CLOEXEC O_PATH GLOB_BRACE INET6_ADDR_GEN_MODE VRF SO_MARK SCHED_RT SCHED_RESET_ON_FORK
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
    * Don't run scripts configured to be run as root if any part of the path is writable by a non-root user.
* [How do I enable: script_security?](https://github.com/acassen/keepalived/issues/901)
* [Unsafe permission found for script 'xxx.sh' -disabling](https://github.com/acassen/keepalived/issues/1372)
    * I found that you have to set the permission so that only the user can modify that scrip.
* [Official man page](https://www.keepalived.org/manpage.html)
