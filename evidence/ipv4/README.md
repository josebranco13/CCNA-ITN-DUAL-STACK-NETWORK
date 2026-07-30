# IPv4 Evidence

This directory contains evidence showing that IPv4 addressing, routing and communication are working correctly.

## Evidence Files

| Evidence | Purpose |
|:---------|:--------|
| [PC IPv4 Configuration](pc-ipv4-config.png) | Shows the IPv4 address, subnet mask, default gateway and DNS server assigned to an Administration computer |
| [PC to DNS Server Ping](pc-to-dns-ipv4-ping.png) | Confirms IPv4 communication between the Administration network and the DNS server |
| [Headquarters to Branch Ping](headquarters-to-branch-ipv4-ping.png) | Confirms IPv4 communication between the headquarters and the remote branch |
| [Branch to Headquarters Ping](branch-to-headquarters-ipv4-ping.png) | Confirms IPv4 communication between the remote branch and the headquarters |
| [Router HQ Interface Summary](RHQ-ipv4-interface-summary.png) | Shows the IPv4 addresses and operational status of the headquarters router interfaces |
| [Router HQ Routing Table](RHQ-ipv4-routing-table.png) | Shows the directly connected and static IPv4 routes known by the headquarters router |
| [Router BR Interface Summary](RBR-ipv4-interface-summary.png) | Shows the IPv4 addresses and operational status of the headquarters router interfaces |
| [Router BR Routing Table](RBR-ipv4-routing-table.png) | Shows the directly connected and static IPv4 routes known by the headquarters router |

---

## Client IPv4 Configuration

The client configuration was checked using:

```text
ipconfig
```

The following information was verified:

- IPv4 address;
- subnet mask;
- default gateway;
- DNS server address.

A correct default gateway is necessary for the computer to communicate with devices located in other networks.

---

## Communication with the DNS Server

The DNS server uses the following IPv4 address:

```text
192.168.30.12
```

The connection was tested using:

```text
ping 192.168.30.12
```

A successful response confirms that:

1. the client has a valid IPv4 configuration;
2. the local switch connection is operational;
3. the local default gateway is reachable;
4. the router can forward traffic to the Server network;
5. the DNS server can return traffic to the client.

---

## Headquarters and Branch Communication

Communication between the headquarters and the remote branch was tested using `ping`.

A successful result confirms that:

- the router-to-router connection is operational;
- the static routes are correct;
- the branch gateway is correctly configured;
- traffic can travel in both directions.

---

## Router Interface Verification

Router interfaces were checked using:

```text
show ip interface brief
```

An operational interface should normally appear as:

```text
up/up
```

The first `up` represents the physical state of the interface.

The second `up` represents the operational state of the line protocol.

---

## IPv4 Routing Table

The IPv4 routing table was checked using:

```text
show ip route
```

The routing table shows the networks that the router knows how to reach.

The headquarters router should contain:

- directly connected headquarters networks;
- the router-to-router network;
- a static route towards the remote branch.

The complete verification process is available in:

[Network Verification](../../docs/verification.md)

[Return to Project Evidence](../README.md)