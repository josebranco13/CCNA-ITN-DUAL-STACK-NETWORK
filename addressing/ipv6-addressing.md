# IPv6 Addressing Plan

## Overview

IPv6 was configured together with IPv4, creating a dual-stack network.

A dual-stack network allows devices to communicate using either IPv4 or IPv6.

Each network area uses a different `/64` IPv6 prefix. The routers use static IPv6 addresses, while computers generate their addresses automatically through SLAAC.


## IPv6 Networks

| Area | IPv6 prefix | Router address |
|:-----|:------------|:---------------|
| Administration | `2001:DB8:1:10::/64` | `2001:DB8:1:10::1` |
| Engineering | `2001:DB8:1:20::/64` | `2001:DB8:1:20::1` |
| Servers | `2001:DB8:1:30::/64` | `2001:DB8:1:30::1` |
| Remote Branch | `2001:DB8:1:40::/64` | `2001:DB8:1:40::1` |
| Router link | `2001:DB8:1:99::/64` | R1: `::1`, R2: `::2` |


## Static IPv6 Addresses

| Device | Role | IPv6 address |
|:-------|:-----|:-------------|
| R1-HQ G0/0 | Administration gateway | `2001:DB8:1:10::1/64` |
| R1-HQ G0/1 | Engineering gateway | `2001:DB8:1:20::1/64` |
| R1-HQ G0/2 | Server network gateway | `2001:DB8:1:30::1/64` |
| R2-BR G0/0 | Branch gateway | `2001:DB8:1:40::1/64` |
| DNS Server | DNS and HTTP services | `2001:DB8:1:30::11/64` |


## Automatic IPv6 Configuration

Computers use SLAAC, which stands for Stateless Address Autoconfiguration.

The routers send Router Advertisement messages containing the IPv6 prefix of each network.

Using this information, each computer can:

1. generate its own IPv6 address;
2. identify the local network prefix;
3. learn the IPv6 default gateway.

The DNS server address was configured separately on the computers so that they can resolve domain names through IPv6.


## Link-Local Addresses

Router interfaces also use the link-local address:

`FE80::1`

A link-local address is used for communication inside the local network segment and is not routed between different networks.

The same link-local address can be used on different router interfaces because each interface belongs to a different local network.


## IPv4 and IPv6 Comparison

| IPv4 | IPv6 |
|:-----|:-----|
| Example: `192.168.20.12` | Example: `2001:DB8:1:30::11` |
| Uses a subnet mask such as `255.255.255.0` | Uses a prefix length such as `/64` |
| Computers receive addresses through DHCP | Computers generate addresses through SLAAC |
| DNS uses an A record | DNS uses an AAAA record |
| Uses ARP to discover local devices | Uses Neighbor Discovery |