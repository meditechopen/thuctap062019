## IPv6 Addressing and Expressions

Ipv6 example:
<img src=https://i.imgur.com/EUzIq0k.png>

- IPv6 has eight groups instead of four.
- The groups are separated by colons instead of period.
- The address is expressed in Hexadecimal just like MAC address is

**Shortened Expressions:**

- To shorten, you have to follow a couple of rules:
  - You can drop any leading zeros in each of the individual blocks.
      
    Example: 2001:0db8:3c4d:0012:0000:0000:1234:56ab -> 2001:db8:3c4d:12:0:0:1234:56ab
  - we can remove the two consecutive blocks of zeros by replacing them with a doubled colom.
  
    Like this: 2001:db8:3c4d:12::1234:56ab

    The rule you have to follow to get away with this is that you can replace only one contiguous block of such zeros
in an address. So if my address has four blocks of zeros and each of them were separated,
I just don’t get to replace them all because I can replace only one contiguous block with a
doubled colon. Check out this example:

    2001:0000:0000:0012:0000:0000:1234:56ab

    You can do this:

    ``2001::12::1234:56ab``<br> Instead, the best you can do is this:<br> ``2001::12:0:0:1234:56ab``

**Address types**

- **Unicast:** Packets addressed to a unicast address are delivered to a single interface. For load balancing, multiple interfaces across several devices can use the same address, but we’ll call that an anycast address.
    
    - **global unicast:** Similar to IPv4 public IP addresses. These addresses are assigned by the IANA and used on public networks. They have a prefix of 2000::/3, (all the addresses that begin with binary 001).




    | 3 bits | 45 bits | 16 bits | 64 bits |
    |--------------------------------------|
    | 001 | Globle Routing prefix | Subnet ID| Interface ID|

     - **unique local:** Similar to IPv4 private addresses. They are used in private networks and aren’t routable on the Internet. These addresses have a prefix of FD00::/8.

    | 8 bits | 40 bits | 16 bits | 64 bits|
    |--------|
    | FD | Globle ID | Subnet ID | interface ID|

     - **link local:** These addresses are used for sending packets over the local subnet. Routers do not forward packets with this addresses to other subnets. IPv6 requires a link-local address to be assigned to every network interface on which the IPv6 protocol is enabled. These addresses have a prefix of FE80::/10.

    | 64 bits | 64 bits |
    |-------------------|
    |FE80:0000:0000:0000|Interface ID|


- **Multicast (FF00::/8):** Multicast addresses in IPv6 are similar to multicast addresses in IPv4. They are used to communicate with dynamic groupings of hosts, for example all routers on the link (one-to-many distribution).

     |8 bits|4 bits|4 bits| 112 bits|
    |---------------|
    |FF|Flags|Scope|Group ID|
