# Processes and Resources

## Background
Process is a program loaded into memory for the CPU to execute. Within the process there might be different pieces of execution, those are threads. The prcocess switches between the different threads.
Multi-core CPUs = more CPUs on the chip to avoid the problem of getting smaller and electric issues.
HyperThreading in a CPU is that the CPU tells the hardware it has more than one core so the computer can send processes to the CPU (the physical core one and the virtual ones) and then the chip can switch through them cores (which have their bit of memory) very fast. This way the OS doesn't have to keep track, it's handled by the CPU.
A 4-core CPU with hyperthreading can tell the OS it has 8 cores.

#### Race Conditions!
ATM machine, 100$ withdrawl. What happens if at the same time you take money you get a deposit of 200$: what if they both read at the same time? one substracts and one adds? do you have 200$ or 300$ xD

## Processes
Use `ps` to see processes running. Use `fg` and `bg` to move processes to foreground or background (ctrl+c to kill then).

A background process starts by adding '&' at the end of it.

Can also use `jobs` to check what's running.
To terminate a process use `kill [pid]` command. Use `-9` to fully kill it (smaller number gives stronger die signals). 

The `signal` command also can do different system signals.

To avoid processes dying when you close the terminal for example use `nohup`. Can still be found in `ps` and `jobs`.

## System processes
To see system processes use `ps aux` to make it nicer add `| less` to the command. 
`top` provides a different type of processes list. use <- -> to sort the list. you can press k to kill a process from inside top.

## proc/ directory
Interface directory to the Kernel. There are lots of empty files.
_sysctl.conf_ file for boot options and `sysctl` command.

## hard drive space
use `df -h` for space info
use `du -h [directory]` for directories