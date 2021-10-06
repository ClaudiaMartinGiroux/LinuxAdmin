# Secure Shell Server Overview

## Background 
MariaDB is based on MYSQL.

### Concerns
The installation doesn't have a root password... also administrators can reset root password and get full access

## Useful packages
- **mariadb** client programs 
- **mairadb-server** which are server programs
- **MySQL-python** MySQL python interface

## Use
- Configuration is found in _/etc/ssh/sshd\_config_ for server and _/etc/ssh/ssh\_config_ for client.
- Also _~/.ssh_ individual users info.
- Common configuration changes would be:
    1. disabling root logins - `PermitRootLogin no` (situations where there are constant attacks)
    2. changing the port number - `Port 2222`
    3. disabling password authentication - `PasswordAuthentication no` (so you have to use kwys to get in which makes it more secure)
    4. changing to X11 forwarding - `X11Forwarding no` (X11 is the gui system so you set it so you can export it or not)
- Use `systemctl` to start and enable callind `sshd.service` 
- SSH is allowed by default through firewall but had be added or removed calling `ssh`. Options can be made `--permanenet` and recall `firewall-cmd --list-all` to verify.

### Keys and known hosts
When connecting to unknown servers, SSH gives you a pubKey which is stored in _~/.ssh/known\_hosts_. Rarely do keys change (replaced machine of mitmattcak). You can manually add and delete entries (for example the ones you trust).

### Key based authentication
Generate a pub/priv key pair with _ssh-keygen_. pubkeys in need to be installed in serves _.ssh/authorized\_keys_ file. To do so you can install/push the pubkey using _ssh-copy-id_ or manually with an editor.
Examples:
- `ssh-keygen -t [type]`
- `ssh-copy-id [user]@[hostname]` to copy pubkey over
- manually copy the pubkey with:

```
scp id_rsa.pub [user]@[hostname]
cat id_rsa.pub >> authorized_keys
```

### Tunneling incantations
- `tar cvfz - [directory] | ssh [hostname] "cat > [file].tar.gz"` tar creates archive files in the stdout to be piped into file in the remote machine
- `tar cvfz - [directory] | ssh [hostname] "tar xvfz - [path]"`
- `rsync -avz -e ssh [hostname]:[remotepath] [localpath]`
- `ssh [user]@[hostname] "firefox"`

## Troubleshooting
- Ip (ip addr)
- services (netstat)
- firewall (firewall-cmd)
- SELinux (ls -alZ)
- remote host (ping)
- remote ports (nmap)
- httpd logs (/var/log/secure)