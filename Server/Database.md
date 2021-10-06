# Database Server Overview

## Background 
The Secure Shell (SSH Protocol) is used to create safe info transfer tunnels using Diffie-Hellman key exchange.

## Useful packages
They are usually installed but:
- **openssh-server** provides SSH server
- **openssh** tools like ssh-keygen
- **openssh-clients** for ssh client command line
- **rsync** makes it easy to synchronize or backup data between two machines

## Use
- Configuration is found in _/etc/my.cnf.d_ with simple `name=value` pairs.
- Use with normal SQL commands.

## Troubleshooting
- Ip (ip addr)
- services (netstat)
- firewall (firewall-cmd)
- SELinux (ls -alZ)
- remote host (ping)
- remote ports (nmap)
- httpd logs (/var/log/mariadb/mariadb.log)