[ACLs](Cisco2-6.md)		|		[Home](index.html)		|		 

# NAT & PAT
------------

MODULE 7 LESSON 1
=================

# Scaling the Network with NAT & PAT

## NAT (Network Address Translation)
*	Allows private users to access the Internet by sharing one or more public IP addresses
*	An IP address is either local or global
*	Local IPv4 addresses are seen inside the network
*	Global IPv4 addresses are seen outside the network
*	Can work in many forms:
	*	Static NAT (one to one) - Servers
	*	Dynamic NAT (many to many) - pool of public addresses
	*	NAT overloading (aka Port Address Translation)(many to one)
*	NAT operation is transparent to users
*	Benefits include improved security and scalability
*	Drawbacks include performance degradation and incompatibility with certain applications that depend on end-to-end functionality.

## PAT
![PAT](images/PAT1.png)

### Translating inside Source address
![static](images/staticnat.gif)

### Configuring and Verifying static nat
*	Establish static translation between an inside local address and an outside global address
	*	*(config)#ip nat inside source static 10.1.1.1 209.165.200.225*
*	Mark the interface as connected to the inside
	*	*(config-if)#ip nat inside*
*	Mark the interface as connected to the outside
	*	*(config-if)#ip nat outside*
*	Display active translations
	*	*show ip nat translations*

### Enabling Static NAT Map
*	*interface s0*
*	*ip address 209.165.200.2 255.255.255.240*
*	*ip nat outside*
*	*interface e0*
*	*ip address 10.1.1.1 255.255.255.0*
*	*ip nat inside*
*	*ip nat inside source static 10.1.1.2 209.165.200.225*
*	*show ip nat translations*
	*	*209.165.20.225	10.1.1.2*

## Dynamic Address Translation
![dynamic](images/dynamicnat.gif)

*	**Syntax:** *Router(config)#ip nat pool name start-ip end-ip {netmask 255.255.255.255 | prefix-length length}*
	*	Define a pool NET209 of global addresses to be allocated as needed
		*	*(config)#ip nat pool NET209 209.165.200.225 209.165.200.238 netmask 255.255.255.240*
*	**Syntax:** *Router(config)#access-list access-list-number permit source [source-wildcard]*
	*	Define a standard IP ACL 1permitting inside local addresses that are to be translated
		*	*(config)#access-list 1 permit 192.168.1.0 0.0.0.255*
*	**Syntax:** *Router(config)#ip nat inside source list access-list-number pool name*
	*	Establish dynamic source translation, specifying the ACL that was defined in the previous step
		*	*(config)#ip nat inside source list 1 NET209*
	*	Display active translations
		*	*Router#show ip nat translations*

![dynamic example](images/dynamicnatex.gif)

## Overloading an Inside Global Address (PAT or NAT Overloading)
![PAT](images/pat2.png)

### Configuring Overloading
*	Define a standard IP ACL 1 permitting inside local addresses that are to be translated
	*	*acces-list 1 permit 192.168.3.0 0.0.0.255*
*	Establish dynamic source translation, specifying the ACL that was defined in the previous step
	*	*ip nat inside source list 1 interface Serial0 overload*
	*	*ip nat inside source list 1 pool POOL overload* - to overload a range of addresses
	*	The overload keyword enables the addition of th port number to the translation
*	Display active translations
	*	*show ip nat translations*

----
	hostname RouterX
	interface e0
		ip address 192.168.3.1 255.255.255.0
		ip nat inside
	interface e1
		ip address 192.168.4.1 255.255.255.0
		ip nat inside
	interface s0
		description to ISP
		ip address 209.165.200.225 255.255.255.240
		ip nat outside
	ip nat inside source list 1 interface Serial0 overload
	ip route 0.0.0.0 0.0.0.0 Serial0
	access-list 1 permit 192.168.3.0 0.0.0.255
	access-list 1 permit 192.168.4.0 0.0.0.255

### Clearing NAT Table
*	clear ip nat translation *
*	clear ip nat translation inside 209.165.200.225 192.168.3.7
*	clear ip nat translation tcp inside 209.165.200.225 1050 192.168.3.7 1050

