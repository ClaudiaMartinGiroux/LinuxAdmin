# People and Permissions

## Users
- `w` to see what users are logged in 
- `last` to see history of users logs

### Change pass
- do `passwd [username]` (if not logged like root, then you need to enter pwd to change it)
- hash pass stored check with `cat /etc/shadow`

### Create and add users
to see `user` options, use tab button without a space.
- use `useradd` and see all options like different groups, expiry dates...
    - users get all files from _/etc/skel_ directory. If you go in and modify that will be the case for all *new* users.
- use `userdel` to see all options (if there are imp files, user files are tied to user ID so have to change userID of the files so new users with same ID don't get files)
- to prevent user logging in -> modify the hash pass: `usermod -L [username]` you can check the chnges in _/etc/shadow_. 
- to unlock an account use `usermod -u [username]`

## Groups
- use `id [username]` to see groups and other info
- use `usermod` command to check other group options
- user info can be found:
    - `cat /etc/group` and can see groups and where users are at - can modify and effect comes in next time you log in
    - `cat /etc/sudoers` info con who can use sudo
- Files with group perm allow all users in group to do something with it.
- `groupadd` and `groupdel` to add and del

## Super users
The wheel group means sudoers can run sudo to access stuff that root can. 

### Permissions
RWX =
- Read
- Write
- Execute (as a dir it means going in)
When running `stat` on a directory, recall you can see access (####/permissions) Uid:...
The #### reflect also the type of permissions. 0 means all RWX... and are basiaclly reflecting the permissions.
You can sometimes see and `s` in the permissions, this means it can be run as root user. 6 would mean root user and root group.

Programs can be run as different users based on the Uid (user owner) or Gid (group owner) they have.

File - binary programs are good with x bit set, but scripts for example need the rx bits because it has to first read the path of binary and then there it directs to read the script.

#### Default permisson
- with root the files have rwx to it's own files - sets owner to be open
- user sets owner and group
- use `umask` to see the umask. (dirs start with 7 usually.)
    - root you want to do 0777 - (the mask)0022 = 0755
    - user you do 0777 - (mask)0002 = 0775
    - recall this is the access number discussed in permissions
- change umask in bash or bashrc for example

### chmod & chown
`chmond` is to change mod or permissions. `chown` changes ownership.
- use `chmod  g+w,o-r [file]` means group can write and other can't read.
- `chmod 775 [file]` makes it read, write and execute. 111 is for just execute, 222 is writable, 444 for just readable
- `chown [user]:[group] [file or dir]` sets user and group to be owner. 

### SELinux
**Security Enhanced Linux**
Some programs are set to only read certain type, which might be an issue with servers.
- check `ls -Z` and check the type
- use `chcon -t [new type] [filename]` 
- change it back with `restorecon [filename]`