# Network Verification

## Overview

This document explains how the network configuration was tested and verified.

The purpose of the verification process was to confirm that:

- devices could communicate inside the same local network;
- devices could communicate between different networks;
- the headquarters could communicate with the remote branch;
- IPv4 was working;
- IPv6 was working;
- DHCP was assigning IPv4 configurations;
- DNS was resolving the internal website name;
- the HTTP service was providing the internal webpage.

---

## Verification Method

The network was tested step by step.

The following order was used:

1. verify the local device configuration;
2. test the local default gateway;
3. test another network connected to the same router;
4. test the router-to-router connection;
5. test communication with the remote branch;
6. test DNS name resolution;
7. test the HTTP service.

This method makes it easier to identify the location of a problem.

---

## Connectivity Test Results

| Test | Source | Destination | Protocol | Expected result | Result |
|:-----|:-------|:------------|:---------|:----------------|:-------|
| Local gateway test | Administration PC | Administration gateway | IPv4 | Successful | Pass |
| Local gateway test | Administration PC | Administration gateway | IPv6 | Successful | Pass |
| Inter-network test | Administration PC | DNS Server | IPv4 | Successful | Pass |
| Inter-network test | Administration PC | DNS Server | IPv6 | Successful | Pass |
| Department communication | Engineering PC | Administration PC | IPv4 | Successful | Pass |
| Headquarters-to-branch test | Headquarters PC | Branch PC | IPv4 | Successful | Pass |
| Headquarters-to-branch test | Headquarters PC | Branch PC | IPv6 | Successful | Pass |
| Branch-to-server test | Branch PC | DNS Server | IPv4 | Successful | Pass |
| Branch-to-server test | Branch PC | DNS Server | IPv6 | Successful | Pass |
| DNS resolution | Client PC | `www.network.local` | DNS | Name resolved | Pass |
| Website access | Client PC | `www.network.local` | HTTP | Page displayed | Pass |

A `Pass` result means that the expected behaviour was successfully confirmed.

---

## IPv4 Verification

IPv4 connectivity was tested using the `ping` command.

Example:

```text
ping 192.168.20.12
```

This test confirms whether a client can reach the DNS server using IPv4.

The IPv4 configuration of the computers was checked using:

```text
ipconfig
```

The following information was verified:

- IPv4 address;
- subnet mask;
- default gateway;
- DNS server address.

---

## IPv6 Verification

IPv6 connectivity was tested using:

```text
ping 2001:DB8:1:30::11
```

This test confirms whether a client can reach the DNS server using IPv6.

The IPv6 configuration of the computers was checked to confirm that each device had:

- a global IPv6 address;
- a `/64` prefix;
- a link-local address;
- an IPv6 default gateway;
- the IPv6 address of the DNS server.

---

## Router Interface Verification

The IPv4 interfaces were checked using:

```text
show ip interface brief
```

The IPv6 interfaces were checked using:

```text
show ipv6 interface brief
```

An operational router interface should normally appear as:

```text
up/up
```

The first `up` means that the physical interface is active.

The second `up` means that the line protocol is operational.

---

## Routing Verification

The IPv4 routing tables were checked using:

```text
show ip route
```

The IPv6 routing tables were checked using:

```text
show ipv6 route
```

These commands were used to confirm that the routers knew:

- their directly connected networks;
- the route towards the remote branch;
- the routes towards the headquarters networks;
- the correct next-hop router.

---

## DHCP Verification

DHCP was selected on the client computers in:

```text
Desktop → IP Configuration
```

The clients were checked to confirm that they automatically received:

- an IPv4 address;
- the correct subnet mask;
- the correct default gateway;
- the correct DNS server address.

Successful automatic configuration confirmed that the DHCP service was working.

---

## DNS Verification

DNS was tested by using the internal website name instead of its IP address.

Example:

```text
ping www.network.local
```

A successful test means that the DNS server translated the name into an IP address.

The DNS server contains two types of records:

| Record | Purpose |
|:-------|:--------|
| `A` | Associates the name with an IPv4 address |
| `AAAA` | Associates the name with an IPv6 address |

The configured name is:

```text
www.network.local
```

---

## HTTP Verification

The HTTP service was tested using the Web Browser application available on the Packet Tracer computers.

The following address was entered:

```text
http://www.network.local
```

The test was successful when the internal webpage was displayed.

This single test confirms that:

1. the client can reach the DNS server;
2. DNS can translate the website name;
3. the client can reach the web server;
4. the HTTP service is active;
5. the server can send the webpage back to the client.

---

## Final Result

The final tests confirmed that:

- devices in the same area can communicate;
- different headquarters networks can communicate;
- the headquarters and remote branch can communicate;
- IPv4 connectivity is operational;
- IPv6 connectivity is operational;
- DHCP is assigning IPv4 configurations;
- DNS is resolving the internal name;
- the internal website can be accessed through HTTP.

All planned project requirements were successfully verified.