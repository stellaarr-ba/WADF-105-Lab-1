# Laboratory Completion Questions and Answers

## 29. What is the difference between the OPNsense WAN and LAN interfaces?

The WAN interface connects OPNsense to the upstream network through VirtualBox NAT, providing a path to the internet. The LAN interface connects OPNsense to the protected ICDFA-LAN network and serves as the Ubuntu client's gateway.

In my lab, the WAN address was 10.0.3.15/24, while the LAN address was 10.10.10.1/24.

## 30. Why must both internal adapters use the same VirtualBox network name?

VirtualBox uses the internal network name to identify which virtual adapters belong to the same virtual network. Both adapters must use exactly ICDFA-LAN so that Ubuntu and the firewall's LAN interface can communicate directly.

Different names would place the adapters on separate virtual networks. The name is case-sensitive.

## 31. What information does the default route provide to Ubuntu?

The default route tells Ubuntu which next-hop gateway and network interface to use when no more specific route matches the destination.

In my lab, it instructed Ubuntu to send this traffic through gateway 10.10.10.1 using interface enp0s3.

## 32. Which packet exchange allows Ubuntu to learn the firewall MAC address?

An ARP request and reply exchange allows Ubuntu to learn the firewall's LAN MAC address.

Ubuntu broadcasts a request asking which device has IPv4 address 10.10.10.1. OPNsense replies with its LAN MAC address, which Ubuntu stores in its neighbour table.

## 33. Why does a successful ping to 1.1.1.1 not automatically prove that DNS is working?

The command uses an IP address directly, so it does not need DNS to resolve a hostname. A successful ping confirms IP connectivity and ICMP replies, but DNS could still be unavailable or incorrectly configured.

I tested name resolution separately using getent hosts opnsense.org and verified the DNS query and response in Wireshark.