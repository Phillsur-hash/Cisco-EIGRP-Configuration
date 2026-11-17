Cisco-EIGRP-Configuration

Overview

This project demonstrates the configuration and implementation of Enhanced Interior Gateway Routing Protocol (EIGRP) dynamic routing between two Cisco routers: New York (NY) and Los Angeles (LA).

EIGRP is an advanced distance-vector routing protocol developed by Cisco. It enables routers to dynamically exchange routing information, establish neighbor relationships, and determine optimal paths to destination networks.

The objective of this lab is to configure EIGRP, establish neighbor adjacencies, exchange routing information, verify dynamically learned routes, and test end-to-end network connectivity using ICMP ping.
Network Topology

The lab consists of two Cisco routers connected through a shared transit network.
Device	Interface	IP Address	Network
Router 1 (NY)	G0/0	192.168.20.1	192.168.20.0/24
Router 1 (NY)	G0/1	192.168.10.1	192.168.10.0/24
Router 2 (LA)	G0/0	192.168.20.2	192.168.20.0/24
Router 2 (LA)	G0/1	192.168.30.1	192.168.30.0/24
Network Diagram
text

          New York (NY) Router
                  NY
                   |
          G0/1     |     G0/0
     192.168.10.1  |  192.168.20.1
                   |
            192.168.20.0/24
                   |
          G0/0     |     G0/1
     192.168.20.2  |  192.168.30.1
                   |
          Los Angeles (LA)
                   |
            192.168.30.0/24
                   |
             Host: 192.168.30.10

Technologies Used

    Cisco IOS
    Cisco Routers
    Enhanced Interior Gateway Routing Protocol (EIGRP)
    IPv4 Addressing
    Dynamic Routing
    Cisco Diffusing Update Algorithm (DUAL)
    ICMP (Ping)
    Cisco Command Line Interface (CLI)

EIGRP Configuration

Both routers were configured using EIGRP Autonomous System (AS) Number 10.
1. Router 1 – New York (NY)

Enter privileged EXEC mode and global configuration mode:
NY> enable
NY# conf t

Enable EIGRP using Autonomous System Number 10:
NY(config)# router eigrp 10

Advertise the connected networks:
NY(config-router)# network 192.168.20.0
NY(config-router)# network 192.168.10.0

Verify the routing table:
NY(config-router)# do show ip route

NY Routing Table Results:

    192.168.10.0/24 – Directly connected.
    192.168.20.0/24 – Directly connected.

The following message appeared after configuring EIGRP:
%DUAL-5-NBRCHANGE: IP-EIGRP 10:
Neighbor 192.168.20.2 (GigabitEthernet0/0)
is up: new adjacency

This confirms that the New York router successfully established an EIGRP neighbor relationship with the Los Angeles router.
2. Router 2 – Los Angeles (LA)

Enter privileged EXEC mode and global configuration mode:
LA> enable
LA# conf t

Enable EIGRP using Autonomous System Number 10:
LA(config)# router eigrp 10

Advertise the connected networks:
LA(config-router)# network 192.168.20.0
LA(config-router)# network 192.168.30.0

Verify the routing table.
LA(config-router)# do show ip route

The following message appeared after configuring EIGRP:
text

%DUAL-5-NBRCHANGE: IP-EIGRP 10:
Neighbor 192.168.20.1 (GigabitEthernet0/0)
is up: new adjacency

This confirms that the Los Angeles router successfully established an EIGRP neighbor relationship with the New York router.

LA Routing Table Results:

    192.168.20.0/24 – Directly connected.
    192.168.30.0/24 – Directly connected.
    192.168.10.0/24 – Learned through EIGRP.

The following routing table entry confirms that LA successfully learned the New York network through EIGRP:
D 192.168.10.0/24 [90/28416] via 192.168.20.1,
  GigabitEthernet0/0

This demonstrates that EIGRP successfully exchanged routing information between the two routers.
Routing Table Verification

The routing tables confirm that the routers successfully exchanged routing information through EIGRP.

