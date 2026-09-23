# Networking Fundamentals Labs

## Overview

This section contains practical networking fundamentals that are
important for cybersecurity, system administration, and network
security.

The purpose of these labs is to develop a strong understanding of how
devices communicate across networks before progressing to network
reconnaissance, traffic analysis, vulnerability assessment, and
penetration testing.

## Lab Environment

- Operating System: Kali Linux
- Virtualization Platform: VirtualBox
- Network Environment: Personal authorized lab
- Primary Interface: eth0
- Tools: Linux networking utilities

## Learning Objectives

The labs in this section will cover:

- OSI and TCP/IP models
- IPv4 addressing
- Subnetting and CIDR notation
- MAC addresses and ARP
- TCP and UDP
- Common ports and protocols
- DNS fundamentals
- DHCP fundamentals
- Routing and default gateways
- Network connectivity and troubleshooting

## Ethical Notice

All networking activities documented in this section are performed
within personal or explicitly authorized lab environments.

The labs are intended for cybersecurity education, networking practice,
and defensive security learning.


---

## Lab 01 - OSI and TCP/IP Models

### Objective

The objective of this lab is to understand the OSI and TCP/IP networking
models and how they describe communication between devices across a
network.

### OSI Model

The OSI (Open Systems Interconnection) model divides network
communication into seven layers:

| Layer | Name | Main Function |
|---|---|---|
| 7 | Application | Provides network services to user applications |
| 6 | Presentation | Handles data formatting, encoding, and encryption |
| 5 | Session | Establishes, manages, and terminates communication sessions |
| 4 | Transport | Provides end-to-end communication using protocols such as TCP and UDP |
| 3 | Network | Handles logical addressing and routing using IP |
| 2 | Data Link | Handles frames, MAC addresses, and local network communication |
| 1 | Physical | Transmits raw bits through physical or wireless media |

### TCP/IP Model

The TCP/IP model is commonly represented using four layers:

| Layer | Examples |
|---|---|
| Application | HTTP, HTTPS, DNS, SSH |
| Transport | TCP, UDP |
| Internet | IPv4, IPv6, ICMP |
| Network Access | Ethernet, Wi-Fi, MAC |

### OSI and TCP/IP Mapping

```text
OSI Model                    TCP/IP Model

7 - Application   ─┐
6 - Presentation  ─┼──────►  Application
5 - Session       ─┘

4 - Transport     ────────►  Transport

3 - Network       ────────►  Internet

2 - Data Link     ─┐
1 - Physical      ─┴──────►  Network Access
```


### Practical - Identify Layer 3 Network Information

To identify the IPv4 configuration of the Kali Linux network interface,
I used the following command:

```bash
ip -4 addr show eth0
```

### Result

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
```

### Explanation

The command displays IPv4 information associated with the `eth0`
network interface.

The important information includes:

- `eth0` - The Ethernet network interface.
- `UP` - The interface is enabled.
- `LOWER_UP` - The network link is operational.
- `10.0.2.15` - The IPv4 address assigned to the Kali Linux system.
- `/24` - The network prefix length.
- `10.0.2.255` - The broadcast address for the network.
- `dynamic` - The IPv4 address was assigned dynamically, normally through DHCP.

The IPv4 address operates at the **Network Layer (Layer 3)** of the OSI
model. Layer 3 addressing allows devices and routers to identify source
and destination networks and route packets between networks.

This practical exercise connects the OSI model with the actual network
configuration of the Kali Linux system.

### Practical - Identify Layer 2 MAC Address

To identify the MAC address of the Kali Linux network interface, I used
the following command:

```bash
ip link show eth0
```

### Result

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP
    link/ether 08:00:27:5a:87:bc brd ff:ff:ff:ff:ff:ff
```

### Explanation

The `ip link show eth0` command displays link-layer information about
the `eth0` network interface.

The important information includes:

- `eth0` - The Ethernet network interface.
- `UP` - The interface is enabled.
- `LOWER_UP` - The underlying network link is operational.
- `link/ether` - Indicates that the following value is an Ethernet MAC address.
- `08:00:27:5a:87:bc` - The MAC address assigned to the `eth0` interface.
- `ff:ff:ff:ff:ff:ff` - The Ethernet broadcast MAC address.

A MAC address operates at the **Data Link Layer (Layer 2)** of the OSI
model. It is used to identify network interfaces when Ethernet frames
are delivered across the local network.

This is different from the IPv4 address `10.0.2.15`, which operates at
the **Network Layer (Layer 3)**.

Therefore, this practical demonstrates two important addressing concepts:

- Layer 2 - MAC Address: `08:00:27:5a:87:bc`
- Layer 3 - IPv4 Address: `10.0.2.15`

Understanding the relationship between Layer 2 and Layer 3 addressing
is important for network troubleshooting, packet analysis, network
reconnaissance, and cybersecurity investigations.

### Lab Conclusion

In this lab, I studied the OSI and TCP/IP networking models and connected
the theoretical concepts to the actual network configuration of a Kali
Linux system.

I identified the IPv4 address used at OSI Layer 3 and the MAC address
used at OSI Layer 2. This demonstrated how different networking layers
perform different functions while working together to enable network
communication.

---

## Lab 02 - IPv4 Addressing and CIDR

### Objective

The objective of this lab is to understand IPv4 addressing, subnet masks,
CIDR notation, network addresses, usable host ranges, and broadcast
addresses.

This lab uses the actual IPv4 configuration of the Kali Linux virtual
machine to demonstrate how an IPv4 network is divided into network and
host portions.

### Current IPv4 Configuration

The Kali Linux system currently uses the following IPv4 configuration:

```text
IPv4 Address: 10.0.2.15
CIDR Prefix:  /24
```

The `/24` CIDR prefix corresponds to the subnet mask:

```text
255.255.255.0
```

### Analyze the IPv4 Network

The following command was used to calculate the network information:

```bash
ipcalc 10.0.2.15/24
```

### Result

```text
Address:   10.0.2.15
Netmask:   255.255.255.0 = 24
Wildcard:  0.0.0.255

Network:   10.0.2.0/24
HostMin:   10.0.2.1
HostMax:   10.0.2.254
Broadcast: 10.0.2.255
Hosts/Net: 254
```

### Explanation

The `ipcalc` command calculates network information from an IPv4 address
and CIDR prefix.

For the address `10.0.2.15/24`, the calculated network information is:

| Property | Value |
|---|---|
| IPv4 Address | `10.0.2.15` |
| CIDR Prefix | `/24` |
| Subnet Mask | `255.255.255.0` |
| Wildcard Mask | `0.0.0.255` |
| Network Address | `10.0.2.0` |
| First Usable Host | `10.0.2.1` |
| Last Usable Host | `10.0.2.254` |
| Broadcast Address | `10.0.2.255` |
| Usable Hosts | `254` |

### Understanding the Network Address

The network address is:

```text
10.0.2.0
```

This address identifies the network itself.

It is not normally assigned to an individual host.

For this `/24` network, all addresses beginning with `10.0.2` belong to
the same IPv4 subnet.

### Understanding the Host Range

The usable host range is:

```text
First Host: 10.0.2.1
Last Host:  10.0.2.254
```

These addresses can be used by devices within the subnet, subject to the
actual network configuration and address allocation.

The Kali Linux virtual machine uses:

```text
10.0.2.15
```

which falls inside this usable host range.

### Understanding the Broadcast Address

The broadcast address is:

```text
10.0.2.255
```

The broadcast address represents all hosts on the local IPv4 subnet and
is not normally assigned to an individual host.

### Understanding CIDR /24

CIDR stands for **Classless Inter-Domain Routing**.

The `/24` value indicates that the first 24 bits of the IPv4 address are
used for the network portion.

```text
IPv4 Address

10       .0        .2        .15
00001010 .00000000 .00000010 .00001111

Subnet Mask

255      .255      .255      .0
11111111 .11111111 .11111111 .00000000
```

The first 24 bits identify the network, while the remaining 8 bits are
available for host addressing.

Therefore:

```text
Network bits = 24
Host bits    = 8
```

The number of addresses available with 8 host bits is:

```text
2^8 = 256 total addresses
```

For a traditional `/24` subnet, the network address and broadcast
address are reserved:

