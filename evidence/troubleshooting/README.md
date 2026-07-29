# Troubleshooting Evidence

This directory contains evidence related to an IPv6 communication problem identified during the project.

The problem affected communication between a client computer and the DNS server.

## Evidence Files

| Evidence | Purpose |
|:---------|:--------|
| [IPv6 Failure Before the Correction](ipv6-failure-before-fix.png) | Shows the unsuccessful IPv6 communication attempt |
| [Router Configuration Check](ipv6-router-configuration-check.png) | Shows the router interfaces and IPv6 configuration examined during diagnosis |
| [Corrected Server Configuration](ipv6-corrected-server-configuration.png) | Shows the corrected IPv6 address, prefix and gateway of the DNS server |
| [Successful Ping After the Correction](ipv6-ping-after-fix.png) | Confirms that communication was restored after correcting the configuration |

---

## Reported Problem

A client computer was unable to communicate with the DNS server using IPv6.

The following test was unsuccessful:

```text
ping 2001:DB8:1:30::11
```

IPv4 communication was operational, which indicated that the physical links and basic network structure were working.

---

## Diagnostic Process

The communication path was tested step by step:

```text
Client PC → Local Switch → R1-HQ → Server Switch → DNS Server
```

The following items were checked:

- client global IPv6 address;
- client IPv6 prefix;
- client default gateway;
- DNS server IPv6 address;
- DNS server prefix length;
- DNS server default gateway;
- router interface connected to the client network;
- router interface connected to the Server network;
- IPv6 routing table;
- IPv6 forwarding configuration.

The following commands were used:

```text
show ipv6 interface brief
show ipv6 route
show running-config
```

---

## Cause

The IPv6 configuration used by the client, router and DNS server needed to be consistent.

The Server network uses:

```text
2001:DB8:1:30::/64
```

The router interface uses:

```text
2001:DB8:1:30::1/64
```

The DNS server uses:

```text
2001:DB8:1:30::11/64
```

IPv6 forwarding also needed to be enabled using:

```text
ipv6 unicast-routing
```

---

## Resolution

The router interface connected to the Server network was configured with the correct IPv6 prefix.

The DNS server was configured with:

```text
IPv6 address: 2001:DB8:1:30::11
Prefix length: 64
Default gateway: FE80::1
```

The interface was enabled and IPv6 forwarding was confirmed.

---

## Final Verification

After correcting the configuration, the original test was repeated:

```text
ping 2001:DB8:1:30::11
```

The DNS server responded successfully.

This confirmed that IPv6 communication between the client and the Server network had been restored.

---

## Lesson from the Incident

A device requires more than a valid IPv6 address.

Communication with another network also requires:

- the correct prefix;
- a valid default gateway;
- an operational router interface;
- IPv6 forwarding;
- a valid route to the destination.

The complete incident report is available in:

[Network Troubleshooting](../../docs/troubleshooting.md)

[Return to Project Evidence](../README.md)