## Translation not occurring: Translation not installed in table
*	Verify that:
	*	No inbound ACLs are denying the packets entry to the NAT router
	*	The ACL referenced by the NAT command is permitting all necessary networks
	*	There are enough addresses in the NAT pool
	*	The route interfaces are appropriately defined as NAT inside or NAT outside

### NAT Information
*	show ip nat statistics
	*	![stats](images/natstats.png)
*	debug ip nat - will crash router in production environment
	*	![debug](images/natdebug.png)
	
### Translation occurring: Installed translation entry not being used
*	Verify that:
	*	What the nat config is supposed to accomplish
	*	That the nat entry exists in the translation table and that it is accurate
	*	That the translation is actually taking place by monitoring the nAT process or statistics
	*	That the NAT router has the appropriate route in the routing table if the packet is going from inside to outside
	*	That all necessary routers have a return route back to the translated address

![nat problem](images/natproblem.gif)

MODULE 7 LESSON 2
===================

# IPv6

*	IPv4 Address is 32 bits
	*	4 billion addresses
*	IPv6 Address is 128 bits
	*	3.4 x 10<sup>38</sup> addresses

## IPv6 Advanced Features
*	Larger address space
	*	Global reachability and flexibility
	*	Aggregation
	*	Multihoming
	*	Autoconfiguration
	*	Plug-and-play
	*	End to end without NAT
	*	Renumbering
*	Mobility and Security
	*	Mobile IP RFC-compliant
	*	IPsec mandatory (or native) 
*	Simpler header
	*	Routing efficiency
	*	Performance and forwarding rate
	*	No broadcasts
	*	No checksums
	*	Extension headers
	*	Flow labels
*	Transition richness
	*	Dual Stack
	*	Translation

### IPv6 Representation
*	Format:
	*	x:x:x:x:x:x:x:x, where x is a 16bit hexadecimal field
		*	Case-insensitive for hex letters
	*	Leading zeros in a field are optional
	*	Successive fields of zeros can be represented as :: only once per address

### Address types
*	Unicast:
	*	Address is for a single interface
	*	IPv6 has several types (global, reserved, link-local, site-local)
*	Multicast
	*	one to many
	*	enables more efficient use of the network
	*	uses a larger address range
*	Anycast
	*	One-to-nearest (allocated from unicast address space)
	*	Multiple devices share the same address
	*	All anycast nodes should provide uniform service
	*	Source devices send packets to anycast address
	*	Routers decide on closest device to reach the destination
	*	Suitable for load balancing and content delivery service

## Unicast Addressing
*	Types of IPv6 unicast addresses:
	*	Global: Starts with 2000::/3 and assigned by IANA
	*	Reserved: Used by IETF
	*	Private: Link local (starts with FE80::/10) (not routable)
	*	Loopback (::1)
	*	Unspecified (::)
*	A single interface will be assigned multiple IPv6 addresses of any type: unicast, anycast, or multicast
	*	Automatic, static assignment
*	IPv6 addressing rules are covered by multiple RFCs
	*	Architecture defined by RFC 4291
	
### IPv6 breakdown
![breakdown](images/ipv6breakdown.png)

### Link-Local address
*	Dynamically created on all IPv6 interfaces by using FE80::/10 and a 64 bit interface identifier
*	Used for automatic address configuration, neighbor discovery, and router discovery
*	Can serve as a way to connect devices on the same local network without needing global addresses
*	When communicating with a link-local address, you must specify the outgoing interface, because every interface is connected to FE80::/10

### Larger address space enables address aggregation
*	Address Aggregation provides the following benefits
	*	Aggregation of prefixes announced in the global routing table
	*	Efficient and scalable routing
	*	Improved bandwidth and functionality

### Assigning IPv6 Global Unicast Addresses
*	Static assignment
	*	Manual interface ID assignment
	*	EUI-64 interface ID assignment
*	Dynamic assignment
*	Stateless assignment
	*	DHCPv6

###	IPv6 Interface Identifier
*	Cisco can use the EUI-64 format for interface identifiers
*	This format expands the 48-bit mac address to 64 bits by inserting FFFE into the middle 16 bits
*	To make sure that the chosen address is from a unique Ethernet mac address, the U/L bit is set to 1 for global scope (0 for local scope)