```text
256 - 2 = 254 usable host addresses
```

### Private IPv4 Address

The address `10.0.2.15` belongs to the private IPv4 address space
`10.0.0.0/8`.

Private IPv4 addresses are commonly used inside internal networks and
are not directly routed across the public Internet.

In this lab, the address is assigned to the Kali Linux virtual machine
inside the VirtualBox NAT network.

### Lab Conclusion

In this lab, I analyzed the IPv4 address `10.0.2.15/24` using `ipcalc`.

I identified the subnet mask, network address, usable host range,
broadcast address, and number of usable host addresses.

The practical exercise demonstrated how CIDR notation determines the
network and host portions of an IPv4 address. Understanding IPv4
addressing and CIDR is an important foundation for subnetting, routing,
network reconnaissance, firewall configuration, and network security.


---

## Lab 03 - IPv4 Subnetting

### Objective

The objective of this lab is to understand how a larger IPv4 network can
be divided into smaller subnets using CIDR notation.

In this practical exercise, the original `10.0.2.0/24` network is divided
into two `/25` subnets.

### Original Network

The original network is:

```text
Network:       10.0.2.0/24
Subnet Mask:   255.255.255.0
Host Bits:     8
Total Addresses: 256
Usable Hosts:  254
```

A `/24` prefix uses 24 bits for the network portion and leaves 8 bits for
host addressing.

### Divide the /24 Network into /25 Subnets

Changing the prefix from `/24` to `/25` borrows one bit from the host
portion.

```text
/24 = 24 Network Bits + 8 Host Bits
/25 = 25 Network Bits + 7 Host Bits
```

Borrowing one bit creates:

```text
2^1 = 2 subnets
```

Each `/25` subnet contains:

```text
2^7 = 128 total addresses
```

After excluding the network and broadcast addresses:

```text
128 - 2 = 126 usable host addresses
```

The `/25` subnet mask is:

```text
255.255.255.128
```

### Analyze the First /25 Subnet

The following command was used:

```bash
ipcalc 10.0.2.15/25
```

### Result

```text
Address:   10.0.2.15
Netmask:   255.255.255.128 = 25
Wildcard:  0.0.0.127

Network:   10.0.2.0/25
HostMin:   10.0.2.1
HostMax:   10.0.2.126
Broadcast: 10.0.2.127
Hosts/Net: 126
```

### Explanation

The address `10.0.2.15` belongs to the first `/25` subnet.

The first subnet contains:

| Property | Value |
|---|---|
| Network Address | `10.0.2.0/25` |
| First Usable Host | `10.0.2.1` |
| Last Usable Host | `10.0.2.126` |
| Broadcast Address | `10.0.2.127` |
| Usable Hosts | `126` |

The network address and broadcast address cannot normally be assigned to
individual hosts.

### Analyze the Second /25 Subnet

To verify the second subnet, I analyzed the address `10.0.2.130/25`.

Command:

```bash
ipcalc 10.0.2.130/25
```

### Result

```text
Address:   10.0.2.130
Netmask:   255.255.255.128 = 25
Wildcard:  0.0.0.127

Network:   10.0.2.128/25
HostMin:   10.0.2.129
HostMax:   10.0.2.254
Broadcast: 10.0.2.255
Hosts/Net: 126
```

### Explanation

The address `10.0.2.130` belongs to the second `/25` subnet.

The second subnet contains:

| Property | Value |
|---|---|
| Network Address | `10.0.2.128/25` |
| First Usable Host | `10.0.2.129` |
| Last Usable Host | `10.0.2.254` |
| Broadcast Address | `10.0.2.255` |
| Usable Hosts | `126` |

### /24 and /25 Comparison

| Property | /24 | /25 |
|---|---|---|
| Subnet Mask | `255.255.255.0` | `255.255.255.128` |
| Network Bits | 24 | 25 |
| Host Bits | 8 | 7 |
| Total Addresses per Subnet | 256 | 128 |
| Usable Hosts per Subnet | 254 | 126 |
| Number of /25 Subnets inside /24 | - | 2 |

### Subnet Structure

The original network:

```text
10.0.2.0/24
```

was divided into:

```text
10.0.2.0/24
│
├── 10.0.2.0/25
│   ├── Network:   10.0.2.0
│   ├── First:     10.0.2.1
│   ├── Last:      10.0.2.126
│   └── Broadcast: 10.0.2.127
│
└── 10.0.2.128/25
    ├── Network:   10.0.2.128
    ├── First:     10.0.2.129
    ├── Last:      10.0.2.254
    └── Broadcast: 10.0.2.255
```

### Lab Conclusion

In this lab, I practiced IPv4 subnetting by dividing the
`10.0.2.0/24` network into two `/25` subnets.

I learned that increasing the CIDR prefix from `/24` to `/25` borrows one
bit from the host portion. This creates two smaller subnets, with each
subnet supporting 126 usable host addresses.

Using `ipcalc`, I verified the network address, usable host range,
broadcast address, subnet mask, and number of usable hosts for both
subnets.

Understanding subnetting is important in cybersecurity and networking
because it supports network segmentation, firewall rule design, access
control, network reconnaissance, and efficient IP address management.


---

## Lab 04 - MAC Addresses and ARP

### Objective

The objective of this lab is to understand the relationship between
IPv4 addresses and MAC addresses on a local network and to examine how
Linux maintains neighbor information.

This practical exercise uses the Linux neighbor table and network
connectivity tests to identify and verify an IPv4-to-MAC address mapping.

### MAC Addresses

A MAC (Media Access Control) address is a Layer 2 address associated with
a network interface.

MAC addresses are used for communication between devices on a local
Ethernet network.

An example MAC address identified during this lab is:

```text
52:54:00:12:35:00
```

MAC addressing operates at the **Data Link Layer (Layer 2)** of the OSI
model.

IPv4 addressing operates at the **Network Layer (Layer 3)**.

### ARP

ARP stands for **Address Resolution Protocol**.

ARP is used with IPv4 on local networks to resolve an IPv4 address to
the corresponding MAC address required for Ethernet communication.

Conceptually:

```text
IPv4 Address
     │
     │ ARP Resolution
     ▼
MAC Address
```

For example, this lab identified the following mapping:

```text
10.0.2.2
    │
    ▼
52:54:00:12:35:00
```

### Examine the Neighbor Table

The following command was used to examine the Linux neighbor table:

```bash
ip neigh
```

### Result

```text
10.0.2.2 dev eth0 lladdr 52:54:00:12:35:00 REACHABLE
fe80::2 dev eth0 lladdr 52:54:00:12:35:00 router STALE
fd17:625c:f037:2::3 dev eth0 lladdr 52:54:00:12:35:00 router STALE
fd17:625c:f037:2::2 dev eth0 lladdr 52:54:00:12:35:00 router STALE
```

### IPv4 Neighbor Entry

The important IPv4 entry identified during this lab was:

```text
10.0.2.2 dev eth0 lladdr 52:54:00:12:35:00 REACHABLE
```

The information can be interpreted as follows:

| Field | Value | Meaning |
|---|---|---|
| IPv4 Address | `10.0.2.2` | Layer 3 address of the neighbor |
| Interface | `eth0` | Interface used to reach the neighbor |
| MAC Address | `52:54:00:12:35:00` | Layer 2 address associated with the neighbor |
| State | `REACHABLE` | The neighbor has recently been confirmed as reachable |

The `lladdr` field means **link-layer address**. In this Ethernet
environment, it represents the MAC address.

### Test Connectivity

To verify connectivity with the IPv4 neighbor, the following command
was used:

```bash
ping -c 3 10.0.2.2
```

### Result

```text
PING 10.0.2.2 (10.0.2.2) 56(84) bytes of data.
64 bytes from 10.0.2.2: icmp_seq=1 ttl=64 time=0.234 ms
64 bytes from 10.0.2.2: icmp_seq=2 ttl=64 time=0.289 ms
64 bytes from 10.0.2.2: icmp_seq=3 ttl=64 time=0.378 ms

--- 10.0.2.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss
rtt min/avg/max/mdev = 0.234/0.300/0.378/0.059 ms
```

### Ping Analysis

The ping test successfully received responses from `10.0.2.2`.

The results showed:

