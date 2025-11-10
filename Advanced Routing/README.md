# Advanced Routing

Here I will demonstrate some more advanced routing implementations. I intend to use OSPF, BGP, and EIGRP in unison. Here is the basic topology I've decided to go with.
<br/>

## Setting things up

R1 and R2 will be iBGP neighbors in AS 65001 and Internet will be an eBGP neighbor in AS 20000. Both R1 and R2 are configured with a default route that points to Internet.


<img alt="Initial Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/1%20Initial%20Topology.png"/>

I've made this full mesh topology into OSPF Area 0 and marked it as such.

<img alt="OSPF Area 0" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/2%20OSPF%20Area%200.png"/>

You can see the routing table for R1 here, showing all the OSPF and BGP learned routes.

<img alt="OSPF and BGP Routes" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/3%20OSPF%20and%20BGP%20Routes.png" />
<br/>

## Crossing the Internet

The first branch needs something to reach across the internet, so I've made this 2nd branch here.

<img alt="Second Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/4%20Second%20Topology.png"/>

I created 2 GRE tunnels from R1 and R2 over the Internet node that provide redundant connections to R5. R1, R2, and R5 all have default routes that point to the internet, which is how they're able to reach each other initially. I then wanted R5 to be a part of OSPF, but in area 1. I was able to successfully form that adjacency, as shown here:

<img alt="OSPF Adjacency over GRE" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/5%20OSPF%20Adjacency%20over%20GRE.png"/>

Forming a GRE tunnel across the internet, however, is not secure. Here is my working IPSec configuration applied to both tunnels:


<img alt="Configured GRE and IPSEC" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/6%20Configured%20GRE%20and%20IPSec.png"/>

Now, at this point, I need to see if I can actually reach networks behind the tunnel. Here I'm pinging from R3 (which is behind the tunnel in OSPF Area 0) to R5's 
loopback 0 interface. As you can see, I am successful!


<img alt="Fake R5 Network" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/7%20Ping%20R5%20Fake%20Network.png"/>

I figure that I should also verify that my tunnels actually provide the redundancy I want them to. I decided to shutdown the tunnel source interface (which is also the direct connection to the internet) and run a traceroute to R5's loopback. Looks like it took the path I wanted it to, so that's another success!


<img alt="Redundancy Test" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/8%20Redundancy%20Test.png"/>

Taking a step back a bit, I noticed that the routing table was getting a little crowded and that it could be summarized. Both R1 and R2 are both ABRs and ASBRs, so they advertize many of the same routes and therefore need similar configurations. Here's my implementation:


<img alt="OSPF Summary" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/9%20OSPF%20Summary.png"/>

There have been a lot of changes over the course of this project. Here's an updated look at the topology with some new labelling.


<img alt="Full Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/10%20Full%20Topology.png"/>


As you can see, I've taken the liberty of changing a couple things. I figured it was about time EIGRP got involved, so I made an off-shoot from R5 and had them form an adjacency. I currently have Area 1 as an NSSA, so this should still work just fine. I redistributed all of my OSPF routes into EIGRP so that way R6 has a way to reach the other side of the tunnel.

Just as hoped, the tunnel routes are there, and all the OSPF routes from the other side of the tunnel are there.

In order to get things pinging from one side to the other, I'll need to set up a static route on R1 and R2 to know how to reach this new EIGRP network without redistributing back into OSPF (although, that is also an option depending on certain limitations).

<img alt="Redistributed Routes R6" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/11%20Redistributed%20Routes%20R6.png"/>

Now, all that's left is to verify that I can reach R6 from OSPF Area 0. Here is a traceroute form R3.

<img alt="Traceroute to R6" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/12%20Traceroute%20to%20R6.png" />
<br/>

## More IP Services
<b/>

### DHCP Relay
<b/>

I know that it is generally poor practice to place a DHCP server so far away from clients that need it (especially across the internet), but, in the spirit of showcasing skills, I've decided to make R6 (across the internet) a DHCP server for our users connected to OSPF Area 0.


