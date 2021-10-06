# Domain Name System Overview

## Background
Domain Name Systems Protocol converts names to IP addresses. It operates on UDP(normal enqueries) and TCP(downloads of zone transfers) ports 53.

### Security issues
1. If you send a request to the DNS and the reply is spoofed (you get a fake response plus other response) it might keep those entries
2. Alternative root DNS can redirect all your traffic
3. DNS manupulation by ISPs
4. Registrar based DNS manipulation

### BIND DNS notes
All host names end with trailing dot. Most of the time it's not seen but BIND needs it and treats it.
Host names and IP addresses in the DNS have largest grouping to the right and smallest to the lest (example: example.es.com).

### Packages
- **bind** BIND DNS server
- **bind-utils** utilities for DNS servers and querying DNS info

### Files and Directories
| Directories | Contents |
|----|----|
|/etc/named.conf | main bind config file|
|/var/named/ | main dir tree for dns zone files|
|/var/names/data/ | dir for zones you control|
|/var/names/slaves/ | dir for zone files that you are acting as secondary/slave for (that you get from somebody else|

## Config example
_named.conf_
```
zone "domain.ext" {
    type master;
    file "doamin.ext.zone"; // probs in /var/named
}

zone "[ipaddress].in-addr-arpa" { // for example 10.
    type master; // could be typer slave if secondary
    file "[ipaddress].zone";
}
```

### Zones
#### Forward zones
Zone that uses names as lookup. This would be the _domain.ext_ forward zone file:
```
$TTL 3h;                    // Time to live for each entry (default)
// @ is for entire zone
@   IN   NS    dns.domain.ext. // zone is named in named.conf
@   IN   SOA   domain.ext. root.domain.ext. ( // the (root...) is the email address and it actually replaces the first dot with an @
    YYYYMMDD00 ; serial // year month day serial number so when doing zone transfers if number is not changing, it will assume no changes have changed
    10800; refresh // written in seconds
    3600; retry
    604800; expire
    86400; default ttl
    )
dns IN  A   [apaddress] // normal IP address format
```
  
#### Reverse zones
Reverse zones go from ip addresses back to names.
```
$TTL 3h;                   
@   IN   NS    dns.domain.ext.
@   IN   SOA   domain.ext. root.domain.ext. ( 
    YYYYMMDD00 ; serial
    10800; refresh
    3600; retry
    604800; expire
    86400; default ttl
    )
$[origin] 0.168.192.in-addr-arpa. // this is doing the 168.192.0 range below
0   IN  PTR     network.domain.ext.
1   IN  PTR     gateway.domain.ext.
```

## Usage
- Use `systemctl`to start it calling it `named.service`, remember to enable for boot.
- Use `firewall-cmd` to add the `dns`. Will need both UDP and TCP port 53 for zone transfers. Use `--permanent` if you want and check with `--list-all`.

## Troubleshooting
- check DNS server is set (/etc/resolv.conf)
- check you can talk to dns (ping, nslookup)
- check records can download (nslookup, dig)
- trace dns hierarchy (dig +trace)
- check firewall
- check logs (/var/log/messages)
- make sure MX and CNAME point to valid A or AAAA (check into dns records)
- check service is running (netstat -tunap | grep named)
- SELinux context (ls -Z)