## Chapter 4. Networking

We examine networking and networking interfaces.
By the end of this section, you should be able to:
Explain how the system looks at networking interfaces and configures and uses them with ip and ifconfig.​​

## Networking and Network Interfaces

The vast majority of network programming in Linux is done using the socket interface. Thus, standards-compliant programs should require little massage to work properly with Linux.

However, there are many enhancements and new features in the Linux networking implementation, such as new kinds of address and protocol families. For example, Linux offers the netlink interface, which permits opening up socket connections between kernel sub-systems and applications (or other kernel sub-systems). This has been effectively deployed to implement firewall and routing applications.

Historically, the wired Ethernet network devices have been known by a name such as **eth0, eth1, etc.,** while wireless devices have had names like **wlan0, wlan1, etc.**

## ip Utility

Basic information about active network interfaces on your system is gathered through both the **ip utility**, or the **older ifconfig** program:

```
$ ip -s link

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    RX: bytes  packets  errors  dropped missed  mcast   
    26092      363      0       0       0       0       
    TX: bytes  packets  errors  dropped carrier collsns 
    26092      363      0       0       0       0       
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether 08:62:66:45:4d:16 brd ff:ff:ff:ff:ff:ff
    RX: bytes  packets  errors  dropped missed  mcast   
    769457748  598391   0       0       0       11526   
    TX: bytes  packets  errors  dropped carrier collsns 
    39740293   289292   0       0       0       0       
    altname enp0s25
```

Information displayed includes information about the hardware MAC address, the MTU (maximum transfer unit), and the IRQ the device is tied to. Also displayed are the number of packets and bytes transmitted, received, or resulting in errors.

This machine has a network card bound to eno1, and the loopback interface, lo, which handles network traffic bound to the machine. You can see the statistical information in abbreviated form by looking at /proc/net/dev, and in one quantity per line display in /sys/class/net/eno1/statistics:

```
$ ls -l /sys/class/net/eno1/statistics

total 0
-r--r--r-- 1 root root 4096 Feb 10 11:55 collisions
-r--r--r-- 1 root root 4096 Feb 10 11:55 multicast
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_bytes
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_compressed
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_crc_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_dropped
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_fifo_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_frame_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_length_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_missed_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_nohandler
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_over_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 rx_packets
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_aborted_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_bytes
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_carrier_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_compressed
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_dropped
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_fifo_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_heartbeat_errors
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_packets
-r--r--r-- 1 root root 4096 Feb 10 11:55 tx_window_errors
```

## Using Predictable Network Interface Device Names

Simply naming network devices as eth0, eth1, etc., can be problematic when multiple interfaces exist, or when the order in which the system probes for and then finds them is not deterministic and can depend on kernel version and options.

Many system administrators have solved this problem in a simple manner, by hard-coding associations between hardware (MAC) addresses and device names in system configuration files and startup scripts.

A more modern approach is offered by the Predictable Network Interface Device Names scheme, which is strongly correlated with the use of udev and integration with systemd. There are now five types of names that devices can be given:

1. Incorporating Firmware or BIOS provided index numbers for on-board devices; for example, eno1.
2. Incorporating Firmware or BIOS provided PCI Express hotplug slot index numbers; for example, ens1.
3. Incorporating physical and/or geographical location of the hardware connection; for example, enp2s0.
4. Incorporating the MAC address; for example, enx7837d1ea46da.
5. Using the old classic method; for example, eth0.

For example, on a machine with two onboard PCI network interfaces that would have been eth0 and eth1 in the older naming system:

```
$ ip -s link | grep eno

2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT
↪   group default qlen 1000
3: eno2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT
↪   group default qlen 1000
```

It is easy to turn off the new scheme and go back to the classic names, if so desired.

To bring a network connection up and get it an assigned address from a DHCP server:
```
$ sudo ip link set eno1 up
$ sudo dhclient eno1
```

To bring a network connection up and assign a static address:
```
$ sudo ip link set eno1 up
$ sudo ip addr add 192.168.1.100 dev eno1
```

While ifconfig has been used reliably for many years, the **ip utility is newer (and far more versatile) than ifconfig**. On a technical level it is more efficient because it uses netlink sockets rather than ioctl system calls.

ip can be used for a wide variety of tasks. It can be used to display and control devices, routing, policy-based routing, and tunneling. The basic syntax is:
**ip [ OPTIONS ] OBJECT { COMMAND | help }**

Some examples include:

```
Show information for all network interfaces:
$ ip link

Show information for the eth0 network interface:
$ ip -s link show eth0

Set the IP address for eth0:
$ sudo ip addr add 192.168.1.7 dev eth0

Bring eth0 down:
$ sudo ip link set eth0 down

Set the MTU to 1480 bytes for eth0:
$ sudo ip link set eth0 mtu 1480

Set the networking route:
$ sudo ip route add 172.16.1.0/24 via 192.168.1.5
```

## Lab 4.1. Static Configuration of a Network Interface

Problem:
You may have to use a different network interface name than eth0. Furthermore, you can most easily do this exercise with nmtui or your system’s graphical interface. We will present a command line solution, but beware details may not exactly fit your distribution flavor or fashion.

Show your current IP address and default route for eth0.
Bring down eth0 and reconfigure to use a static address instead of DCHP, using the information you just recorded.
Bring the interface back up.
Make sure your configuration works after a reboot.
You will probably want to restore your configuration when you are done.

Solution:

```
## Show your current IP address and default route for eth0
$ ip addr show eth0
or
$ ifconfig eth0

## Bring down eth0 and reconfigure to use a static address instead of DCHP, using the information you just recorded
## Assuming the address was 192.168.1.100:
$ sudo ip link set eth0 down
$ sudo ip addr add 192.168.1.200 dev eth0
$ sudo ip link set eth0 up
or
$ sudo ifconfig eth0 down
$ sudo ifconfig eth0 up 192.168.1.100
$ sudo ip link set eth0 up
$ sudo dhclient eth0
or
$ sudo ifconfig eth0 up
$ sudo dhclient eth0
$ sudo reboot
```

