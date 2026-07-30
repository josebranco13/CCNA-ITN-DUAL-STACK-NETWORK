# IPv6 Evidence

This directory contains evidence showing that IPv6 addressing, routing and communication are working correctly.

## Evidence Files

| Evidence | Purpose |
|:---------|:--------|
| [PC IPv6 Configuration](pc-ipv6-config.png) | Shows the global IPv6 address, link-local address and default gateway of an Administration computer |
| [PC to DNS Server Ping](pc-to-dns-ipv6-ping.png) | Confirms IPv6 communication between the Administration network and the DNS server |
| [Headquarters to Branch Ping](headquarters-to-branch-ipv6-ping.png) | Confirms IPv6 communication between the headquarters and the remote branch |
| [Branch to Headquarters Ping](branch-to-headquarters-ipv6-ping.png) | Confirms IPv6 communication between the remote branch and the headquarters |
| [Router HQ IPv6 Interface Summary](RHQ-ipv6-interface-summary.png) | Shows the IPv6 addresses and operational status of the headquarters router interfaces |
| [Router HQ IPv6 Routing Table](RHQ-ipv6-routing-table.png) | Shows the connected and static IPv6 routes known by the headquarters router |
| [Router BR IPv6 Interface Summary](RBR-ipv6-interface-summary.png) | Shows the IPv6 addresses and operational status of the headquarters router interfaces |
| [Router BR IPv6 Routing Table](RBR-ipv6-routing-table.png) | Shows the connected and static IPv6 routes known by the headquarters router |

---

## Client IPv6 Configuration

Client computers use IPv6 automatic configuration, also known as SLAAC.

The routers send Router Advertisement messages containing the IPv6 prefix used by each local network.

Using this information, a computer can automatically obtain:

- a global IPv6 address;
- a `/64` network prefix;
- a link-local address;
- an IPv6 default gateway.

The configuration was checked using:

```text
ipconfig
```

---

## Communication with the DNS Server

The DNS server uses the following IPv6 address:

```text
2001:DB8:1:30::11
```

The connection was tested using:

```text
ping 2001:DB8:1:30::11
```

A successful response confirms that:

1. the client has a valid global IPv6 address;
2. the IPv6 default gateway is reachable;
3. IPv6 forwarding is enabled on the router;
4. the Server network uses the correct IPv6 prefix;
5. the DNS server has a valid address and default gateway.

---

## Headquarters and Branch Communication

IPv6 communication between the headquarters and the remote branch was also tested.

A successful result confirms that:

- both routers have IPv6 enabled;
- the router-to-router IPv6 connection is operational;
- the required IPv6 routes are present;
- both networks can return traffic to each other.

---

## Router Interface Verification

IPv6 router interfaces were checked using:

```text
show ipv6 interface brief
```

This command displays:

- the interface state;
- global IPv6 addresses;
- link-local IPv6 addresses.

The router interfaces should appear as operational.

---

## IPv6 Routing Table

The IPv6 routing table was checked using:

```text
show ipv6 route
```

The headquarters router should know:

- the directly connected Administration network;
- the directly connected Engineering network;
- the directly connected Server network;
- the router-to-router network;
- the route towards the remote branch.

The complete verification process is available in:

[Network Verification](../../docs/verification.md)

[Return to Project Evidence](../README.md)