# PacketTracer-GRE-Tunnel
Packet Tracer project for configuring GRE tunnels between two routers to establish private network communication.


# Packet Tracer - Configuring GRE Tunnel

## Description
This project demonstrates how to configure a **GRE Tunnel** between two routers in Cisco Packet Tracer, enabling communication between remote networks.

## Topology
- **Router A (RA)**: Connects to **192.168.1.0/24** and has a GRE tunnel to **Router B (RB)**.
- **Router B (RB)**: Connects to **192.168.2.0/24** and establishes the tunnel with **RA**.

## Addressing Table
| Device | Interface  | IP Address        | Subnet Mask       | Default Gateway |
|--------|-----------|-------------------|-------------------|----------------|
| RA     | G0/0      | 192.168.1.1       | 255.255.255.0     | N/A            |
|        | S0/0/0    | 64.103.211.2      | 255.255.255.252   | N/A            |
|        | Tunnel 0  | 10.10.10.1        | 255.255.255.252   | N/A            |
| RB     | G0/0      | 192.168.2.1       | 255.255.255.0     | N/A            |
|        | S0/0/0    | 209.165.122.2     | 255.255.255.252   | N/A            |
|        | Tunnel 0  | 10.10.10.2        | 255.255.255.252   | N/A            |

## Configuration Steps

### 1. **Verify Router Connectivity**
Run the following commands to check interface configurations:
```sh
show ip interface brief
ping <Remote_Router_IP>
interface tunnel 0
 ip address 10.10.10.1 255.255.255.252
 tunnel source s0/0/0
 tunnel destination 209.165.122.2
 tunnel mode gre ip
 no shutdown
interface tunnel 0
 ip address 10.10.10.1 255.255.255.252
 tunnel source s0/0/0
 tunnel destination 209.165.122.2
 tunnel mode gre ip
 no shutdown
interface tunnel 0
 ip address 10.10.10.2 255.255.255.252
 tunnel source s0/0/0
 tunnel destination 64.103.211.2
 tunnel mode gre ip
 no shutdown
RA(config)# ip route 192.168.2.0 255.255.255.0 10.10.10.2
RB(config)# ip route 192.168.1.0 255.255.255.0 10.10.10.1
ping 192.168.2.2  (From PCA)
ping 192.168.1.2  (From PCB)
traceroute 192.168.2.2

