### IP Header

An **IP header** is a prefix to an **IP packet** that contains information about the **IP version**, **length** of the packet, **source** and **destination IP addresses**, etc. It consists of the following fields:

<img src=https://i.imgur.com/G2QU5R9.jpg>

Here is a description of each field:

- **Version** - The version of the IP Protocol, for IPv4, this field has the value of 4.
- **Header length** - The length of the header in 32-bit words. The minimum value is 20 bytes, and the maximum value is 60 bytes.
- **Priority and Type of Service** - specifies how the datagram should be handled. The first 3 bits are the priority bits.
- **Total length** – the length of the entire packet (header + data). The minimum length is 20 bytes, and the maximum is 65,535 bytes.
- **Identification** – used to differentiate fragmented packets from different datagrams.
- **Flags** – used to control or identify fragments.
- **Fragmented offset** – used for fragmentation and reassembly if the packet is too large to put in a frame.
- **Time to live** – limits a datagram’s lifetime. If the packet doesn’t get to its destination before the TTL expires, it is discarded.
- **Protocol** – defines the protocol used in the data portion of the IP datagram. For example, TCP is represented by the number 6 and UDP by 17.
- **Header checksum** – used for error-checking of the header. If a packet arrives at a router and the router calculates a different checksum than the one specified in this field, the packet will be discarded.
- **Source IP address** – the IP address of the host that sent the packet.
- **Destination IP address** – the IP address of the host that should receive the packet.
- **Options** – used for network testing, debugging, security, and more. This field is usually empty.