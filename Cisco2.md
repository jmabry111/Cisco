[Networking Fundamentals and Concepts](Cisco1.md) | [List](index.html) | [Module 3](Cisco3.md)

MODULE 2 LESSON 1
=================

# Shared (Switched) LAN

## LAN Segment Limitations

*	LAN Segment: a part of network where every device communicates using the same physical medium
*	Signals degrade with transmission distance
*	Each Ethernet type has a max segment length
*	LANS can be extended by adding a layer 1 device (hub or repeater) or layer 2 device (switch or bridge)
*	Extending segments can cause
	*	sharing bandwidth
	*	extending cable distances
	*	repeating or amplifying signals

### Collisions

*	Each port on a hub is a member of a single collision domain
	*	Every device hears every other device that is connected to any port on the hub
*	On a switch, each port has it's own collision domain
	*	Devices can only hear broadcast traffic from other devices on the *same port*

### Carrier Sense Multiple Access with Collision Detection

![CSMA/CD](images/csmacd.png)


MODULE 2 LESSON 2
=================

# Solving challenges with Switched LAN Technology

### Bridges
	
*	Divide an Ethernet LAN into multiple segments for more collision domains
*	Layer 2 Device
*	Forward, Filter, or flood frames
*	Have few ports
*	SLOW

### Switches

*	Also Layer 2
*	Forward, filter, or flood frames based on MAC address tables
*	Have many full-duplex ports to segment a large LAN into many smaller segments
*	Fast, support different port speeds

### LAN Switches

*	High port density
*	Large frame buffers
*	Mixture of port speed
*	Fast internal switching
*	Low per-port cost
*	Switching modes:
	*	Store-and-Forward - Variable latency
	*	Cut-through
		*	Fragment-free - Waits 64 bytes - potentially corrupts data
		*	Cut-through (fast-forward) - Sends as soon as the destination MAC address field is read - potentially corrupts data

**Features**
*	Dedicated Communication between devices
*	Multiple simultaneous conversatinos
*	Full-Duplex communication - only if there are no hubs
*	Media-Rate adaption

## Switching Frames

1. 	The switch receives a broadcast from PC A on Port 1
2. 	The switch enters the MAC address and the switch port that received the frame into the MAC table
3. 	Because destination address is broadcast, the switch floods the frame to all ports, except the source port
4.	The destination device replies to the broadcast with a unicast frame destined to PC A
5.	The switch enters the source MAC address of PC B and the address of the port that received the frame in the the MAC table; the destination address of the frame and and its associated port is found in the MAC table
6.	The switch can now forward frames between source and destination devices without flooding, b/c it has entries in the MAC table that identify the associated ports

### Frame Forwarding

1.	Switches learn where MAC addresses are by looking at the source MAC Address in a frame
2.	Switches forward frames based on the destination MAC address 
	*	if they know the location, they forward it to 1 port
	*	if they don't know the MAC yet, they flood
	*	broadcasts are always flooded
	*	unicasts are flooded if the destination has not yet been learned
3.	Switches will rewrite their MAC Address table immediately if they detect a change
	
	![Frame Forwarding](images/frameforwarding.png)
	

### LANs today
	
*	Users grouped by physical location
*	More switches added to networks
*	Support advanced features:
	*	Port security
	*	VLANs
	*	Port speeds
	*	PoE
	*	Link aggregation
	
	

MODULE 2 LESSON 3
=================




