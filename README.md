# network

___________________________________________________________
## ip command
```
ip a
ip addr show
ip addr flush dev eth1
ip addr add 192.168.1.1/24 dev eth1
ip link set eth1 up
```

* DNS
```
cat /etc/resolv.conf

systemd-resolve --status
```

## Activate a network interface on the boot
ONBOOT="yes" is in /etc/sysconfig/network-scripts/ifcfg-eth0

##
```bash
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
PROXY_METHOD=none
BOOTPROTO=none
ONBOOT=yes
#PREFIX=24
IPADDR=192.168.203.136
DEVICE=ens33
UUID=83f2c89f-2c51-48a6-948d-9f982bbce60a
DEFROUTE=yes
GATEWAY=192.168.203.2
DNS1=192.168.203.2
DNS2=8.8.8.8
```
____________________________________________________________
* Use netplan
```
ls /etc/netplan/
00-installer-config.yaml  01-installer-config.yaml

cat /etc/netplan/00-installer-config.yaml
# This is the network config written by 'subiquity'
network:
  ethernets:
    ens3:
      dhcp4: false
      addresses:
        - 192.168.0.54/24
      gateway4: 192.168.0.254
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1, 127.0.0.53]
  version: 2

netplan --debug apply

# 2 interfaces
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      addresses:
       - 192.168.2.2/24
      dhcp4: no
      routes:
       - to: 192.168.2.0/24
         via: 192.168.2.1
         table: 101
      routing-policy:
       - from: 192.168.2.0/24
         table: 101
    ens5:
      addresses:
       - 192.168.22.2/24
      dhcp4: no
      gateway4: 192.168.22.1
      routes:
       - to: 192.168.22.0/24
         via: 192.168.22.1
         table: 102
      routing-policy:
        - from: 192.168.22.0/24
          table: 102
  
netplan --debug apply
```

## Change mac addr
## On linux
```
ifconfig eth0  hw ether 00:1e:21:e3:1a:1a
```


## On mac
```
ifconfig en0 ether 000:1e:21:e3:1a:1a
```
