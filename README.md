# network

## Activate a network interface on the boot
ONBOOT="yes" is in /etc/sysconfig/network-scripts/ifcfg-eth0

##
cat /etc/sysconfig/network-scripts/ifcfg-ens33
#TYPE=Ethernet
#PROXY_METHOD=none
#BROWSER_ONLY=no
#BOOTPROTO=dhcp
#DEFROUTE=yes
#IPV4_FAILURE_FATAL=no
#IPV6INIT=yes
#IPV6_AUTOCONF=yes
#IPV6_DEFROUTE=yes
#IPV6_FAILURE_FATAL=no
#IPV6_ADDR_GEN_MODE=stable-privacy
#NAME=ens33
#UUID=4562c89f-2c45-48a6-948d-9f982bbce60a
#DEVICE=ens33
#ONBOOT=yes


TYPE=Ethernet
BOOTPROTO=none
ONBOOT=yes
PREFIX=24
IPADDR=192.168.203.136
DEVICE=ens33
#UID=4562c89f-2c45-48a6-948d-9f982bbce60a
DEFROUTE=yes
