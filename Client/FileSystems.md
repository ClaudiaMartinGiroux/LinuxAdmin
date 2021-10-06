# File Systems

Recall Digital Forensics for more info. Different file systems have different features that can make them better for storing images for example (like journaling: say what you are going to wrtie, write it and then remove the entry).

## Partitions
Partition tables have the info of the pieces of the disk (of the volumes).

Can edit with `fdisk`. The kernel doesn't know until you use utilities to reread partition tables (use `ioctl()`).

Formats are:

### MBR: Master Boot Record
Adresses are only up to 32bit numbers. Quite limiting of large harddrives.
### GPT: GUID Partition Table
Resolves MBR issues like partitions allowed, and addresses.

## Handling partitions
Can do it from utilities, disk. But form CL:
- `fdisk -l` to see patitions
- `fdisk [partiton name]` 
    - can use `m` to see options of actions
    - `p` to see partition table in the partition name
    - `n` for new one then choose type of partition
    - decide how big next  `+####M` M for example for megabytes.
    - you can then choose type of file system to see options use `l` and use the hex value.
    - once chosen use `w` to write it.
    DONE

## Formatting
We now need to give it a file system using mkfs.
Run `mkfd.[system] [partition]` to call partitions it's like calling a dir (recall _fdisk_ to see them all). Can add labels and other options.
- labels can be: `[partiton] -L [the label]`
- to chage it same command but different system extension but you can use `-f` to forece rewrite.
- if there is data, some (ext2 to ext3) you add a journal
    - `tune2fs -j [partition]` (no need to mkfd then) 

## Mounting
You need to mount it (it it doesn't mount, might not be formatted). You take part of your dir structure and link it to the new partition.
- Where shall we put the partiton? for example in a directory. Do `mount [partition] [the  mount point]`
- to unmount can do `umount [partition]` or `umount [mount point]`. if fstab is updated `mount` and `umount` can be used with only the partition or the mount point.

## File system table
Has the info of where things are mounted to.
- do `nano /etc/fstab/` and then in there input: 
`[partition]     [mount point]      [type]       defaults       0    0` then exit and save (keep the tabs in between).
- if you use `mount` you should see it's now mounted.
Once the fstab  has been updated, mount and umount can be done to the partiton and it would affect the mount list of partitons.
**MAKE SURE YOU DON'T HAVE ISSUES IN FSTAB OR IT COULD MAKE EVERYTHING CRASH**

## File System Features
- use `stat [filename]` for detailed file info
- SELinux for access but really nice and secure. [CentOS deets](https://wiki.centos.org/HowTos/SELinux)
- Disk quotas: keep track of what you do on files