```text
Packets Transmitted: 3
Packets Received:    3
Packet Loss:         0%
Average RTT:         0.300 ms
```

This confirmed that the IPv4 neighbor was reachable from the Kali Linux
system.

### Verify the IPv4-to-MAC Mapping

After generating network communication, the following command was used
to examine the specific neighbor entry:

```bash
ip neigh show 10.0.2.2
```

### Result

```text
10.0.2.2 dev eth0 lladdr 52:54:00:12:35:00 REACHABLE
```

This verified the relationship:

```text
Layer 3
IPv4 Address
10.0.2.2
     │
     │ IPv4 Neighbor / ARP Resolution
     ▼
Layer 2
MAC Address
52:54:00:12:35:00
```

The `REACHABLE` state indicates that the Linux networking stack has
recently confirmed that this neighbor is reachable.

### Layer 2 and Layer 3 Relationship

This practical exercise demonstrates how Layer 2 and Layer 3 work
together.

```text
Layer 3 - IPv4 Address
        10.0.2.2
            │
            ▼
     ARP Resolution
            │
            ▼
Layer 2 - MAC Address
   52:54:00:12:35:00
```

IPv4 addresses provide logical addressing, while MAC addresses are used
for local Ethernet frame delivery.

When communicating with an IPv4 destination on the local subnet, the
system can use ARP to determine the MAC address associated with the
destination IPv4 address.

### Cybersecurity Relevance

Understanding ARP and MAC addressing is important in cybersecurity
because these concepts are involved in:

- Network traffic analysis
- Local network troubleshooting
- Device identification
- Packet analysis
- Network monitoring
- ARP spoofing detection
- Man-in-the-middle attack analysis
- Incident investigation

Security analysts should understand normal IPv4-to-MAC resolution before
investigating suspicious changes in local network mappings.

### Lab Conclusion

In this lab, I studied the relationship between IPv4 addresses and MAC
addresses on a local network.

Using `ip neigh`, I identified an IPv4 neighbor at `10.0.2.2` associated
with the MAC address `52:54:00:12:35:00`.

I then used `ping` to verify network connectivity and confirmed that all
three ICMP echo requests received replies with 0% packet loss.

Finally, I used `ip neigh show 10.0.2.2` to verify the neighbor entry and
observed its `REACHABLE` state.

This practical exercise demonstrated how Layer 3 IPv4 addressing and
Layer 2 MAC addressing work together during local network communication.

---

## Lab 05 - TCP vs UDP

### Objective

The objective of this lab is to understand the differences between TCP
and UDP and examine TCP and UDP sockets on a Kali Linux system.

This practical exercise uses the `ss` command to identify active TCP
connections, TCP listening sockets, UDP sockets, and UDP listening
sockets.

### TCP

TCP stands for **Transmission Control Protocol**.

TCP is a connection-oriented transport-layer protocol. It establishes a
connection between communicating endpoints before application data is
exchanged.

Important characteristics of TCP include:

- Connection-oriented communication
- Reliable data delivery
- Sequencing of data
- Error detection and recovery
- Retransmission of lost data
- Flow and congestion control

Common protocols that normally use TCP include:

```text
HTTP    - TCP 80
HTTPS   - TCP 443
SSH     - TCP 22
FTP     - TCP 21
SMTP    - TCP 25
```

### UDP

UDP stands for **User Datagram Protocol**.

UDP is a connectionless transport-layer protocol. It sends datagrams
without establishing a TCP-style connection and does not itself provide
TCP's delivery guarantees, retransmission, or ordered byte stream.

Important characteristics of UDP include:

- Connectionless communication
- Low protocol overhead
- No built-in retransmission of lost datagrams
- No guarantee of delivery
- No guarantee of packet ordering

Applications can implement additional reliability mechanisms themselves
when required.

Protocols and applications that commonly use UDP include:

```text
DNS     - UDP 53 for many standard queries
DHCP    - UDP 67 and 68
NTP     - UDP 123
```

### TCP and UDP Comparison

| Feature | TCP | UDP |
|---|---|---|
| Communication Type | Connection-oriented | Connectionless |
| Reliability | Provides reliable delivery mechanisms | No built-in delivery guarantee |
| Ordering | Maintains ordered byte stream | No built-in ordering guarantee |
| Retransmission | Supported | Not provided by UDP |
| Overhead | Higher | Lower |
| Typical Uses | HTTPS, SSH, web applications | DHCP, DNS queries, NTP |

Both TCP and UDP operate at the **Transport Layer (Layer 4)** of the OSI
model.

---

### Practical 1 - Examine Active TCP Connections

The following command was used to display TCP sockets:

```bash
ss -t
```

### Result

```text
State  Recv-Q  Send-Q   Local Address:Port     Peer Address:Port
ESTAB  0       0            10.0.2.15:44872     18.97.36.49:https
ESTAB  0       0            10.0.2.15:39382   109.176.239.0:https
ESTAB  0       0            10.0.2.15:34024   34.107.243.93:https
```

### Analysis

Three established TCP connections were visible.

The `ESTAB` state means that a TCP connection is currently established.

For example:

```text
10.0.2.15:44872  →  18.97.36.49:https
```

In this connection:

- `10.0.2.15` is the local Kali Linux IPv4 address.
- `44872` is the local TCP port used by this connection.
- `18.97.36.49` is the remote IPv4 address.
- `https` represents the HTTPS service, normally TCP port 443.
- `ESTAB` indicates an established TCP connection.

This demonstrates the connection-oriented nature of TCP.

---

### Practical 2 - Examine TCP Listening Sockets

The following command was used:

```bash
ss -lt
```

### Result

```text
State  Recv-Q  Send-Q   Local Address:Port     Peer Address:Port
```

No TCP listening sockets were displayed at the time the command was
executed.

This is different from the previous `ss -t` output. The previous command
showed established TCP connections, while `ss -lt` specifically searched
for TCP sockets in the listening state.

---

### Practical 3 - Examine UDP Sockets

The following command was used to display UDP sockets:

```bash
ss -u
```

### Result

```text
Recv-Q  Send-Q      Local Address:Port       Peer Address:Port
0       0          10.0.2.15%eth0:bootpc         10.0.2.2:bootps
```

### Analysis

A UDP socket associated with DHCP communication was identified.

```text
10.0.2.15%eth0:bootpc  →  10.0.2.2:bootps
```

The service names represent:

```text
bootpc = BOOTP/DHCP Client - UDP Port 68
bootps = BOOTP/DHCP Server - UDP Port 67
```

Therefore, this output provides a practical example of a network service
using UDP.

The `%eth0` portion indicates that the local address is associated with
the `eth0` network interface.

---

### Practical 4 - Examine UDP Listening Sockets

The following command was used:

```bash
ss -lu
```

### Result

```text
State  Recv-Q  Send-Q   Local Address:Port     Peer Address:Port
```

No UDP listening/unconnected sockets were displayed by this command at
the time it was executed.

Socket information can change over time as applications and network
services start, stop, establish communication, or terminate sessions.

---

### Practical TCP and UDP Comparison

The practical results demonstrated an important difference between the
two transport protocols.

TCP connections displayed a connection state:

```text
ESTAB
```

This reflects TCP's connection-oriented design.

The UDP output did not display an `ESTAB` TCP connection state. UDP does
not establish connections using the TCP handshake and state model.

The observed UDP socket was associated with DHCP communication:

```text
Client: 10.0.2.15:68
Server: 10.0.2.2:67
```

### Cybersecurity Relevance

Understanding TCP and UDP is important in cybersecurity because network
services expose transport-layer ports that security analysts frequently
inspect.

Knowledge of TCP and UDP is useful for:

- Network reconnaissance
- Port scanning
- Firewall configuration
- Packet analysis
- Intrusion detection
- Network troubleshooting
- Vulnerability assessment
- Incident investigation

For example, when analyzing network traffic, a security analyst should
understand whether a service uses TCP or UDP and how normal communication
for that protocol should appear.

### Lab Conclusion

In this lab, I studied the differences between TCP and UDP and examined
their behavior on a Kali Linux system.

Using `ss -t`, I identified three established TCP connections. Using
`ss -lt`, I observed that no TCP listening sockets were displayed at the
time of testing.

