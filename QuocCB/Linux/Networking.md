### How to Configure CentOS 7 Network Settings

#### Common Settings

**GATEWAY:** The IP address of your network gateway. Required if you require connectivity beyond your local network subnet, such as having Internet connectivity.

**IPADDR:** The IP address of the network interface.

##### Configuring a Static IP

1. A static address is one that is permanently assigned to one host. It is an address that is manually configured by the administrator.

Open the configuration file for your network interface.
    
   >vi /etc/sysconfig/network-scripts/ifcfg-eth0

2. Add the following settings to the file:

>DEVICE=eth0<br>
>ONBOOT=yes<br>
>IPADDR=192.168.1.10<br>
>NETMASK=255.255.255.0<br>
>GATEWAY=192.168.1.1<br>

3. Save your changes and exit
4. Your new settings will not apply until the network interface is restarted or brought online. If you are remotely logged into the server and modifying the network settings of the interface you are connected to, reboot the system.
5. Restarting the network interface.

>ifdown eht0

>ifup eth0

##### Configuring DHCP Settings
A dynamic address is one leased from a DHCP server when a system boots or a network interface comes online. The following settings configure a network interface for DHCP.

1. Open the configuration file for your network interface.
vi /etc/sysconfig/network-scripts/ifcfg-
2. Add the following settings. If a configuration already exists, modify it to look like the following:

>DEVICE=eth0<br>
ONBOOT=yes<br>
BOOTPROTO=dhcp


3. Save your changes and exit
4. Your new settings will not apply until the network interface is restarted or brought online. If you are remotely logged into the server and modifying the network settings of the interface you are connected to, reboot the system.
5. Restarting the network interface.

>ifdown eth0

>ifup eth0

