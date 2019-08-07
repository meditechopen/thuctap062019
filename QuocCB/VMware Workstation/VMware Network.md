### VMware Network

1. **Introduction to Vitual Networking in VMware Workstation**.

Which's virtual network, as created by VMware Workstation. Which connects your virtual machine to the physical network.
Typically, the most importance thing you want physical network connectivity for is to connect a VM to the local LAN and then to the Internet.
After all, just like your desktop or laptop, your VMs need Internet access to browse the web or check email, for example.
VMs also need access to enterprise apps that are running on the local LAN.

By default, VMware Workstation offers 3 types of virtual networks – NAT, bridged, and host-only. 

**Three Types Of Virtual Networks In Workstation, By Default:**

Bridged = VMnet0

NAT = VMnet8

Host-only = VMnet1

Used to manage the virtual networks, here’s what the Workstation Virtual Network Editor looks like.

<img src=https://i.imgur.com/4TS82kJ.png>

Additional notes:

- The virtual DHCP server serves NAT and host-only networks.

- You can create your own custom VMnet networks.

- Virtual network adaptors are in each VM and you can add multiple, if needed.


**Understanding VMware Workstation NAT Networks**

*NAT gives a virtual machine access to Network resources using the host computer IP'address*

A network access translation connection is set up automatically if you follow the **Custom** path in the New Virtual Machine Winzard and select **Use network address translation**

If you want to connect to the Internet or other TCP/IP Network using the host computer's dial up networking or broadband connection and you are not able to give your virtual machine an IP address on the external network, NAT is often the easiest way to give your virtual machine access to that network.

NAT also allows you to connect to a TCP/IP network using a Token Ring adapter on the host computer.

If you use NAT, your virtual machine does not have its own IP address on the external network. Instead, a separate private network is set up on the host computer. Your virtual machine gets an address on that network from the VMware virtual DHCP server. The VMware NAT device passes network data between one or more virtual machines and the external network. It identifies incoming data packets intended for each virtual machine and sends them to the correct destination.

If you select NAT, the virtual machine can use many standard TCP/IP protocols to connect to other machines on the external network. For example, you can use HTTP to browse Web sites, FTP to transfer files and Telnet to log on to other computers. In the default configuration, computers on the external network cannot initiate connections to the virtual machine. That means, for example, that the default configuration does not let you use the virtual machine as a Web server to send Web pages to computers on the external network.

If you make some other selection in the New Virtual Machine Wizard and later decide you want to use NAT, you can make that change in the virtual machine settings editor (VM > Settings). For details, see Changing the Networking Configuration.


**Understanding VMware Workstation Bridged Networks**

Bridged networking connects a virtual machine to a network using the host computer's Ethernet adapter.

Bridged networking is set up automatically if you select Use bridged networking in the New Virtual Machine Wizard or if you select the Typical setup path. This selection is available on a Linux host only if you enable the bridged networking option when you install VMware Workstation.

If your host computer is on an Ethernet network, this is often the easiest way to give your virtual machine access to that network. Linux and Windows hosts can use bridged networking to connect to both wired and wireless networks.

If you use bridged networking, your virtual machine needs to have its own identity on the network. For example, on a TCP/IP network, the virtual machine needs its own IP address. Your network administrator can tell you whether IP addresses are available for your virtual machine and what networking settings you should use in the guest operating system. Generally, your guest operating system may acquire an IP address and other network details automatically from a DHCP server, or you may need to set the IP address and other details manually in the guest operating system.

If you use bridged networking, the virtual machine is a full participant in the network. It has access to other machines on the network and can be contacted by other machines on the network as if it were a physical computer on the network.

Be aware that if the host computer is set up to boot multiple operating systems and you run one or more of them in virtual machines, you need to configure each operating system with a unique network address. People who boot multiple operating systems often assign all systems the same address, since they assume only one operating system will be running at a time. If you use one or more of the operating systems in a virtual machine, this assumption is no longer true.

If you make some other selection in the New Virtual Machine Wizard and later decide you want to use bridged networking, you can make that change in the virtual machine settings editor (VM > Settings). For details, see Changing the Networking Configuration.

**Understanding VMwara Host-only Networks**

Host-only Network creates a network that is completely contained within the host computer.

A host-only network is set up automatically if you select Use Host-only Networking in the New Virtual Machine Wizard. On Linux hosts, this selection is available only if you enabled the host-only networking option when you installed VMware Workstation.

Host-only networking provides a network connection between the virtual machine and the host computer, using a virtual Ethernet adapter that is visible to the host operating system. This approach can be useful if you need to set up an isolated virtual network.

If you use host-only networking, your virtual machine and the host virtual adapter are connected to a private Ethernet network. Addresses on this network are provided by the VMware DHCP server.

If you make some other selection in the New Virtual Machine Wizard and later decide you want to use host-only networking, you can make that change in the virtual machine settings editor (VM > Settings). For details, see Changing the Networking Configuration. 