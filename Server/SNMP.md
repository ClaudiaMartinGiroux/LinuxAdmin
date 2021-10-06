# Simple Network Management Protocol Overview

## Background
Used for info from network devices. Operates on UDP ports 161 and 162.

### MIB
SNMP provides info in hierarchical dotted format called Object Identifier (OID). 
The OID for hostname is `1.3.6.1.2.1.1.5.0`.
The Management Information Base (MIB) provides names for the numbers. You can get the hostname with `sysName.0` or `system.sysName.0`.

### Community Strings
Basically a password: 
1. For read-only info you can use the default community string **public**
2. For read-write info and setting you can use the default community string **private**

### Issues
1. SNMP uses UDP so messages with incorrect community string are ignored - you don't know if a message is ignored or dropped
2. Many network devices have active SNMP (like printers with public and private turned on) and admins are not aware - make sure you turn it off
3. Not secure - stuff comes and goes in plaintext

## Packages
- **net-snmp** snmp server
- **net-snmp-utils** utilities for performing queries and making changes like:
    - `snmpget`
    - `snmpset`
    - `snmpwalk` ...

## Configuration
Server is configured in _/etc/snmp/snmpd.conf_ where you can change the community string for example like:
```
com2sec notConfigUser default public
```
to
```
com2sec notConfigUser default aloha123
```

## Geneal setup
- Use `systemctl` to start or enable the `snmpd.service` service.
- Recall to add the service to the firewall calling it `snmp` and make it permanenet if you want.

## Usage
To verify it's working try with the utils package. Assuming the community string is *aloha123* and you are connecting to ocalhost although you could connect to IP of a server:
```
// you pass the version with -v usually 1 or 2c
// you pass the community string with the -c option

// here you are getting the system name (so sysName.0)
snmpget localhost -v 2c -c aloha123 sysName.0

// here you are walking the entire system 
snmpwalk localhost -v 2c -c aloha123 system
```

## Troubleshooting
- check DNS is set (/etc/resolv.conf)
- check you can talk to snmp server (ping)
- check the firewall is set correctly
- check the logs (/var/log/messages)
- check the community string is correct
- make sure the object name is correct (sysName.0)
- check service is running (netstat -tunap)