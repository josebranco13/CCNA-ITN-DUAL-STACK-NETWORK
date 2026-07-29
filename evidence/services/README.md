# Network Services Evidence

This directory contains evidence showing that the DHCP, DNS and HTTP services are working correctly.

## Evidence Files

| Evidence | Purpose |
|:---------|:--------|
| [DHCP Client Configuration](dhcp-client-configuration.png) | Shows a client computer receiving its IPv4 configuration automatically |
| [DNS A and AAAA Records](dns-a-and-aaaa-records.png) | Shows the IPv4 and IPv6 DNS records configured for the internal website |
| [DNS Name Resolution](dns-name-resolution.png) | Shows the internal website name being translated into an IP address |
| [HTTP Website Access](http-website-access.png) | Shows the internal webpage being opened through its DNS name |

---

## DHCP Service

DHCP automatically provides IPv4 configuration to client computers.

The DHCP service provides:

- an IPv4 address;
- a subnet mask;
- a default gateway;
- a DNS server address.

This avoids manually configuring every client computer.

Servers and printers use static addresses because their addresses should remain unchanged.

A successful DHCP test confirms that the client received an address from the correct network pool.

---

## DNS Service

DNS stands for **Domain Name System**.

DNS translates a readable name into an IP address.

The internal website uses the following name:

```text
www.network.local
```

The DNS server stores two records:

| Record type | Name | Address type |
|:------------|:-----|:-------------|
| `A` | `www.network.local` | IPv4 address |
| `AAAA` | `www.network.local` | IPv6 address |

The configured DNS server addresses are:

```text
IPv4: 192.168.20.12
IPv6: 2001:DB8:1:30::11
```

The `A` record allows the website name to be resolved through IPv4.

The `AAAA` record allows the same name to be resolved through IPv6.

---

## DNS Resolution Process

When a computer tries to access:

```text
www.network.local
```

the following process occurs:

1. the computer sends a request to the DNS server;
2. the DNS server searches for the requested name;
3. the DNS server returns the associated IPv4 or IPv6 address;
4. the computer uses the returned address to contact the web server.

DNS does not provide the webpage. It only helps the client discover the correct server address.

---

## HTTP Service

HTTP is responsible for providing the internal webpage.

The website was tested using:

```text
http://www.network.local
```

A successful website test confirms that:

1. the client has network connectivity;
2. the DNS server is reachable;
3. the name is resolved correctly;
4. the web server is reachable;
5. the HTTP service is active;
6. the webpage is returned to the client.

The complete service verification is available in:

[Network Verification](../../docs/verification.md)

[Return to Project Evidence](../README.md)