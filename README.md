# 001-Basic-DHCP-config

Cisco DHCP Client Configuration Lab
This repository contains the configuration for a Cisco router acting as a DHCP client to receive a public IP address from an ISP, as per the FlackBox lab 23-1 DHCP Configuration. The lab demonstrates how to set up a router's outside interface as a DHCP client, verify the assignment, and optionally set up internal DHCP services. The external DHCP server (ISP) is pre-configured, and the focus is on the client side.
Lab Description
In this lab, you perform a DHCP configuration for a small campus network. You configure a router's outside interface as a DHCP client to receive a public IP from the ISP. Later, you can extend it to internal DHCP services using the router or an external server. Note: The external DHCP server at 10.10.20.10 is not used until the last part of the lab.
Prerequisites

Cisco router (e.g., 2811 or similar in Packet Tracer).
Outside interface connected to the ISP (simulated DHCP server).
Internal LAN interface for optional DHCP server setup.

Configuration Commands (Cisco DHCP Client)
Configure the outside interface (FastEthernet 0/0) on R1 to receive its IP via DHCP:

```
Configure terminalterface f0/0
 ip address dhcp
 no shutdown
end
write memory

E
```
Explanation

ip address dhcp: Configures the interface as a DHCP client to request an IP from the ISP.
no shutdown: Brings the interface up.
The ISP is already configured – you have no access to it.


```
show ip int brief

```

```
Interface IP-Address OK? Method Status Protocol
FastEthernet0/0 203.0.113.2 YES DHCP up up
FastEthernet0/1 unassigned YES unset administratively down down
FastEthernet1/0 unassigned YES unset administratively down down
FastEthernet1/1 unassigned YES unset administratively down down
Vlan1 unassigned YES unset administratively down down

```
Log message: %DHCP-6-ADDRESS_ASSIGN: Interface FastEthernet0/0 assigned DHCP address 203.0.113.2, mask 255.255.255.0, hostname R1
