# Building an OS/161 Kernel (Short Version)

The OS/161 kernel has been already configured, built, and installed on your CSE4001 Docker container. However, as you modify the OS/161 source code during your assignments, you will want to prepare 
new kernels so that you can test the modified version.

## Building the kernel-level programs: 

Let's start by building the current version of the kernel. We need to work on the linux terminal (i.e., console). Open a Terminal window. To build the kernel, type: 

```shell
cd ~/os161/src/kern/conf
./config DUMBVM
cd ../compile/DUMBVM
bmake depend
bmake
bmake install
```

In this case, the source directory is named `src` and the kernel configuration file is `DUMBVM`. However, these two names may change depending on the assignment. Each assignment will have a different source code directory and a different configuration file. For example, an assignment might have the kernel source files in a directory named `add_system_calls` innstead of `src`, and a configuration file named `ASSIGNMT01` instead of `DUMBVM`, which means that the building instructions need to be changed accordingly. 

## Building the user-level programs (i.e., `userland`): 

To build `userland`, go to the `src/` directory of OS/161 and execute the following commands:

```shell
cd ~/os161/src/
bmake includes
bmake
bmake install
```


## Running the kernel

Once the building process is completed, you can test your kernel:

```shell
cd ~/os161/root
sys161 kernel
```

The kernel will print various messages as it boots. When it has finished booting, it will present you with a command prompt. The output should look something like this:

```
linux028.student[182]% sys161 kernel
sys161: System/161 release 1.99.06, compiled Aug 23 2013 10:23:34

OS/161 base system version 1.99.05
Copyright (c) 2000, 2001, 2002, 2003, 2004, 2005, 2008, 2009
   President and Fellows of Harvard College.  All rights reserved.

Put-your-group-name-here's system version 0 (ASST0 #1)

312k physical memory available
Device probe...
lamebus0 (system main bus)
emu0 at lamebus0
ltrace0 at lamebus0
ltimer0 at lamebus0
beep0 at ltimer0
rtclock0 at ltimer0
lrandom0 at lamebus0
random0 at lrandom0
lhd0 at lamebus0
lhd1 at lamebus0
lser0 at lamebus0
con0 at lser0

cpu0: MIPS r3000
OS/161 kernel [? for menu]:
```
