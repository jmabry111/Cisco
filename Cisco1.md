MODULE 1 LESSON 1
=================
Catalyst Switches
-----------------
	Low end switches
	Lots of similarities to higher end switches
	
Physical components
-------------------
	RJ-45
	NIC
	
![Symbols](NetworkIcons.png)
	
> show ip interface brief - overview of ports

>Fa - Fast Ethernet
>Gi - Gigabit Ethernet
>Te - 10Gig Ethernet

###Rollover cable = Console Cable 
	really serial on both ends, just has RJ-45 on router end
	
VPN
---
	IPsec
	SSL or Web VPN - basically uses https technology
	
Network user applications
-------------------------
	Email
	Web browsing
	IM
	Collaboration
	Databases
	Mobile phone apps
	peer to peer - Skype, BitTorrent, Joost, etc
	Online Gaming
	
Impact of user applications on network
--------------------------------------
###	Batch Applications
*		FTP, TFTP, inventory updates
*		No direct human interaction
*		Bandwidth is important, but not critical
		
###	Interactive Applications
*		Inventory inquiries, database updates
*		Human to machine interaction
*		B/c human is waiting for a response, response time is important, but not critical, unless wait is too long
	
###	Real-time Applications
*		VoIP, video
*		human to human interaction
*		Gaming
*		end to end latency is critical
		
Characteristics of network
--------------------------
*	Speed			measure of how fast data is transmitted - bps
*	Cost			indicates general cost of network components
*	Security		indicates how easily or difficult the network is to access as well as the data that is transmitted. 
*	Availability 	measure of the probability that the network will be available for use when it is required
					Calculated by dividing the uptime by total time in a year times 100
*	Scalability		how well the network can expand and accomodate more uses and data transfer requirements
*	Reliability		dependability of the network components, measured as probability of failure or mean time between failures (MTBF)
*	Topology 		Physical - arrangement of the cables, network devices, and end systems
					Logical - the path that the data signals take through the physical topology
					
Physical Topologies
-------------------
	Bus		All devices receive all signals
	
	Ring	Signals travel around a ring
			Multiple single points of failure
			
	Star	Transmission thru a central point
			Single point of failure
			
	Extended-Star	More scalable than star
					Most common
					
	Full Mesh		Highly fault tolerant
					Expensive
					
	Partial-Mesh	Trade off between redundancy and cost
	
	
Connections to internet
-----------------------
*	Wireless
*	Fiber
*	Copper
	

MODULE 1 LESSON 2
=================

###Security - always keep in mind no matter what you are doing on network

*Closed network - not connected to internet
*Open network - has connection to internet

Classes of attacks
------------------
	Passive		Traffic analysis, monitoring of unprotected communications, decrypting traffic, capturing authentication infomation
	Active		Attempts to circumvent or break protection features, introduce malicious code, steal or modify information
				Can result in disclosure of sensitive data, DoS, or modification of data
	Close-in	Ordinary individuals attaining close physical proximity to networks, systems, or facilities for modifying, gathering or denying access to data
	Insider		Can be malicious or non-malicious. Used for eavesdropping or snooping or can result from carlessness, lack of knowledge or lack of network security
	Distributed	Focus on malicious modification of hardware or software during distribution. Add a "back door" to the software or hardware.
	
Common threats
--------------
###	Physical:
		Hardware threats
		Environmental threats
		Electrical threats
		Maintenance threats
###	Reconnaissance:
		Learing information about target network by using available applications and information
###	Access:
		Used to retrieve data
		Used to gain access
		Used to Escalate access privileges
###	Password:
		Password crackers and guessers
		
Password Attack Threat Mitigation
---------------------------------
*	No default passwords
*	Do not allow users to use same password on multiple systems
*	Disable accounts after certain # of incorrect attempts
*	Do not use cleartext passwords
*	Use strong - non-dictionary passwords
	
>	sh run | include secret 
>	sh run | include password
>	login block-for 43200 attempts 10 within 90 - blocks all users for 1/2 day
	
	tomas - enable secret cracker - brute force
	tomas -cns <hash>
	

![Threats](threats.png)

MODULE 1 LESSON 3
==================
Host-to-Host communications model
----------------------------------

###Try to adhere to Standardized model as much as possible

#OSI Model
7.	Application
6.	Presentation
5.	Session
4.	Transport
3.	Network
2.	Data Link
1.	Physical

###All People Seem To Need Data Processing
###Please Do Not Throw Sausage Pizza Away


###Why layered network?
*	Reduces complexity
*	Standardizes interfaces
*	Facilitates modular engineering
*	Ensures interoperable tehnology
*	Accelerates evolution
*	Simplifies teaching and learning

Layers
------
###Physical:
*	Binary Transmission - defines electrical, mechanical, procedural, and functional specs for activating, maintaining, and deactivating the physical link
						- Defines how we encode data for transmission
** 	Hubs, cables, terminators, jacks

###Data Link:
*	Access to Media 
	*	defines how data is formatted for transmission and how access to network is controlled
	*	Provides error detection
	*	Describes HOW we transmit data
	*	MAC Addresses, switches, 

###Network:
*	Data Delivery 
	*	Routes data packets, Provides error detection, Provides logical addressing and path selection
	*	Routers, routing enabled switches, IPv4/IPv6 addresses

###Transport:
*	End-to-End Connections 
	*	Handles transportation issues between hosts 
	*	Ensures data transport reliability
	*	Establishes, maintains, and terminates virtual circuits
	*	Provides reliability through fault detection and recovery information flow control
	*	UDP, TCP

###Sessions:
*	Interhost Communications 
	*	Establishes, manages, and terminates sessions between applications
	*	Allows multiple tabs for example
							
###Presentation:
*	Data Representation 
	*	Ensures that data is readable by receiving systems
	*	Formats & Structures data
	*	Negotiates data transfer syntax for application layer
	*	Provides encryption
	*	method for encoding audio, video (format), text formatting, image format

###Application
*	Network Processes to Applications 
	*	Provides network services to application processes (email, ftp, terminal emulation)
	*	Provides authentication
	*	API basically, developers' "hook" into the network stack
	

##Data Encapsulation

Start with user data. As it travels down the layers (starting from 7), each layer wraps the data with its own information. 

##De-Encapsulation

Each layer takes the info from its layer's header and remove it and send it to the next layer.

![Encapsulation Diagram](encapsulation.png)
![Data-link Layer](data-link.png)
![Network Layer](network.png)
![Transport Layer](transport.png)

##Peer to Peer Communication
*	Physical Layer - Bits			Bacon		Birthdays
*	Data link Layer - Frames		Frying		Fear
*	Network Layer - Packets			Produces	People
*	Transport Layer - Segments		Salivation	Some
*	Session - Application Layers - Data

## TCP/IP Stack
###Application
	*	Represents data users
	*	Encodes & controls dialog
###Transport
	*	Supports communication between end devices across diverse network
###Internet
	*	Provides logical addressing and determines best path through network
###Network access
	*	Controls the hardware devices and media that make up the network
	
![Summary](1.63Summary.png)




