## Chapter 4. Networking

We examine networking and networking interfaces.
By the end of this section, you should be able to:
Explain how the system looks at networking interfaces and configures and uses them with ip and ifconfig.​​

## Networking and Network Interfaces

The vast majority of network programming in Linux is done using the socket interface. Thus, standards-compliant programs should require little massage to work properly with Linux.

However, there are many enhancements and new features in the Linux networking implementation, such as new kinds of address and protocol families. For example, Linux offers the netlink interface, which permits opening up socket connections between kernel sub-systems and applications (or other kernel sub-systems). This has been effectively deployed to implement firewall and routing applications.

Historically, the wired Ethernet network devices have been known by a name such as **eth0, eth1, etc.,** while wireless devices have had names like **wlan0, wlan1, etc.**
