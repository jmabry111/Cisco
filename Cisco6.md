[Router & WAN Config](Cisco5.md)  |  [List](index.html)

MODULE 6 LESSON 1
==================

# CDP

## Creating a Network Map
**A network topology map is critical in network management**

## Cisco Discovery Protocol
*	CDP is a proprietary utility that gathers information about direct-connected Cisco switches, routers, and other devices
*	CDP discovers neighboring devices, regardless of which protocol suite they are running
*	Physical media must support the SNAP encapsulation
*	LLDP - alternative standards-based discovery protocol
*	Runs on Cisco IOS devices
*	By default, each device sends messages every 60 seconds to directly connected Cisco devices
*	Summary information includes:
	*	Device identifiers
	*	Address list
	*	Port identifier
	*	Capabilities list
	*	Platform

### Using CDP
	Router#show cdp neighbors
	Router#show cdp neighbors detail

### Enabling/Disabling CDP
*Can disable globally or on a specific interface*

	RouterA(config)#no cdp run
	RouterA(config-if)#no cdp enable

	RouterA#show cdp traffic


MODULE 6 LESSON 2
==================
