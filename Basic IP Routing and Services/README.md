My first showcase is a demonstration of some more complex integrations of routing, including redistribution, multiple routing protocols, as well as a few IP services. 
I've decided to use Cisco Packet Tracer instead of GNS3 or CML because of how quick it is to get things spinning up, as well as not having a limit on the number of running devices.
There is, however, quite a few limitations that I encounter due to this, such as not being able to summarize routes, utilize QoS, use IPSec to protect a GRE tunnel, and much more. It isn't perfect, but it gets the idea accross. 

This is the the starting topology I've decided to represent the internet.

<img alt="Initial Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/Initial%20Topology.png" />

I've decided that I want to use BGP to get things rolling on the internet side of things, but first, some basic IP connectivity is required.

<img alt="First Connection" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/First%20Connection.png" />
<img alt="Full Basic Connectivity" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/Full%20Basic%20Connectivity.png" />

Just wrapping up a simple BGP configuration. Packet Tracer unfortunately doesn't have many in-depth options for BGP, so I'm mainly focusing on getting some basic connectivity going.

<img alt="First BGP Connections with ping" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/First%20BGP%20Connection%20with%20ping.png" />
<img alt="Full BGP" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/Full%20BGP.png" />

Something I've discovered during this project is that iBGP peering is not supported in Packet Tracer, so every adjacency formed will have to be eBGP. Another fantastic reason to not use it for a skills showcase at this level. I'll be using
CML or GNS3 for future showcases.

Here I've decided to add a branch that connects to the "internet". Here I start to implement some IGPs. Mainly OSPF for this section, but I do include a small bit of EIGRP later.

<img alt="First OSPF Adjacency" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/First%20OSPF%20Adjacency.png" />

Here is a complete OSPF Area 0 with full adjacency.

<img alt="OSPF Area 0 Complete" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/OSPF%20Area%200%20Complete.png" />

Now, finally, here is the full topology, with an implementation of a LAN as well as another representation of a branch connection that uses EIGRP.

<img alt="Complete Config" src="https://github.com/sweetcriminal/Portfolio/blob/main/Basic%20IP%20Routing%20and%20Services/Images/Complete%20Config.png" />


Now, a couple things to note:

I largely left most security settings unconfigured. Packet Tracer doesn't support many of them and, quite frankly, it just wasn't meant to be the star of the show here.
DPT01-R1 is configured as a DHCP server for the access part of the LAN. I've also established a GRE tunnel from DPT01-R1 over to EXT01
