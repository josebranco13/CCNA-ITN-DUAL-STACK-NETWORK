# Network Troubleshooting

## Overview

Troubleshooting is the process of identifying, analysing and correcting network problems.

During this project, problems were investigated step by step instead of changing several configurations at the same time.

The general troubleshooting method was:

1. identify the problem;
2. verify the local device configuration;
3. test the local default gateway;
4. test the next network device;
5. inspect the router interfaces;
6. inspect the routing tables;
7. correct the configuration;
8. repeat the original test.

---

## Incident 1 — IPv6 Communication Failure

### Problem

A computer was unable to reach the DNS server using IPv6.

IPv4 communication was working, but the following IPv6 test failed:

```text
ping 2001:DB8:1:30::11
```

---

### Expected Behaviour

The computer should have been able to communicate with the DNS server through the headquarters router.

The communication path was:

```text
Client PC → Local Switch → R1-HQ → Server Switch → DNS Server
```

---

### Diagnostic Process

The problem was investigated by checking:

- the IPv6 address of the computer;
- the IPv6 prefix used by the computer;
- the IPv6 default gateway of the computer;
- the IPv6 address of the DNS server;
- the prefix length of the DNS server;
- the default gateway of the DNS server;
- the router interface connected to the client network;
- the router interface connected to the Server network;
- whether IPv6 routing was enabled.

The following router commands were used:

```text
show ipv6 interface brief
show ipv6 route
show running-config
```

The connection was then tested in stages.

First, the client tested its local gateway:

```text
ping <LOCAL_IPV6_GATEWAY>
```

The client then tested the router interface connected to the Server network:

```text
ping 2001:DB8:1:30::1
```

Finally, the client tested the DNS server:

```text
ping 2001:DB8:1:30::11
```

---

### Cause

The problem was related to the IPv6 configuration of the communication path to the DNS server.

The router interface, server address, prefix length and default gateway needed to use a consistent IPv6 configuration.

IPv6 forwarding also needed to be enabled on the router.

---

### Resolution

The router interface connected to the Server network was configured in the following IPv6 network:

```text
2001:DB8:1:30::/64
```

The router interface used:

```text
2001:DB8:1:30::1/64
```

The DNS server used:

```text
IPv6 address: 2001:DB8:1:30::11
Prefix length: 64
```

IPv6 routing was enabled on the router using:

```text
ipv6 unicast-routing
```

The router interface was also enabled using:

```text
no shutdown
```

---

### Final Verification

After correcting the configuration, the original test was repeated:

```text
ping 2001:DB8:1:30::11
```

The DNS server responded successfully.

This confirmed that IPv6 communication between the client and the Server network was operational.

---

### Lesson from the Incident

A valid IPv6 address alone is not enough to communicate with another network.

The device also requires:

- the correct IPv6 prefix;
- a valid default gateway;
- an operational router interface;
- IPv6 forwarding enabled on the router;
- a valid route to the destination network.

The incident also demonstrated the importance of testing communication one step at a time.

---

## General Troubleshooting Checklist

The following checklist can be used for future network problems:

- Is the device connected to the correct switch?
- Is the cable active?
- Is the router interface enabled?
- Does the interface show `up/up`?
- Does the device have the correct IPv4 or IPv6 address?
- Is the subnet mask or prefix length correct?
- Is the default gateway correct?
- Can the device reach its local gateway?
- Does the router know the destination network?
- Is the destination device correctly configured?
- Is the required network service enabled?
- Does the DNS record contain the correct address?