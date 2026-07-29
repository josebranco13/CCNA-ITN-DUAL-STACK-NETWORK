# IPv4 Addressing Plan

## Overview

IPv4 addresses are used to uniquely identify devices on the network.

Each company area was assigned a separate IPv4 network. This prevents address conflicts and allows the routers to forward traffic between the different areas.

Each device requires:

- an IPv4 address, which identifies the device;
- a subnet mask, which identifies the local network;
- a default gateway, which allows the device to communicate with other networks;
- a DNS server address, which allows names such as `www.network.local` to be translated into IP addresses.


## IPv4 Networks

| Area | Network address | Subnet mask | Default gateway |
|:-----|:----------------|:------------|:----------------|
| Administration | `192.168.10.0/24` | `255.255.255.0` | `192.168.10.1` |
| Engineering | `192.168.20.0/24` | `255.255.255.0` | `192.168.20.1` |
| Servers | `192.168.30.0/24` | `255.255.255.0` | `192.168.30.1` |
| Remote Branch | `192.168.40.0/24` | `255.255.255.0` | `192.168.40.1` |
| Router link | `192.168.50.0/30` | `255.255.255.252` | Not applicable |


## Static IPv4 Addresses

| Device | Role | IPv4 address | Default gateway |
|:-------|:-----|:-------------|:----------------|
| R1-HQ G0/0 | Administration gateway | `<ADDRESS>` | Not applicable |
| R1-HQ G0/1 | Engineering gateway | `<ADDRESS>` | Not applicable |
| R1-HQ G0/2 | Server network gateway | `192.168.20.1` | Not applicable |
| R1-HQ WAN | Headquarters WAN interface | `<ADDRESS>` | Not applicable |
| R2-BR G0/0 | Branch gateway | `<ADDRESS>` | Not applicable |
| R2-BR WAN | Branch WAN interface | `<ADDRESS>` | Not applicable |
| DNS Server | DNS and HTTP services | `192.168.20.12` | `192.168.20.1` |
| DHCP Server | DHCP service | `<ADDRESS>` | `<GATEWAY>` |
| Administration Printer | Network printer | `<ADDRESS>` | `<GATEWAY>` |
| Branch Printer | Network printer | `<ADDRESS>` | `<GATEWAY>` |