# Apache Web Server Overview

## Background 
HTTPS (HyperText Transfer Protocol Secure) layers HTTP on top of SSL/TLS protocol (TLS is the newer one and it's for signing digital certificates).

Because HTTP is transfered on plaintext it has maaaany issues.
HTTPS also has SSL and TLS levels of security. Certificate Authorities can also be exploited so heads up.

## Useful packages
- **httpd** Which instals Apache and dependencies
- **links** text based web browser if you need to test things
- **openssl** alloows to make and sign certificates
- **mod_ssl** integrate into Apache the HTTPS functionality

## Use
- Start and enable with `systemctl` calling it `httpd.service`
- Firewall rules with `firewall-cmd` setting zone to public and adding the service http and https and make permanent if you want. use `--list-all` to check the rules.
- It's found in _/etc/httpd/conf_ dir and more in _hhtpd.conf_. Other configurations in _/etc/httpd/conf.d_. The standard locations for web pages is the _/var/www/html/_ directory.
- SELinux types - there are a few based on need like:
    1. `hhtpd_sys_content_t` (system web pages)
    2. `httpd_user_content_t` (user web pages)
    3. `httpd_user_script_exec_t` (user CGI scripts)
    4. More for dirs too

## Troubleshooting
- Ip (ip addr)
- services (netstat)
- firewall (firewall-cmd)
- SELinux (ls -alZ)
- remote host (ping)
- remote ports (nmap)
- httpd logs (/var/log/httpd)
- system logs (/var/log/messages)