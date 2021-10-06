# Services and Firewalls

## Services and Daemons
A service is some program that runs in the background that processes requests (like time update, or the mail server _which is smtp_).
A Daemon operates in the background like a service but the Daemon only serves it's master.

## Managing services
Check what we have with `systemctl`:
- If we want to check a specific service use `systemctl status [service name]`
- You can disable services with '`systemctl disable [service]` - it will remain active and running but it means that at boot time it will not initiate
- To stop that service right there use `systmctl stop [service]`
- To enable it use `ststemctl enable [service]` (set of symlinks happening)
- To activate it use `systemctl start [service]`

## Service Scripts
Recall the symlinks created when enabling a service (you can go to the directory) - those are the scripts.

## Netstat
To check the state of the actual running services with `netstat` (for example with know ssh is on port 22).
- `netstat -tunap` this shows tcp, udp, the IP numbers instead of names and all. p stands for processes that are using it. 

## Nmap
Port scanning and much more!
- example `nmap localhost`
- check ip with `ap addr` and you can then scan it with the `nmap [address]` (you wouldn't get the same because some only sit on the localhost.)
- From the outside you can only see what gets in the firewall: we could see the ssh service. What means is that the other services didn't send a respond back.

## Scheduling tasks
`crontab` location is in _/var/spool/cron/_
You can use it by editing the crontab file `crontab -e`
    - enter the 5 fields (minute, hour, day of month, month, day of week) and what is to be executed (like a command line command).
    - use `man 5 crontab` for the fields info
    - file gets saved automatically in the location above
    - be aware: somtimes it produces mail (in _/var/spool/mail_)
Also location _/etc/cron.*_ which has different cron options (daily, hourly...). You can cd in it to see what's running.

## Firewalls
CentOS on redhat right now, lives in _/usr/lib/firewalld/_
- restart with `systemctl restart firewalld`
- check `firewall-cmd --list-all'` lists services allowed through.
- also check them all with `firewall-cmd --get-services` or in direcotry and then in services.
- add service with `firewall-cmd --add-service=[service]` but if you reboot the changes will no longer be there, add `--permanent` option for that (careful, service might not be running yet, it turned on the port only)
- remove with `firewall-cmd --remove-service=[service]` and can add `--permanent`
- in _etc/firewalld/zones/public.xml_ you can see what is open and if something was openned and added permanetly it will appear there.
- want to add a port? `firewall-cmd --add-port=###/tcp` still not permanent. Can also remove like services