Using `ss -u`, I identified UDP communication associated with DHCP
between the Kali Linux system and another network endpoint. The local
DHCP client used UDP port 68 while the DHCP server endpoint used UDP
port 67.

Finally, `ss -lu` was used to examine UDP listening/unconnected sockets,
and no entries were displayed at that time.

This practical exercise provided a foundation for understanding
transport-layer protocols, ports, network services, firewall rules,
packet analysis, and network reconnaissance.


---

## Lab 06 - Common Ports and Protocols

### Objective

The objective of this lab is to identify common network services and
understand the TCP or UDP ports associated with them.

Knowing common ports and protocols is important for network
administration, traffic analysis, firewall configuration, vulnerability
assessment, and cybersecurity investigations.

### Understanding Network Ports

Transport-layer protocols such as TCP and UDP use port numbers to
identify network services and application endpoints.

A port number should normally be considered together with its transport
protocol.

For example:

```text
22/TCP
53/TCP
53/UDP
80/TCP
443/TCP
```

TCP port 53 and UDP port 53 use the same numerical port number but are
different transport-layer endpoints.

Port numbers range from:

```text
0 - 65535
```

They are commonly grouped into:

| Range | Category |
|---|---|
| 0 - 1023 | Well-Known Ports |
| 1024 - 49151 | Registered Ports |
| 49152 - 65535 | Dynamic/Private Ports |

---

### Practical 1 - Examine Common Network Services

Kali Linux contains the `/etc/services` file, which provides mappings
between service names and port/protocol combinations.

The following command was used to examine SSH, DNS, HTTP, and HTTPS
entries:

```bash
grep -E '^(ssh|http|https|domain)[[:space:]]' /etc/services
```

### Result

```text
ssh             22/tcp                          # SSH Remote Login Protocol
domain          53/tcp                          # Domain Name Server
domain          53/udp
http            80/tcp          www             # WorldWideWeb HTTP
https           443/tcp                         # http protocol over TLS/SSL
https           443/udp                         # HTTP/3
```

### Analysis

The output identified several important network services.

| Service | Port/Protocol | Purpose |
|---|---|---|
| SSH | `22/TCP` | Secure remote login and administration |
| DNS | `53/TCP` | DNS communication over TCP |
| DNS | `53/UDP` | DNS communication over UDP |
| HTTP | `80/TCP` | Standard web communication |
| HTTPS | `443/TCP` | HTTP communication protected using TLS |
| HTTPS / HTTP/3 entry | `443/UDP` | HTTP/3 communication |

An important observation is that a service may use more than one
transport protocol.

DNS entries were available for both:

```text
53/TCP
53/UDP
```

The system service database also contained HTTPS-related entries for:

```text
443/TCP
443/UDP
```

The UDP 443 entry was identified as HTTP/3 in the local service
database.

---

### Practical 2 - Examine FTP and Email-Related Services

The following command was used:

```bash
grep -E '^(ftp|smtp|pop3|imap)[[:space:]]' /etc/services
```

### Result

```text
ftp             21/tcp
smtp            25/tcp          mail
pop3            110/tcp         pop-3           # POP version 3
```

### Analysis

The following service mappings were identified:

| Service | Port/Protocol | Purpose |
|---|---|---|
| FTP | `21/TCP` | File Transfer Protocol control connection |
| SMTP | `25/TCP` | Email transfer |
| POP3 | `110/TCP` | Email retrieval |

No entry matching the exact `imap` pattern was displayed by this command
on the tested Kali Linux system.

The practical documentation therefore records only the entries that were
actually observed.

---

### Practical 3 - Examine Additional Mail Service Ports

The following command was used to search for additional mail-related
service entries:

```bash
grep -Ei '^(imap|imaps|pop3s|submission)[[:space:]]' /etc/services
```

### Result

```text
submission      587/tcp                         # Submission [RFC4409]
imaps           993/tcp                         # IMAP over SSL
pop3s           995/tcp                         # POP-3 over SSL
```

### Analysis

Three additional TCP services were identified:

| Service | Port/Protocol | Purpose |
|---|---|---|
| Submission | `587/TCP` | Email message submission |
| IMAPS | `993/TCP` | Encrypted IMAP service |
| POP3S | `995/TCP` | Encrypted POP3 service |

These results demonstrate that related application services may use
different ports depending on their purpose and security configuration.

---

### Ports Identified During the Lab

The following port and protocol mappings were directly identified from
the Kali Linux `/etc/services` file during this practical exercise:

```text
21/TCP   - FTP
22/TCP   - SSH
25/TCP   - SMTP
53/TCP   - DNS
53/UDP   - DNS
80/TCP   - HTTP
110/TCP  - POP3
443/TCP  - HTTPS
443/UDP  - HTTP/3
587/TCP  - Submission
993/TCP  - IMAPS
995/TCP  - POP3S
```

### Port Numbers and Services

A port number does not prove that a particular service is currently
running on a system.

The `/etc/services` file provides standard service-name mappings.

For example:

```text
ssh 22/tcp
```

indicates that SSH is conventionally associated with TCP port 22.

It does not mean that an SSH server is currently listening on TCP port
22 on the Kali Linux machine.

Actual listening services can be investigated using tools such as:

```bash
ss
```

or, in authorized environments, network reconnaissance tools such as
Nmap.

---

### Cybersecurity Relevance

Understanding common ports and protocols is important because security
analysts frequently use port information when examining network
activity.

Common examples include:

```text
21/TCP   FTP
22/TCP   SSH
25/TCP   SMTP
53/TCP   DNS
53/UDP   DNS
80/TCP   HTTP
443/TCP  HTTPS
```

This knowledge supports:

- Network reconnaissance
- Firewall rule analysis
- Packet analysis
- Vulnerability assessment
- Service identification
- Intrusion detection
- Incident response
- Network troubleshooting

For example, identifying TCP port 22 during an authorized network
assessment may indicate that an SSH-compatible service should be
investigated further.

However, the port number alone should not be treated as definitive proof
of the application running behind it. Service identification and
additional evidence may be required.

### Lab Conclusion

In this lab, I examined common network ports and protocols using the
Kali Linux `/etc/services` database.

I identified service mappings for SSH, FTP, SMTP, DNS, HTTP, HTTPS,
POP3, email submission, IMAPS, and POP3S.

The practical exercise also demonstrated that some application
protocols can operate using both TCP and UDP. DNS entries were identified
for both TCP and UDP port 53, while the local service database contained
HTTPS-related mappings for TCP and UDP port 443.

This lab improved my understanding of the relationship between
application protocols, transport protocols, and port numbers, providing
a foundation for later work involving Nmap, Wireshark, firewall
analysis, vulnerability assessment, and network security monitoring.


---

## Lab 07 - DNS Fundamentals

### Objective

The objective of this lab is to understand the basic operation of the
Domain Name System (DNS), identify the DNS resolvers configured on a
Kali Linux system, and perform DNS queries for IPv4 and IPv6 records.

The practical exercises use `nslookup` and `dig` to examine DNS name
resolution.

### What is DNS?

DNS stands for **Domain Name System**.

DNS provides a distributed naming system that allows domain names to be
resolved to information such as IP addresses.

For example:

```text
Domain Name
example.com
     │
     │ DNS Resolution
     ▼
IP Address
```

Without DNS, users would frequently need to identify services using IP
addresses instead of human-readable domain names.

DNS commonly uses port:

```text
53/UDP
53/TCP
```

The transport protocol used depends on the DNS operation and
circumstances.

---

### Common DNS Record Types

Some important DNS record types include:

| Record | Purpose |
|---|---|
| A | Maps a hostname to an IPv4 address |
| AAAA | Maps a hostname to an IPv6 address |
| CNAME | Creates an alias to another canonical hostname |
| MX | Identifies mail servers for a domain |
| NS | Identifies authoritative name servers |
| TXT | Stores text information associated with a domain |

This lab focuses primarily on `A` and `AAAA` records.

---

### Practical 1 - Examine DNS Resolver Configuration

The following command was used to examine the DNS resolver configuration
of the Kali Linux system:

```bash
cat /etc/resolv.conf
```

### Result

```text
# Generated by NetworkManager
nameserver 192.168.1.1
nameserver fd17:625c:f037:2::3
```

### Analysis

