[Wireless LANs](Cisco3.md)  |  [List](index.html)  |

# Router Fundamentals
---------------------

MODULE 4 LESSON 1
=================

## Routers

*	Routers have the following components
	*	CPU
	*	Motherboard
	*	Memory
*	Routers have network adapters to which IP addresses are assigned
*	Routers may have 2 kinds of ports
	*	Console/AUX
	*	Network
*	Routers forward packets based on a routing table

### Router Functions
1.	Gathers routing information and inform other routers about changes
2.	Determines where to forward packets
	![Routing Table](images/routingtable.png)
	
**Path determination**
Routers determine the best path to destination

## Routing Tables

**Routing tables list all known destinations and information regarding how to teach them.**
*All routers ahve to know ALL networks*

### Routing entries

**Directly connected** - Router attaches to this network
**Static routing** - Entered manually by an administrator
**Dynamic routing** - Learned by exchange of routing information - RIP, OSPF, EGP, BGP, EIGRP
**Default route** - Statically or Dynamically learned; used when no explicit route to network is known
![Routing Table](images/routingtable2.png)

### Dynamic Routing Protocols

*	Routing Information Protocol (RIP) - Standards based, distance vector routing protocol not well suited for medium to large networks
*	Open Shortest Path First (OSPF) - Standards based link-state routing protocol designed for large networks
*	Enhanced Interior Gateway Routing Protocol (EIGRP) - Cisco Proprietary hybrid routing protocol designed for large networks and offers fast convergence

**Routing Metrics**
*	RIP uses hop count
*	OSPF uses cost
*	EIGRP uses Bandwidth and Delay

### Distance Vector Routing Protocols
	Distance: How far?
	Vector: In which direction?
*	RIPv1, RIPv2, IGRP(Interior Gateway Routing Protocol)
*	Collect distance and vector to neighboring routers
*	Send periodic updates of routing table to neighbors

### Link-state Routing Protocols
*	OSPF, ISIS(Intermediate Systems to Intermediate Systems)
*	Create the network topology map
*	Send event-triggered link-state updates
