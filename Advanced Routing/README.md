Here I will demonstrate some more advanced routing implementations. I intend to use OSPF, BPG, and EIGRP in unison. Here is the basic topology I've decided to go with:
R1 and R2 will be iBGP neighbors in AS 65001 and Internet will be an eBGP neighbor in AS 20000. Both R1 and R2 are configured with a default route that points to Internet.


<img alt="Initial Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/1%20Initial%20Topology.png"/>

I've made this full mesh topology into OSPF Area 0 and marked it as such.

<img alt="OSPF Area 0" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/2%20OSPF%20Area%200.png"/>

You can see the routing table for R1 here, showing all the OSPF and BGP learned routes.

<img alt="OSPF and BGP Routes" src="https://github.com/sweetcriminal/Portfolio/blob/main/Advanced%20Routing/Images/3%20OSPF%20and%20BGP%20Routes.png" />















<img alt="" src=""/>
