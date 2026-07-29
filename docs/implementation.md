# Network Implementation

## Overview

This document explains how the network was designed and configured in Cisco Packet Tracer.

The project represents a small company with a headquarters and a remote branch. The network was created to demonstrate the practical application of the concepts studied in the Cisco Networking Academy **Introduction to Networks (ITN)** course.

The network supports both IPv4 and IPv6, creating a dual-stack environment.

---

## Network Scenario

The company network is divided into the following areas:

- Administration;
- Engineering;
- Server Room;
- Remote Branch.

Each area uses its own local network.

The headquarters contains the Administration, Engineering and Server networks. The remote branch is connected to the headquarters through a second router.

---

## Devices Used

The following devices were added to the Packet Tracer topology:

| Device type | Quantity |
|:------------|---------:|
| Routers | 2 |
| Switches | 4 |
| Computers | 11 |
| Servers | 2 |
| Network printers | 2 |
| **Total devices** | **21** |

The main network devices are:

| Device | Purpose |
|:-------|:--------|
| `R1-HQ` | Connects the networks located at the headquarters |
| `R2-BR` | Connects the remote branch to the headquarters |
| `SW-ADM` | Connects the Administration devices |
| `SW-ENG` | Connects the Engineering devices |
| `SW-SRV` | Connects the servers |
| `SW-BR` | Connects the remote branch devices |

---

## Physical Connections

Computers, printers and servers were connected to their local switches.

Each switch was connected to the router responsible for its network.

The general structure is:

```text
Administration ── SW-ADM ──┐
                            │
Engineering ───── SW-ENG ───┼── R1-HQ ─── R2-BR ─── SW-BR ─── Remote Branch
                            │
Servers ───────── SW-SRV ───┘
```

Switches are responsible for connecting devices inside the same local network.

Routers are responsible for forwarding traffic between different networks.

---

## Basic Device Configuration

The routers and switches were given clear hostnames to make them easier to identify.

Router and switch interfaces were configured and enabled using:

```text
no shutdown
```

Descriptions were added to the main router interfaces to identify the connected network.

The configurations were saved after the implementation was completed.

---

## IPv4 Implementation

A different IPv4 network was assigned to each company area.

The router interface connected to each area was configured as the default gateway for that network.

The IPv4 configuration of a device includes:

- IPv4 address;
- subnet mask;
- default gateway;
- DNS server address.

Most computers receive their IPv4 configuration automatically through DHCP.

Servers and printers use static IPv4 addresses because their addresses should remain unchanged.

The complete IPv4 addressing plan is available in:

```text
addressing/ipv4-addressing.md
```

---

## IPv6 Implementation

IPv6 was configured together with IPv4, creating a dual-stack network.

Each area uses a different `/64` IPv6 prefix.

IPv6 forwarding was enabled on both routers using:

```text
ipv6 unicast-routing
```

Router interfaces and servers use static IPv6 addresses.

Computers use SLAAC, also called IPv6 automatic configuration, to automatically:

- generate a global IPv6 address;
- identify their network prefix;
- learn their default gateway.

The complete IPv6 addressing plan is available in:

```text
addressing/ipv6-addressing.md
```

---

## Routing

The headquarters router is directly connected to:

- the Administration network;
- the Engineering network;
- the Server network;
- the router-to-router network.

The branch router is directly connected to:

- the Remote Branch network;
- the router-to-router network.

Static routes were configured so that both routers know how to reach networks that are not directly connected.

Separate routes were configured for IPv4 and IPv6.

Without these routes, the headquarters and remote branch would not be able to communicate.

---

## DHCP Service

The DHCP service automatically provides IPv4 configuration to the client computers.

The DHCP configuration includes:

- an available IPv4 address;
- subnet mask;
- default gateway;
- DNS server address.

This avoids manually configuring every computer.

Servers and printers use static addresses because they must always be available at known addresses.

---

## DNS Service

DNS stands for **Domain Name System**.

The DNS server translates a readable name into an IP address.

In this project, users can access the internal website using:

```text
www.network.local
```

The DNS server contains:

- an `A` record for the IPv4 address;
- an `AAAA` record for the IPv6 address.

The configured DNS server addresses are:

```text
IPv4: 192.168.20.12
IPv6: 2001:DB8:1:30::11
```

DNS only identifies the address of the server. It does not provide the webpage itself.

---

## HTTP Service

The HTTP service provides the internal webpage.

After DNS translates `www.network.local` into an IP address, the computer connects to the HTTP server and requests the webpage.

The website can be opened using:

```text
http://www.network.local
```

---

## Final Configuration

After completing the implementation:

- all required devices were connected;
- router interfaces were enabled;
- IPv4 addresses were configured;
- IPv6 addresses were configured;
- static routes were added;
- DHCP was activated;
- DNS records were created;
- the HTTP service was activated;
- connectivity tests were performed;
- router and switch configurations were saved.

The final Packet Tracer project is available in:

```text
packet-tracer/ccna-itn-dual-stack-network.pkt
```