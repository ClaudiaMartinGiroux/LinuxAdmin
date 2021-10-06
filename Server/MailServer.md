# Mail Servers (Postfix) Overview

## Background 
The Simple Mail Transfer Protocol (SMTP) uses paintext commands to communicate with remote servers listening on TCP port 25.
It's by default on CentOS listening locally.

## Useful packages
- **postfix** the SMTP mail server
- **dovecot** support for mail over protocols like POP and IMAP
- **telnet** terminal that allows you to connect to ports
- **alpine** nano like email client (need first epel libraries from epel-release packages)

## Files and Directories
| Directories | Contents |
|----|----|
| /etc/postfix | containing config giles|
| /var/spool/mail | contains and mbox file for each user with all ther mail messages|
| /var/spool/postfix | dir and subdirs where data is stored acting as server|
| /var/log/maillog | logs to troubleshoot mail problems|

## Security concerns
1. Plaintext messages can be viewed.
2. SPAM is very cheat (anyone can send unsolicited messages)
3. Allow relays (making easier to spoof)
4. Messages can contain malware files themselves
5. Rejected messages can be used for directory harvesting attacks (send message to everybody in system and the ones bounced probs mean there is no one is there and use the info of the ones there to try to login)

## Allow Postfix on external connections
Edit the _/etc/postfix/main.cf_ by changing it to: 
```
inet_interfaces = all
#inet_interfaces = localhost
```
Then start service with `systemctl start postfix.service` it should be running by defualt so should not require enable.
Make sure to let it through the firewall to TCP port 25 using `firewall-cmd --add-service=smtp` and verify with the `--list-all` argument you can also make it permanenet.

## External Email Server Identification
It does not use the _/etc/hosts_ files but uses the _host@domain_ structure and checks for a DNS server (first MX record and if not found A record).

## Troubleshooting
- Ip (ip addr)
- services (netstat)
- firewall (firewall-cmd)
- verify the DNS records (dig -t MX [server])
- SELinux (ls -alZ)
- remote host (ping)
- remote ports (nmap)
- logs (/var/log/maillog)
- mail directory (/var/spool/mail)