Understanding Routing Table Codes
Code	Meaning
C	Directly Connected
L	Local Interface Address
D	EIGRP Internal Route
EX	EIGRP External Route
O	OSPF Learned Route
R	RIP Learned Route
S	Static Route
Understanding the EIGRP Route
text

D 192.168.10.0/24 [90/28416] via 192.168.20.1

    D: Route learned through EIGRP.
    192.168.10.0/24: Destination network.
    90: EIGRP administrative distance.
    28416: EIGRP composite metric.
    192.168.20.1: Next-hop router (NY).

The administrative distance of 90 identifies the route as an internal EIGRP route. The metric of 28416 represents the calculated path cost used by EIGRP to select routes.
Connectivity Testing

After completing the EIGRP configuration, an ICMP ping test was performed to verify end-to-end network connectivity.

Test Destination: 192.168.30.10

Command:
C:\> ping 192.168.30.10

Ping Test Results:

Pinging 192.168.30.10 with 32 bytes of data:

Reply from 192.168.30.10: bytes=32 time<1ms TTL=126
Reply from 192.168.30.10: bytes=32 time=1ms TTL=126
Reply from 192.168.30.10: bytes=32 time=4ms TTL=126
Reply from 192.168.30.10: bytes=32 time<1ms TTL=126

Ping statistics for 192.168.30.10:
    Packets: Sent = 4,
    Received = 4,
    Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:
    Minimum = 0ms,
    Maximum = 4ms,
    Average = 1ms

Ping Test Summary
Metric	Result
Destination IP	192.168.30.10
Packets Sent	4
Packets Received	4
Packets Lost	0
Packet Loss	0%
Minimum Response Time	0ms
Maximum Response Time	4ms
Average Response Time	1ms

Result: Successful connectivity.

All four ICMP packets received responses, confirming successful communication with the destination host.
EIGRP Verification Commands

The following Cisco IOS commands can be used to verify EIGRP operation and routing information.
show ip route
show ip eigrp neighbors
show ip eigrp topology
show ip protocols
show ip eigrp interfaces
show running-config

Command	Purpose
show ip route	Displays the routing table
show ip eigrp neighbors	Displays EIGRP neighbor relationships
show ip eigrp topology	Displays EIGRP topology information
show ip protocols	Displays active routing protocols
show ip eigrp interfaces	Displays EIGRP-enabled interfaces
show running-config	Displays the current router configuration
Project Results

The EIGRP configuration was successfully implemented between the New York and Los Angeles routers.

The following objectives were achieved:

    Configured EIGRP on both Cisco routers.
    Used Autonomous System Number 10.
    Advertised connected networks through EIGRP.
    Successfully established EIGRP neighbor adjacencies.
    Verified neighbor relationships through DUAL adjacency messages.
    Confirmed dynamically learned routes using show ip route.
    Verified the EIGRP internal route to 192.168.10.0/24.
    Completed an end-to-end ping test with 0% packet loss.

Conclusion

This lab demonstrates how EIGRP enables dynamic routing between separate networks using Cisco routers.

By configuring EIGRP with Autonomous System Number 10 on the New York and Los Angeles routers, both devices successfully established neighbor relationships and exchanged routing information.

The routing table verification confirmed that the Los Angeles router dynamically learned the New York network through EIGRP with an administrative distance of 90 and a composite metric of 28416.

The DUAL neighbor adjacency messages further confirmed successful communication between the routers.

Finally, the successful ping test to 192.168.30.10, with four packets transmitted and zero packets lost, demonstrated end-to-end network connectivity.

This project provided hands-on experience with Cisco IOS, EIGRP configuration, DUAL, neighbor adjacency verification, routing table analysis, and network troubleshooting.

Project Name: Cisco-EIGRP-Configuration
Routing Protocol: EIGRP
Autonomous System Number: 10
Routers: New York (NY) and Los Angeles (LA)
Connectivity Test: Successful (0% Packet Loss)
