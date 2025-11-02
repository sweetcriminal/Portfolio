# DMVPN Demonstration

In this demonstration, I will be implementing a DMVPN protected with IPSec, and advertising networks (represented by loopback interfaces) across the DMVPN.

Here is the initial topology with basic connectivity. The only configurations made on the Internet router are those that will allow basic connectivity. Other than that, it is completely untouched.

<img alt="Initial Topology" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/Initial%20Topology.png" />

After establishing tunnels, NHRP needed to be configured. That peership is shown here.
The NBMA (public IP) address of the spoke routers are represented by those in the 15.0.0.0/28 series of networks. Being able to
group these IP addresses together in that 15.0.0.0 range makes the IPSec configuration later on a bit easier.

<img alt="NHRP Peers" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/NHRP%20Peers.png" />

Here is the ISAKMP and IPSec configuration between R1-Sp and HUB. At this point, the tunnel protection is established and working as planned.

<img alt="First IPSec" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/First%20IPSec.png" />

I've copied the configuration across all the spoke routers and verified connectivity with the following pings. The tunnel network is 192.168.1.0/24. R1-Sp's tunnel IP address is 192.168.1.2, which is why it isn't shown in the list of pings.
No need to ping itself! 192.168.1.1 is the tunnel IP of HUB, and .3 and .4 are the other spokes.

<img alt="IPSec Pings" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/IPSec%20Pings.png" />

Shown here is the full configuration for the DMVPN and for the IPSec protection!

<img alt="Show Run Spoke1 and Hub" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/Show%20Run%20Spoke1%20and%20Hub.png" />

To wrap things up, I need some loopbacks configured and advertised across this DMVPN.

I've configured each spoke with a loopback that matches their number. R1-Sp has 1.1.1.1, R2-Sp has 2.2.2.2, R3-Sp has 3.3.3.3, and HUB has 4.4.4.4, all with /32 masks.

This configuration has been copied and altered to match each individual device. The only significant difference is that 
split-horizon has been disabled on the HUB, but it is still enabled on the spokes. The networks learned through the tunnel interface need to be advertised back
out of that interface, so disabling it is pretty important.

<img alt="EIGRP Config" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/EIGRP%20Config.png" />

And just like that, the routes and adjacencies populate.

<img alt="EIGRP IP Route" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/EIGRP%20IP%20Route.png" />
<img alt="EIGRP Neighbors" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/EIGRP%20Neighbors.png" />

All that's left is to verify that all the loopbacks can be pinged. I'll be testing this from R1-Sp.

<img alt="EIGRP Loopback Pings" src="https://github.com/sweetcriminal/Portfolio/blob/main/DMVPN%20Demonstration/Images/EIGRP%20Loopback%20Pings.png" />

#### Success! This concludes my DMVPN demonstration!
