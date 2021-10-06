# Kernel and Hardware

## Kernel
To know about which kernel you are running, use `uname -r` command. Also check inside _/etc/_ the distribution rlease.
Even more info in _/proc/version_.

Where is it? in the boot directory (recall _/etc/fstab_).

At times, if a kernel can't be read, it might be because it lacks drivers. Any new drivers must go in the _initram_.

The source code is in the _/usr/src/kernels_ directory. some versions are shit without the kernel. 
You can download `kernel-devel` for the headers and even the ncurses for a gui you can `make menuconfig` after do `make all`.
We might need drivers still based on the hardware!
kernel building can take hours or at best to 20 minutes.

### Changing kernels
Recall bootloader need to know which kernel to load.
Inisde the boot directory, go into grub but you want to find _menuentry_ info at the begining. It should reflect the kernel and distribution you are using there.
Check inside the _grub.d_ directory inside _etc_.
Use `grub#.*` like `grub2.mkconfig` as different kernal file changing commands.

## Hardware
- Run `lsusb` to know usb info
- run `lspci` for more hardware info you can use `-v` for hardware but also drivers info for the hardware (more info with `-vv` or even `-vvv`).

### Modules
Kernel modules are basically drivers - they are built outside because you may not need them all and some might conflict.
Which are loaded? use `lsmod` or go in the _/lib/odules/[kernel]_ directory.
- Let's say you want to find the net driver, you do: `find /lib/modules[hernel] | grep [netdriver]` and it will show you the dirs and files that get loaded at boot time.
How do I load them? `insmod` or `modprobe`.
