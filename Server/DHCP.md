# Dynamic Host Configuration Protocol Overview

## Background
Operates on UDP ports 68 and 67. It is based on the following messages:
- DISCOVERY
- OFFER
- REQUEST
- ACKNOWLEDGE

### Security issues
1. With Rogue they can give out addresses
2. Clients can spoof MAC addresses
3. Clients can obtain multiple IP addresses by presenting multiple MAC addresses (for example they can be blocked and not used)

## Useful packages
- **dhcp** the server
- **dhcp-libs** service libraries
- **dhcp-common** service common files

### Files and directories
|Directories|Contents|
|-----|-----|
|/etc/dhcp | config files|
|/etc/sysconfig/network-scripts/ifcfg-eth0 | config info con eth0 network interface|
|/var/lib/dhcpd/dhcpd.leases | info about dhcp clients and addresses (the leases) given out by the dhcpd service |
|/var/log/messages | logs including dhcp protocol dialog|

#### Example configuration
Inside the _/etc/dhcp/dhcp.conf_ file example of range addresses giveout:
```
option domain-name "example.com";
option domain-name-servers 8.8.8.8.;  // DNS people are using to get out

default-lease-time 300;               // so 5 minutes
max-lease-time 1200;                  // 20 minutes  you usually want longer times 
subnet 10.10.0.0 netmask 255.255.0.0 {// subnet is the 10.10.0.0/16
    range 10.10.0.100 10.10.0.150;    // we are only giving 51 addresses
    option routers 10.10.0.1;         // the default gateway
}
```
Another example of static IP address assignment (this can be useful for a machine using a MAC address and you always want that one as it provides a specific service). This would go **inside** the _subnet_ section for the previous example:
```
host printer {
    hardware ethernet 00:11:22:33:44:55; // this is the MAC address
    fixed-address 10.10.10.10;
}
```

## To be able to use it
- Use `systemctl`to enable, start (...) the service
- Use `firewall-cmd`to let it to the firewall and remember to make it permanent if you want it at boot time

## Troubleshooting
- Check client have cables and NIC driver (cables, lspci)
- Check server address is static (ifcfg-enXXX)
- Check firewall allows connection (firewall-cmd --list-all)
- Check logs (/var/log/messages)
- Check the leases (/var/lib/dhcpd/dhcpd.leases)
### For non-Linux issues
- Verify the router forwards requests
- Verify spanning-tree is not a problem (sometimes it assumes machines booting up to be switches until it's determined it's not a switch)
- Verify switches allow you to answer (machine needs to be connected to an interface that allows DHCP offers out (it does see the dircovery))