The system had two DNS resolver addresses configured:

```text
IPv4 DNS Resolver:
192.168.1.1

IPv6 DNS Resolver:
fd17:625c:f037:2::3
```

The comment:

```text
# Generated by NetworkManager
```

indicates that the resolver configuration was generated or managed by
NetworkManager.

The `nameserver` entries identify DNS resolvers that the system can use
for name resolution.

---

### Practical 2 - Resolve a Domain Name with nslookup

The following command was used:

```bash
nslookup example.com
```

`example.com` was used as a public domain suitable for documentation and
testing.

### Result

```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   example.com
Address: 172.66.147.243
Name:   example.com
Address: 104.20.23.154
Name:   example.com
Address: 2606:4700:10::ac42:93f3
Name:   example.com
Address: 2606:4700:10::6814:179a
```

### Analysis

The DNS query was sent through:

```text
DNS Resolver: 192.168.1.1
Port:         53
```

The query returned both IPv4 and IPv6 addresses.

IPv4 addresses observed:

```text
172.66.147.243
104.20.23.154
```

IPv6 addresses observed:

```text
2606:4700:10::ac42:93f3
2606:4700:10::6814:179a
```

This demonstrates that a single domain name can resolve to multiple IP
addresses.

The output also contained:

```text
Non-authoritative answer
```

This indicates that the answer was returned through the queried resolver
rather than being presented as a direct authoritative response from the
domain's authoritative name server.

---

### Practical 3 - Query an A Record with dig

An `A` record maps a hostname to an IPv4 address.

The following command was used:

```bash
dig example.com A
```

### Result

```text
; <<>> DiG 9.20.26-1-Debian <<>> example.com A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8056
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; QUESTION SECTION:
;example.com.                   IN      A

;; ANSWER SECTION:
example.com.            123     IN      A       104.20.23.154
example.com.            123     IN      A       172.66.147.243

;; Query time: 8 msec
;; SERVER: 192.168.1.1#53(192.168.1.1) (UDP)
;; MSG SIZE  rcvd: 100
```

### A Record Analysis

The DNS query completed successfully:

```text
Status: NOERROR
```

The question section showed:

```text
example.com. IN A
```

This means that an IPv4 `A` record was requested for `example.com`.

The answer section returned two IPv4 addresses:

```text
104.20.23.154
172.66.147.243
```

The observed TTL value was:

```text
123 seconds
```

TTL stands for **Time To Live**.

In a DNS response, TTL indicates how long the record may be cached before
it should be refreshed.

The output also showed:

```text
SERVER: 192.168.1.1#53(192.168.1.1) (UDP)
```

This confirms that this particular DNS query used the resolver
`192.168.1.1`, port `53`, over UDP.

The query completed in:

```text
8 msec
```

---

### Practical 4 - Query an AAAA Record with dig

An `AAAA` record maps a hostname to an IPv6 address.

The following command was used:

```bash
dig example.com AAAA
```

### Result

```text
; <<>> DiG 9.20.26-1-Debian <<>> example.com AAAA
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42802
;; flags: qr rd ra ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; QUESTION SECTION:
;example.com.                   IN      AAAA

;; ANSWER SECTION:
example.com.            183     IN      AAAA    2606:4700:10::ac42:93f3
example.com.            183     IN      AAAA    2606:4700:10::6814:179a

;; Query time: 11 msec
;; SERVER: 192.168.1.1#53(192.168.1.1) (UDP)
;; MSG SIZE  rcvd: 124
```

### AAAA Record Analysis

The query completed successfully:

```text
Status: NOERROR
```

The question section showed:

```text
example.com. IN AAAA
```

This means an IPv6 `AAAA` record was requested.

Two IPv6 addresses were returned:

```text
2606:4700:10::ac42:93f3
2606:4700:10::6814:179a
```

The observed TTL was:

```text
183 seconds
```

The DNS resolver was:

```text
192.168.1.1
```

and this particular query used:

```text
UDP port 53
```

The query time was:

```text
11 msec
```

---

### A Record vs AAAA Record

The practical exercises demonstrated the difference between two
important DNS record types:

```text
A Record
Domain Name ─────► IPv4 Address

AAAA Record
Domain Name ─────► IPv6 Address
```

For `example.com`, the lab observed:

```text
A Records:

104.20.23.154
172.66.147.243
```

and:

```text
AAAA Records:

2606:4700:10::ac42:93f3
2606:4700:10::6814:179a
```

DNS responses and TTL values can change over time, so future queries may
return different values.

---

### DNS Resolution Process

A simplified DNS resolution process can be represented as:

```text
User/Application
       │
       │ Requests example.com
       ▼
Operating System
       │
       ▼
Configured DNS Resolver
192.168.1.1
       │
       │ DNS Query
       ▼
DNS Infrastructure
       │
       ▼
DNS Response
       │
       ▼
IPv4 / IPv6 Address
```

The actual DNS infrastructure may involve caches, recursive resolvers,
root servers, top-level domain servers, and authoritative name servers.

---

### Cybersecurity Relevance

DNS knowledge is important in cybersecurity because DNS activity can
provide useful information during both defensive analysis and authorized
security assessments.

DNS analysis can support:

- Network troubleshooting
- Domain and hostname investigation
- Traffic analysis
- Incident response
- Detection of suspicious domain activity
- Malware investigation
- Network reconnaissance
- DNS security monitoring

Security analysts may examine DNS queries and responses to understand
which domains systems are attempting to contact.

Unexpected DNS requests can also provide indicators that require further
investigation.

---

### Lab Conclusion

In this lab, I studied the fundamentals of the Domain Name System and
performed practical DNS queries from Kali Linux.

I first examined `/etc/resolv.conf` and identified the IPv4 and IPv6 DNS
resolvers configured on the system.

Using `nslookup`, I resolved `example.com` and observed both IPv4 and
IPv6 addresses.

I then used `dig` to query the `A` and `AAAA` records separately. The
`A` query returned IPv4 addresses, while the `AAAA` query returned IPv6
addresses.

The `dig` output also demonstrated DNS concepts including query status,
answer sections, TTL values, resolver addresses, query times, and UDP
port 53.

This practical exercise provides a foundation for DNS traffic analysis,
network troubleshooting, reconnaissance, and cybersecurity monitoring.


---

## Lab 08 - DHCP Fundamentals

### Objective

The objective of this lab is to understand the fundamentals of DHCP and
examine how a Kali Linux system automatically receives IPv4 network
configuration.

The practical exercises use NetworkManager and `nmcli` to identify the
DHCP configuration, assigned IPv4 address, subnet mask, default gateway,
DNS server, DHCP server, and lease information.

### What is DHCP?

DHCP stands for **Dynamic Host Configuration Protocol**.

DHCP allows devices to automatically obtain network configuration rather
than requiring an administrator to manually configure every device.

DHCP can provide information such as:

- IPv4 address
- Subnet mask
- Default gateway
- DNS server
- Lease duration
- Other network configuration options

DHCP commonly uses UDP:

```text
UDP 67 - DHCP Server
UDP 68 - DHCP Client
```

---

### DHCP DORA Process

A common DHCP address allocation process is represented by the acronym
**DORA**:

```text
Client                         DHCP Server
  │                                 │
  │──── DHCP Discover ─────────────►│
  │                                 │
  │◄──── DHCP Offer ────────────────│
  │                                 │
  │──── DHCP Request ──────────────►│
  │                                 │
  │◄──── DHCP Acknowledgement ──────│
  │                                 │
```

The stages are:

1. **Discover** - The client searches for an available DHCP server.
2. **Offer** - A DHCP server offers network configuration to the client.
3. **Request** - The client requests the offered configuration.
4. **Acknowledgement** - The server acknowledges the lease and provides
   the configuration.

This represents the normal initial DHCP lease process conceptually.

---

### Practical 1 - Examine the Current Network Configuration

The following command was used:

```bash
nmcli device show eth0
```

### Observed Configuration

Important information identified from the output included:

```text
GENERAL.DEVICE:     eth0
GENERAL.TYPE:       ethernet
GENERAL.HWADDR:     08:00:27:5A:87:BC
GENERAL.STATE:      100 (connected)

IP4.ADDRESS[1]:     10.0.2.15/24
IP4.GATEWAY:        10.0.2.2
IP4.DNS[1]:         192.168.1.1

IP6.GATEWAY:        fe80::2
IP6.DNS[1]:         fd17:625c:f037:2::3
```

