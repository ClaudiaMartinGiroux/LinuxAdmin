# Samba Overview

It's a file protocol which has nice interaction with windows and Mac OS X systmes and Unix and allows them all wo connect as clients. Build on *SMB* which has had many exploits.

## Packages
- `samba`
- `samba-client` to navigate remote shares
- `cifs-utils` to mount samba shares

## Start
- Use `systemctl start smb.service' (and recall to enable).
- Needs to get through firewall with `firewall-cmd --zone=public --add-service=samba` and check with `firewall-cmd --list-all`

## Configuration
Found in _/etc/samba_ mainly the _smb.conf_ file.
Example:
```
[software]          // based on the /share/software dir
comment = Windows Software Packages
path = /share/software
public = yes
writable = yes
printable = no      // it's not a printer
```

## SELinux issues
You might have issues with the contest type which must be `samba_share_t` (recall ServicesFirewall.md for fix).

## Troubleshooting
- IP (ip addr)
- Services are running (netstat)
- Firewall (firewall-cmd --list-all)
- SELinux context (ls -alZ)
- Remote host is up (ping)
- Remote ports are open (nmap)
- Check logs (/var/log)