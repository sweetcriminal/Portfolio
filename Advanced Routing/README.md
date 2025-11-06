Here I will demonstrate some more advanced routing implementations. I intend to use OSPF, BGP, and EIGRP in unison. Here is the basic topology I've decided to go with.
R1 and R2 will be iBGP neighbors in AS 65001 and Internet will be an eBGP neighbor in AS 20000. Both R1 and R2 are configured with a default route that points to Internet.


<img alt="Initial Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/1%20Initial%20Topology.png"/>

I've made this full mesh topology into OSPF Area 0 and marked it as such.

<img alt="OSPF Area 0" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/2%20OSPF%20Area%200.png"/>

You can see the routing table for R1 here, showing all the OSPF and BGP learned routes.

<img alt="OSPF and BGP Routes" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/3%20OSPF%20and%20BGP%20Routes.png" />

The first branch needs something to reach across the internet, so I've made this 2nd branch here.

<img alt="Second Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/4%20Second%20Topology.png"/>

I created a GRE tunnel over the Internet node. R1, R2, and R5 all have default routes that point to the internet, which is how they're able to reach each other 
initially. I then wanted R5 to be a part of OSPF, but in area 1. I was able to successfully form that adjacency, as shown here:

<img alt="OSPF Adjacency over GRE" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/5%20OSPF%20Adjacency%20over%20GRE.png"/>














<img alt="" src=""/>
