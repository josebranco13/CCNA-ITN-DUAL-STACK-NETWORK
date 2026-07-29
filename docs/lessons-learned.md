# Lessons Learned

## Overview

This project helped transform theoretical networking concepts into a practical network implementation.

The project required different technologies to work together, including IPv4, IPv6, routing, DHCP, DNS and HTTP.

---

## Network Planning

One of the main lessons was the importance of planning before configuring the devices.

Each company area required:

- its own IPv4 network;
- its own IPv6 prefix;
- a router interface;
- a default gateway;
- a connection to the correct switch.

Creating an addressing plan before configuring the devices reduced errors and made the network easier to understand.

---

## IPv4 and IPv6 Work Independently

The project demonstrated that IPv4 and IPv6 are separate protocols.

A device can communicate successfully through IPv4 while still having an incorrect IPv6 configuration.

For this reason, both protocols must be configured and tested separately.

This is an important characteristic of a dual-stack network.

---

## Importance of the Default Gateway

The default gateway is required when a device needs to communicate outside its local network.

A device may have a correct IP address but still fail to reach another network when:

- the gateway is missing;
- the gateway is incorrect;
- the gateway belongs to another network;
- the router interface is disabled.

The IPv6 communication problem with the DNS server helped demonstrate the importance of the default gateway.

---

## IPv6 Automatic Configuration

The computers used SLAAC to automatically configure their IPv6 addresses.

The routers send Router Advertisement messages containing the IPv6 prefix used by the local network.

Using this information, computers can:

- generate their own global IPv6 address;
- identify the local network;
- learn their IPv6 default gateway.

Servers use static addresses because network services should always remain available at known addresses.

---

## DNS and HTTP Have Different Roles

The project helped clarify the difference between DNS and HTTP.

DNS translates a readable name such as:

```text
www.network.local
```

into an IP address.

HTTP provides the actual webpage.

Therefore:

- DNS finds the address of the server;
- HTTP provides the webpage stored on the server.

The project also demonstrated that:

- an `A` record is used for IPv4;
- an `AAAA` record is used for IPv6.

---

## Static Routing

Routers automatically know only the networks directly connected to their interfaces.

Static routes are required to reach networks connected to another router.

The project also demonstrated that IPv4 and IPv6 require separate routing configurations.

An IPv4 route does not automatically create an equivalent IPv6 route.

---

## DHCP

DHCP makes network administration easier by automatically providing IPv4 configurations to computers.

Without DHCP, every client would need to be configured manually.

Servers and printers still require static addresses because other devices need to know where to find them.

---

## Step-by-Step Troubleshooting

One of the most important lessons was to test communication in stages.

A useful testing order is:

1. check the local device configuration;
2. ping the local gateway;
3. ping the remote router interface;
4. ping the destination device;
5. test the network service;
6. test the service using its DNS name.

This method helps identify the exact point where communication fails.

Changing only one configuration at a time also makes it easier to understand which correction solved the problem.

---

## Connectivity and Services Are Different

A device responding to `ping` does not necessarily mean that all its services are working.

For example:

- the server may respond to ping;
- the DNS service may still be disabled;
- the HTTP service may still be disabled;
- the DNS record may contain an incorrect address.

Basic connectivity and application services must therefore be tested separately.

---

## Documentation

Documenting the project was an important part of the work.

The addressing plans, configuration files, screenshots and test results allow another person to:

- understand the network;
- identify the purpose of each device;
- reproduce the configuration;
- verify the results;
- troubleshoot possible problems.

Good documentation is an important networking skill because real networks are normally maintained by more than one person.

---

## Final Reflection

This project improved my practical understanding of:

- network topology design;
- Cisco Packet Tracer;
- IPv4 addressing;
- IPv6 addressing;
- dual-stack networking;
- default gateways;
- static routing;
- DHCP;
- SLAAC;
- DNS;
- HTTP;
- network verification;
- network troubleshooting;
- technical documentation.

The main conclusion is that a network should not only be configured.

It should also be tested, documented and explained clearly.