### Analysis

The `eth0` Ethernet interface was connected and had the following IPv4
configuration:

| Property | Value |
|---|---|
| Interface | `eth0` |
| MAC Address | `08:00:27:5A:87:BC` |
| IPv4 Address | `10.0.2.15/24` |
| Default Gateway | `10.0.2.2` |
| IPv4 DNS Server | `192.168.1.1` |

At this stage, the command showed the active network configuration.

However, these values alone do not prove that the configuration was
obtained through DHCP. Therefore, the NetworkManager connection method
was examined next.

---

### Practical 2 - Verify Automatic IPv4 Configuration

The following command was used:

```bash
nmcli connection show "Wired connection 1" | grep -E '^ipv4.method|^ipv4.addresses|^ipv4.gateway|^ipv4.dns'
```

### Result

```text
ipv4.method:                            auto
ipv4.dns:                               --
ipv4.dns-search:                        --
ipv4.dns-options:                       --
ipv4.dns-priority:                      0
ipv4.addresses:                         --
ipv4.gateway:                           --
```

### Analysis

The most important value was:

```text
ipv4.method: auto
```

This indicates that the NetworkManager connection profile is configured
to obtain IPv4 network configuration automatically.

The following values were not manually configured in the connection
profile:

```text
ipv4.addresses: --
ipv4.gateway:   --
ipv4.dns:       --
```

This supports the observation that the active IPv4 configuration was
being obtained automatically rather than being manually entered into the
connection profile.

---

### Practical 3 - Examine DHCP Options

The following command was first used to display DHCP information:

```bash
nmcli -f DHCP4 device show eth0
```

Some values were truncated by the terminal display.

To obtain a clearer multiline output, the following command was used:

```bash
nmcli --mode multiline --fields DHCP4 device show eth0
```

### Result

```text
DHCP4.OPTION[1]:  dhcp_client_identifier = 01:08:00:27:5a:87:bc
DHCP4.OPTION[2]:  dhcp_lease_time = 86400
DHCP4.OPTION[3]:  dhcp_server_identifier = 10.0.2.2
DHCP4.OPTION[4]:  domain_name_servers = 192.168.1.1
DHCP4.OPTION[5]:  expiry = 1790137940
DHCP4.OPTION[6]:  ip_address = 10.0.2.15
DHCP4.OPTION[7]:  next_server = 10.0.2.2
DHCP4.OPTION[8]:  requested_broadcast_address = 1
DHCP4.OPTION[9]:  requested_domain_name = 1
DHCP4.OPTION[10]: requested_domain_name_servers = 1
DHCP4.OPTION[11]: requested_domain_search = 1
DHCP4.OPTION[12]: requested_host_name = 1
DHCP4.OPTION[13]: requested_interface_mtu = 1
DHCP4.OPTION[14]: requested_ms_classless_static_routes = 1
DHCP4.OPTION[15]: requested_nis_domain = 1
DHCP4.OPTION[16]: requested_nis_servers = 1
DHCP4.OPTION[17]: requested_ntp_servers = 1
DHCP4.OPTION[18]: requested_rfc3442_classless_static_routes = 1
DHCP4.OPTION[19]: requested_root_path = 1
DHCP4.OPTION[20]: requested_routers = 1
DHCP4.OPTION[21]: requested_static_routes = 1
DHCP4.OPTION[22]: requested_subnet_mask = 1
DHCP4.OPTION[23]: requested_time_offset = 1
DHCP4.OPTION[24]: requested_wpad = 1
DHCP4.OPTION[25]: routers = 10.0.2.2
DHCP4.OPTION[26]: subnet_mask = 255.255.255.0
```

---

### DHCP Configuration Analysis

The DHCP options provided direct evidence of the network configuration
received by the Kali Linux system.

The important values were:

| DHCP Property | Value |
|---|---|
| DHCP Client Identifier | `01:08:00:27:5a:87:bc` |
| DHCP Server Identifier | `10.0.2.2` |
| Assigned IPv4 Address | `10.0.2.15` |
| Subnet Mask | `255.255.255.0` |
| Router | `10.0.2.2` |
| DNS Server | `192.168.1.1` |
| Lease Time | `86400` seconds |

The DHCP server was identified as:

```text
10.0.2.2
```

The IPv4 address provided to the Kali system was:

```text
10.0.2.15
```

The subnet mask was:

```text
255.255.255.0
```

which corresponds to:

```text
/24
```

The router/default gateway provided was:

```text
10.0.2.2
```

The DNS server provided through DHCP was:

```text
192.168.1.1
```

---

### Understanding the DHCP Lease

The DHCP lease time was:

```text
86400 seconds
```

Converting this value:

```text
86400 / 60 = 1440 minutes

1440 / 60 = 24 hours
```

Therefore, the DHCP lease duration observed during this lab was:

```text
24 hours
```

A DHCP lease allows the client to use the assigned network configuration
for a defined period. DHCP clients normally attempt to renew their
leases automatically before they expire.

---

### DHCP Client Identifier

The DHCP client identifier observed was:

```text
01:08:00:27:5a:87:bc
```

The Ethernet MAC address of the Kali interface was:

```text
08:00:27:5A:87:BC
```

The DHCP client identifier contains the interface's MAC address together
with an identifier prefix used by the DHCP client.

This helps the DHCP infrastructure distinguish clients when managing
leases.

---

### DHCP Information Observed in the Lab

The complete IPv4 configuration identified during the practical
exercise can be summarized as:

```text
                 DHCP Server
                  10.0.2.2
                     │
                     │ DHCP Configuration
                     ▼
               Kali Linux eth0
          MAC: 08:00:27:5A:87:BC
                     │
       ┌─────────────┼─────────────┐
       │             │             │
       ▼             ▼             ▼
IP Address       Gateway          DNS
10.0.2.15        10.0.2.2         192.168.1.1
       │
       ▼
Subnet Mask
255.255.255.0 (/24)

Lease Time: 86400 seconds (24 hours)
```

---

### DHCP and Static IPv4 Configuration

The practical results demonstrated an automatically configured IPv4
connection.

A DHCP-based configuration can automatically provide parameters such as:

```text
IP Address
Subnet Mask
Default Gateway
DNS Server
```

A static configuration requires these values to be manually configured
or otherwise explicitly assigned.

In this lab, NetworkManager showed:

```text
ipv4.method: auto
```

and the DHCP options provided the actual assigned network values.

---

### Cybersecurity Relevance

Understanding DHCP is important in cybersecurity because DHCP directly
affects how devices obtain network configuration.

Security professionals may examine DHCP information during:

- Network troubleshooting
- Asset identification
- Incident response
- Network monitoring
- Rogue DHCP server investigation
- Network access investigations
- Packet analysis
- Security auditing

A malicious or unauthorized DHCP server can potentially provide clients
with incorrect network parameters such as an unexpected gateway or DNS
resolver.

Therefore, understanding normal DHCP behavior helps security analysts
identify unusual network configuration changes.

---

### Lab Conclusion

In this lab, I studied DHCP fundamentals and examined the automatic IPv4
configuration of a Kali Linux system.

Using `nmcli device show eth0`, I identified the active IPv4 address,
gateway, DNS server, MAC address, and interface status.

I then verified that the NetworkManager connection profile used:

```text
ipv4.method: auto
```

Finally, I examined the DHCP options and identified the DHCP server,
assigned IPv4 address, subnet mask, router, DNS server, client
identifier, and lease duration.

The DHCP server was `10.0.2.2`, and the Kali Linux system received the
IPv4 address `10.0.2.15` with the subnet mask `255.255.255.0`. The
router was `10.0.2.2`, the DNS server was `192.168.1.1`, and the lease
duration was 86400 seconds, equivalent to 24 hours.

This practical exercise provided a foundation for understanding dynamic
network configuration, IP address management, network troubleshooting,
and DHCP-related security monitoring.


---

## Lab 09 - Routing and Default Gateway

### Objective

The objective of this lab is to understand IPv4 routing, directly
connected networks, default routes, and default gateways.

