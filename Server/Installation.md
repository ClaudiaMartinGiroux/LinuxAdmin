# Linux Installation Overview

## CentOS
It fits inside the Red Hat Enterprise Linux (inside Red Hat family).
You first find the Anaconda Installar (install wizard written in Python and C). It's responsible for making sure the OS is correct.

You have to configure networking:
    - Hostname (don't stay with localhost)
    - DHCP or static manual adresses (ip addr, mask, gateway and DNS)
    - Activate the interface
Other confirgure:
    - Date and time based on time zone (after networking for NTP updates)
Select software:
    - easy to start with gnome desktop
    - for server, start with minimal install

## Instalation destination
Anaconda can automatically create partitions (standard with older names and fixed size or use LVM partitions and use blocks for more flexibility).
Partitions you usually want:
- `/` for root
- `swap` for virtual memory
- `/boot` for boot loader
Once install, check /Client/PeoplePermissions.md file for groups and user information.