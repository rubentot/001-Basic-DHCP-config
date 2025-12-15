# 001-Basic-DHCP-config

Cisco DHCP Configuration Lab – CCNA Practice Project
This repository demonstrates a complete Cisco router configuration for DHCP services in a small campus network, based on the FlackBox lab 23-1 DHCP Configuration. The lab covers:

Configuring the router's outside interface as a DHCP client to receive a public IP from the ISP.
Setting up the router as an internal DHCP server for LAN clients.
Excluding reserved IPs and specifying DNS/gateway.

This project showcases fundamental CCNA skills in IP addressing, DHCP client/server setup, and network connectivity. It's designed to simulate a real-world edge router scenario where the WAN receives a public IP via DHCP, and the LAN gets private IPs automatically.
Lab Topology Overview

Router R1:
Outside interface (Fa0/0): DHCP client – receives public IP from ISP (e.g., 203.0.113.2/24).
Internal interface: Serves DHCP for LAN (e.g., 10.10.10.0/24).

External DHCP server (10.10.20.10): Used in later lab steps (not configured here).
PCs/clients on LAN receive IPs via router's DHCP pool.

![Lab Topology](/Topology.png)

Key Configuration Highlights
1. DHCP Client on WAN Interface
```
interface FastEthernet0/0
 ip address dhcp
 no shutdown
```
R1 requests and receives a public IP from the ISP (pre-configured DHCP server).

2. Internal DHCP Server
```
ip dhcp excluded-address 10.10.10.1 10.10.10.10   ! Reserve for servers/printers
ip dhcp pool LAN_POOL
 network 10.10.10.0 255.255.255.0
 default-router 10.10.10.1
 dns-server 10.10.20.10
 lease 7
```
```
interface FastEthernet0/1   ! Internal LAN interface
 ip address 10.10.10.1 255.255.255.0
 no shutdown
```
Pool assigns 10.10.10.11–254.
Gateway = router's LAN IP.
DNS = 10.10.20.10 (external server in lab).

Verification Commands
```
textshow ip interface brief          ! Check WAN IP from DHCP
show ip dhcp pool                ! View pool status
show ip dhcp binding             ! Leased IPs
show ip dhcp server statistics   ! DHCP stats
```
Skills Demonstrated

DHCP client configuration for WAN.
DHCP server setup with exclusions, gateway, DNS.
Interface activation and IP assignment.
Troubleshooting DHCP leases and bindings.