The practical exercises examine the Kali Linux routing table and compare
how the operating system selects routes for local and external
destinations.

### What is Routing?

Routing is the process of determining where network packets should be
sent in order to reach their destination.

A system uses a routing table containing information about reachable
networks and available gateways.

Linux can display the IPv4 routing table using:

```bash
ip route
```

A route can contain information such as:

- Destination network
- Gateway
- Network interface
- Source IP address
- Route source
- Metric

---

### What is a Default Gateway?

A default gateway is a router or next-hop device used when the routing
table does not contain a more specific route for a destination.

For example, the Kali Linux system in this lab belongs to:

```text
10.0.2.0/24
```

Its default gateway is:

```text
10.0.2.2
```

Therefore, traffic for destinations outside directly connected networks
can use the default route through `10.0.2.2`.

A simplified representation is:

```text
Kali Linux
10.0.2.15
    │
    │ eth0
    ▼
Default Gateway
10.0.2.2
    │
    ▼
Other Networks
```

---

### Practical 1 - Examine the IPv4 Routing Table

The following command was used:

```bash
ip route
```

### Result

```text
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 metric 100
```

### Analysis

The routing table contained two important routes.

The first route was:

```text
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
```

This is the default route.

Important fields include:

| Field | Value | Meaning |
|---|---|---|
| Destination | `default` | Used when no more-specific route matches |
| Gateway | `10.0.2.2` | Next-hop gateway |
| Interface | `eth0` | Interface used to send traffic |
| Route Protocol | `dhcp` | Route was obtained through DHCP configuration |
| Source Address | `10.0.2.15` | Source IPv4 address |
| Metric | `100` | Route preference value |

The keyword:

```text
via 10.0.2.2
```

identifies the next-hop gateway.

The keyword:

```text
dev eth0
```

identifies the network interface used by the route.

The value:

```text
proto dhcp
```

shows that the route was installed as part of the DHCP-provided
configuration.

---

### Directly Connected Network Route

The second route was:

```text
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 metric 100
```

This represents the directly connected IPv4 network:

```text
10.0.2.0/24
```

The Kali Linux system has:

```text
10.0.2.15/24
```

on `eth0`, so the operating system knows that the `10.0.2.0/24` network
is directly reachable through that interface.

The route does not contain a `via` gateway because destinations on this
directly connected subnet can be reached through the local link.

---

### Practical 2 - Examine Route Selection for an External Destination

The following command was used to ask the Linux routing system which
route it would select for `8.8.8.8`:

```bash
ip route get 8.8.8.8
```

### Result

```text
8.8.8.8 via 10.0.2.2 dev eth0 src 10.0.2.15 uid 1000
    cache
```

### Analysis

The route selected for the destination was:

```text
Destination: 8.8.8.8
Gateway:     10.0.2.2
Interface:   eth0
Source IP:   10.0.2.15
```

The important part is:

```text
via 10.0.2.2
```

The destination `8.8.8.8` is not part of the directly connected
`10.0.2.0/24` network.

Therefore, the routing system selected the default gateway:

```text
10.0.2.2
```

The packet would leave through:

```text
eth0
```

using the source IPv4 address:

```text
10.0.2.15
```

The `ip route get` command performs a route lookup. This exercise did not
require sending a ping or performing a network scan against the
destination.

---

### Practical 3 - Examine Route Selection for a Local Destination

The following command was used:

```bash
ip route get 10.0.2.2
```

### Result

```text
10.0.2.2 dev eth0 src 10.0.2.15 uid 1000
    cache
```

### Analysis

The route selected for the local destination was:

```text
Destination: 10.0.2.2
Interface:   eth0
Source IP:   10.0.2.15
```

An important difference is that the output does not contain:

```text
via <gateway>
```

This is because `10.0.2.2` belongs to the directly connected network:

```text
10.0.2.0/24
```

Therefore, the destination is reachable through the local `eth0`
interface without routing it through another next-hop gateway.

---

### Local vs External Route Selection

The practical results demonstrate the difference between local and
external route selection.

#### Local Destination

```text
Destination: 10.0.2.2

Kali Linux
10.0.2.15
    │
    │ eth0
    ▼
10.0.2.2
```

Selected route:

```text
10.0.2.2 dev eth0 src 10.0.2.15
```

No separate next-hop gateway is required because the destination belongs
to the directly connected subnet.

#### External Destination

```text
Destination: 8.8.8.8

Kali Linux
10.0.2.15
    │
    │ eth0
    ▼
Default Gateway
10.0.2.2
    │
    ▼
8.8.8.8
```

Selected route:

```text
8.8.8.8 via 10.0.2.2 dev eth0 src 10.0.2.15
```

The default gateway is selected because there is no more-specific route
for the external destination in the displayed routing table.

---

### Routing Decision Summary

The routing behavior observed during this lab can be summarized as:

```text
Destination Packet
       │
       ▼
Check Routing Table
       │
       ├── Destination matches 10.0.2.0/24
       │          │
       │          ▼
       │     Send through eth0
       │     using direct route
       │
       └── No more-specific route matches
                  │
                  ▼
            Use Default Route
                  │
                  ▼
             Gateway 10.0.2.2
                  │
                  ▼
                 eth0
```

Linux normally selects routes based on the most specific matching route.
If no more-specific route matches, an available default route can be
used.

---

### Relationship with DHCP

The routing table showed:

```text
proto dhcp
```

for the default route.

In the previous DHCP lab, the DHCP options identified:

```text
DHCP Server: 10.0.2.2
Router:      10.0.2.2
```

The current routing lab independently confirmed that the active default
route uses:

```text
default via 10.0.2.2
```

This demonstrates how DHCP-provided network configuration can influence
the system's routing table.

---

### Cybersecurity Relevance

Understanding routing and default gateways is important in cybersecurity
because network traffic depends on correct routing decisions.

Routing knowledge is useful for:

- Network troubleshooting
- Packet analysis
- Firewall analysis
- Network segmentation
- Incident response
- Network reconnaissance
- VPN troubleshooting
- Detecting unexpected gateway changes
- Understanding traffic paths

For example, an unexpected default gateway may require investigation
because changing the gateway can alter where network traffic is sent.

Security analysts should therefore understand the normal routing
configuration of systems they monitor.

---

### Lab Conclusion

In this lab, I examined IPv4 routing and the default gateway on a Kali
Linux system.

Using `ip route`, I identified the directly connected network
`10.0.2.0/24` and the default gateway `10.0.2.2`.

The routing table showed that the default route was obtained through
DHCP and used `eth0` with the source IPv4 address `10.0.2.15`.

Using `ip route get 8.8.8.8`, I verified that a destination outside the
directly connected subnet would use the default gateway `10.0.2.2`.

Using `ip route get 10.0.2.2`, I verified that a destination within the
directly connected network is reached directly through `eth0` without a
separate next-hop gateway.

This practical exercise improved my understanding of routing tables,
directly connected networks, default routes, gateways, and Linux route
selection.

---

## Lab 10 - Network Troubleshooting

### Objective

The objective of this lab is to perform a structured network
troubleshooting process on a Kali Linux system.

The lab verifies the network connection step by step, starting from the
local network interface and continuing through IPv4 configuration,
default gateway connectivity, external IP connectivity, DNS resolution,
and end-to-end domain connectivity.

A structured troubleshooting process helps identify the layer or
component responsible for a network connectivity problem.

---

### Network Troubleshooting Method

The following troubleshooting sequence was used:

```text
Network Interface
       │
       ▼
IPv4 Configuration
       │
       ▼
Default Gateway
       │
       ▼
External IP Connectivity
       │
       ▼
DNS Resolution
       │
       ▼
End-to-End Domain Connectivity
```

Testing the network in this order makes it easier to isolate problems.

For example, if an external IP address is reachable but a domain name
cannot be resolved, the problem may be related to DNS rather than the
underlying IP connection.

---

### Step 1 - Check the Network Interface

The first troubleshooting step was to verify that the `eth0` network
interface was operational.

The following command was used:

```bash
ip link show eth0
```

