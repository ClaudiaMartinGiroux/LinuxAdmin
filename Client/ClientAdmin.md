# Client Side Linux

## Background 
### What is Linux
Linux is a Kernel that powers different Linux Operating Systems -> Kernel + OS is a Linux Distribution.
Kernel speaks to the hardware and manage resources - all else speaks to the Kernel throgh syscalls.

CL = Command Line

### Distributions (Families)
- **Red Hat** (packets come in RPM files, DB takes care of checking which are installed and dependencies - more company) like CentOS, Fedora, Oracle...
- **Debian** (Like red hat but dev packages instead of RPM - more end user) like Ubuntu, Kali, Mint
- **Source Code** (to optimise stuff - can also be worse)
- **SystemD** (System V Init) (Init was the first thing to run ofter the Kernel and it starts services and GUI or CL... - SystemD is to not be as sequencial as Init) like Android, Arch, Gentoo...

### Hardware considerations
1. Can it boot installation media? USB, floppy disk...
2. Hard drive space you need?
3. How much RAM do you need? Atleast 1 gigabyte
4. Will video or wireless card work? (Yes drivers but if source code is already at best then its optimised, better...)
5. Any other hardware need? camares, mics... any software...?

## Installation
- DVD or ISO installation (like for VMs)
- USB 
- Hard Drive (if its already there)
- Network installation (requires boot service)

Time and date matter for this. Time zones, and network time (which is requested to the server). Linux instead of using local time, it uses UTC to work with moving from one time zone to the other.

You want to select the right software: minimal install of full for desktop, what about hardare? am i running it as server?... You can always install packages from repos later.

Set _root_ there! then set other users (admins so you can run root, users...) make sure to set the passwords. Login from GUI or CL. Pass username and password. Can login with root too (ctrl+alt+f2 for CL too for root).

#### Kdump
Feature to have all memory writen to hard drive in case of Kernel crash.

### Partitions
- **SWAP Partition** run out of memory so it takes a portion and uses it as virtual memory (you run out of RAM) so you take pieces of not used RAM temporarily to read, and then when need the RAM, info is moved to hard drive. Don't to it much - makes it slow.
- **LVM** (Logical Volume Management) to resize and mve data and more partitions...

You need **FILE SYSTEM** - minex and then ext 1, and 2, 3... (can have FAT32...). **MOUNT POINT** so you have partition (root as first) and hav directories there that can redirect to other partitions = mount point (in Windows, C drive, H drive...)

### Networking
- Need _Hostname_ to avoid just localhost (need networking for updates) which is set in _/etc/hostname_
- DHCP or manual config? client usually DHCP and manual usually for server
You can change networking later.

Use _IP Config_ for IP, MAC address info or type `ip addr`. 
DNS is also in _/etc/resolv.conf_.
IP is set usually in _/etc/sysconfig-[interface name]_.
To test network use ping for example.

#### Boot Process
Boot loader load the OS. It can have different boot options (can access from BIOS or GRUB Configurations). Boot directory has kernel, RAM disc, mapping and grub config.

## Software Updates
- Use YUM `yum update yum` which is an update updater. Also just `yum update` can install with `yum install.
- `rpm -qa` to see all packages to `rpm -q [package]` to see if it's there.
- uninstall with `yum remove [package]` or `rpm -e [package]`.
- ssh is installed by default. To remote connect `ssh [username]@[ipaddress]` to login.
- to shutdon on CL us `shutdown [when or now]` or use `eboot`.