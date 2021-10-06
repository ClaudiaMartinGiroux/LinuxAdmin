# Network File System Overview

Useful items:
- _/Client/FileSystems.md_
- _/Client/ServicesFirewall.md_

You need **nfs-utils** and **man**.
Make sure it happens after the RPC so:
- `systemctl start rpcbind.service`
- `systemctl start nfs-server.service`
Recall: for them to happen at boot time they ust be enabled.

## Sharing directories
It needs a series of directories to export listed in _etc/exports_ file. The format is `[directory] [who or * for everyone](permissions)`. Then use `exportfs` you can use `-a` for all shares.

## Firewall rules
For NFS to get through, do: 
- `firewall-cmd --zone=public --add-service=rpc-bind`
- `firewall-cmd --zone=public --add-service=nfs`
Might need `--permanenet` for after firewall is rebooted.
To check use either `firewall-cmd --list-all` or `firewall-cmd --zone=public --list-services`.
(When you use enable it will create the needed symlinks).

## Mounting NFS shares
Check you can manually mount them before putting them in _fstab_.
To do so you: `mount [servername]:[share or dir exported] [mountpoint or dir of location]`
example: `mount sample.com:/music local/music`.
Put it in the _etc/fstab_ then! Check useful items.

## Troubleshooting
Check:
- Ip Address is correct
- Services are running (use exportfs or netstat)
- Firewall is not on the way (firewall-cmd)
- Remote host is up (use ping)
- Ports are open (nmap)