### Result

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:5a:87:bc brd ff:ff:ff:ff:ff:ff
```

### Analysis

The important values were:

```text
Interface:   eth0
Status:      UP
Link Status: LOWER_UP
State:       UP
MAC Address: 08:00:27:5a:87:bc
MTU:         1500
```

The `UP` flag indicates that the network interface is enabled.

The `LOWER_UP` flag indicates that the underlying network link is
operational.

The result therefore confirmed that the `eth0` interface was active and
available for network communication.

---

### Step 2 - Check the IPv4 Configuration

After confirming the interface status, the IPv4 configuration was
examined.

The following command was used:

```bash
ip -4 addr show eth0
```

### Result

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute eth0
       valid_lft 35232sec preferred_lft 35232sec
```

### Analysis

The IPv4 configuration was:

```text
IPv4 Address:      10.0.2.15
CIDR Prefix:       /24
Subnet Mask:       255.255.255.0
Broadcast Address: 10.0.2.255
Assignment:        Dynamic
```

The system therefore had a valid IPv4 address on `eth0`.

The `/24` prefix indicates that the system belongs to the network:

```text
10.0.2.0/24
```

The `dynamic` field indicates that the address was dynamically
configured.

---

### Step 3 - Test the Default Gateway

The default gateway identified in the previous routing lab was:

```text
10.0.2.2
```

The following command was used to test connectivity to the gateway:

```bash
ping -c 3 10.0.2.2
```

### Result

```text
PING 10.0.2.2 (10.0.2.2) 56(84) bytes of data.
64 bytes from 10.0.2.2: icmp_seq=1 ttl=64 time=0.338 ms
64 bytes from 10.0.2.2: icmp_seq=2 ttl=64 time=0.255 ms
64 bytes from 10.0.2.2: icmp_seq=3 ttl=64 time=0.406 ms

--- 10.0.2.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2055ms
rtt min/avg/max/mdev = 0.255/0.333/0.406/0.061 ms
```

### Analysis

The test produced:

```text
Packets Sent:     3
Packets Received: 3
Packet Loss:      0%
Average RTT:      0.333 ms
```

All three packets received responses.

This confirmed that the Kali Linux system could communicate successfully
with its default gateway.

At this stage, the local network path between the Kali system and the
gateway was operational.

---

### Step 4 - Test External IP Connectivity

The next step was to test connectivity to an external IP address without
depending on DNS name resolution.

The following command was used:

```bash
ping -c 3 8.8.8.8
```

### Result

```text
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=64 time=43.6 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=64 time=41.4 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=64 time=41.8 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2009ms
rtt min/avg/max/mdev = 41.402/42.249/43.583/0.954 ms
```

### Analysis

The external connectivity test produced:

```text
Destination:      8.8.8.8
Packets Sent:     3
Packets Received: 3
Packet Loss:      0%
Average RTT:      42.249 ms
```

The successful responses confirmed that external IP connectivity was
working during the test.

Because an IP address was used directly, this test did not depend on DNS
name resolution.

This distinction is useful during troubleshooting.

For example:

```text
External IP works + Domain name fails
                │
                ▼
        Investigate DNS
```

---

### Step 5 - Test DNS Resolution

After confirming external IP connectivity, DNS resolution was tested.

The following command was used:

```bash
nslookup example.com
```

### Result

```text
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   example.com
Address: 104.20.23.154
Name:   example.com
Address: 172.66.147.243
Name:   example.com
Address: 2606:4700:10::6814:179a
Name:   example.com
Address: 2606:4700:10::ac42:93f3
```

### Analysis

The configured DNS resolver used for the query was:

```text
192.168.1.1
```

The output showed that `example.com` was successfully resolved to both
IPv4 and IPv6 addresses.

IPv4 addresses included:

```text
104.20.23.154
172.66.147.243
```

IPv6 addresses included:

```text
2606:4700:10::6814:179a
2606:4700:10::ac42:93f3
```

The successful DNS response confirmed that name resolution was
operational during the test.

---

### Step 6 - Test End-to-End Domain Connectivity

The final test used a domain name rather than a direct IP address.

The following command was used:

```bash
ping -c 3 example.com
```

### Result

```text
PING example.com (172.66.147.243) 56(84) bytes of data.
64 bytes from 172.66.147.243: icmp_seq=1 ttl=64 time=11.0 ms
64 bytes from 172.66.147.243: icmp_seq=2 ttl=64 time=8.66 ms
64 bytes from 172.66.147.243: icmp_seq=3 ttl=64 time=10.9 ms

--- example.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 8.658/10.169/10.962/1.068 ms
```

### Analysis

The domain name was resolved to:

```text
172.66.147.243
```

The connectivity test then produced:

```text
Packets Sent:     3
Packets Received: 3
Packet Loss:      0%
Average RTT:      10.169 ms
```

This test demonstrated both successful DNS resolution and successful
ICMP communication with the resolved destination during the test.

---

### Troubleshooting Results

The completed troubleshooting process produced the following results:

| Test | Result |
|---|---|
| Network interface | Operational |
| IPv4 configuration | Configured |
| Default gateway | Reachable |
| External IP connectivity | Working |
| DNS resolution | Working |
| Domain connectivity | Working |

The complete troubleshooting path was therefore:

```text
eth0
 │
 │ UP / LOWER_UP
 ▼
10.0.2.15/24
 │
 ▼
Default Gateway
10.0.2.2
 │
 │ Reachable
 ▼
External IP
8.8.8.8
 │
 │ Reachable
 ▼
DNS Resolver
192.168.1.1
 │
 │ Resolution Successful
 ▼
example.com
 │
 ▼
172.66.147.243
 │
 │ Reachable
 ▼
Network Test Successful
```

---

### Troubleshooting Logic

A structured troubleshooting process can help identify where a network
problem occurs.

For example:

```text
1. Is the interface UP?
        │
        ├── No  → Investigate interface or link
        │
        └── Yes
             │
             ▼
2. Is an IPv4 address configured?
        │
        ├── No  → Investigate DHCP or IP configuration
        │
        └── Yes
             │
             ▼
3. Is the default gateway reachable?
        │
        ├── No  → Investigate local network/gateway
        │
        └── Yes
             │
             ▼
4. Is an external IP reachable?
        │
        ├── No  → Investigate routing/upstream connectivity
        │
        └── Yes
             │
             ▼
5. Does DNS resolution work?
        │
        ├── No  → Investigate DNS configuration
        │
        └── Yes
             │
             ▼
6. Test the required network service
```

This approach is more effective than randomly changing network settings
because each test isolates a different part of the communication path.

---

### Important Troubleshooting Commands

The commands used during this lab were:

```bash
ip link show eth0
ip -4 addr show eth0
ping -c 3 10.0.2.2
ping -c 3 8.8.8.8
nslookup example.com
ping -c 3 example.com
```

Other commands studied in previous networking labs can also support
troubleshooting, including:

```bash
ip route
ip route get <destination>
ip neigh
ss
dig
nmcli device show eth0
```

Together, these commands can help examine network interfaces, IP
addresses, routes, neighboring devices, sockets, DNS, and DHCP
configuration.

---

### Cybersecurity Relevance

Network troubleshooting is an important skill for cybersecurity
professionals.

Security analysts may need to determine whether a connectivity problem
is caused by:

- An inactive network interface
- Incorrect IP configuration
- DHCP problems
- Gateway problems
- Routing problems
- DNS problems
- Firewall filtering
- Network segmentation
- Service availability
- Upstream network failures

The same networking knowledge is also useful when analyzing packet
captures, investigating security incidents, validating firewall rules,
monitoring network infrastructure, and performing authorized security
assessments.

A structured troubleshooting process helps distinguish normal network
failures from configuration problems and potential security-related
issues.

---

### Lab Conclusion

In this lab, I performed a structured network troubleshooting process on
a Kali Linux system.

I first verified that the `eth0` network interface was operational and
confirmed that the system had the IPv4 address `10.0.2.15/24`.

I then tested the default gateway `10.0.2.2` and received responses with
0% packet loss.

Next, I tested an external IP address and confirmed that IP-level
external connectivity was working.

DNS resolution was tested using `nslookup example.com`, which
successfully returned IPv4 and IPv6 addresses.

Finally, I tested `example.com` directly and received responses from the
resolved IPv4 address with 0% packet loss.

These tests demonstrated a systematic method for diagnosing network
connectivity problems from the local interface through to external
network and DNS communication.

