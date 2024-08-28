# Building OS/161 (Detailed version)

In these notes, the directory `src/` contains the kernel source files. For assignments, you will be provided a different version of the source code and the directory name might be different and, as a result, you will need to change the name `src/` to the name of the directory containing the source code for OS/161.

## Kernel-level building steps 

The OS/161 kernel has been already configured, built, and installed on your computer. However, as you modify the OS/161 source code during your assignments, you will want to prepare new kernels so that you can test your changes.

Preparing a kernel involves several steps: configuration, building, and installation:

### Configure

Normally, it is not necessary to re-configure each time you prepare a new kernel. However, there are two exceptions to consider. One exception to this is when you have added new kernel source files or removed kernel source files. In that case, you must edit the kernel configuration file, and reconfigure the kernel before you attempt to build it. The other exception is when you are first starting a new assignment. Kernel configuration is assignment-specific, so you when you start a new assignment you should re-configure before building the kernel for the first time.

The main kernel configuration file is located in the directory `~/os161/src/kern/conf` in a file called `conf.kern`. This file defines various kernel options and devices. Towards the end of `conf.kern` you will find file declarations like this

```
file      thread/spinlock.c
```

for each section of the kernel code, e.g., the thread section or the file system section. If you add a new file to the kernel code, you must add a corresponding file declaration in `kern.conf` and then reconfigure the kernel. Once you have changed `kern.conf`, you re-configure the kernel by running

```
./config ASSTX
```

in the same directory. Here, the `ASSTX` parameter indicates which assignment you are working on. For the first assignment, use `ASST1`, for the second assignment, use `ASST2`, and so on.

### Build

Kernels should always be built in the kernel build directory, which is `~/os161/src/kern/compile/ASSTX` for the X-th assignment. (This directory is created when you configure the kernel.) To build a new kernel, issue the following commands in the kernel build directory:

```shell
bmake depend
bmake
```

If your kernel builds successfully, you should see a line similar to this near the end of the output from bmake:

```
*** This is ASST1 build #5 ***
```

Each new version of your kernel gets assigned a new "build number" when it gets made. Take note of this number - you'll see why when we talk about running the kernel.

### Install
If everything goes smoothly with the kernel build, you may then install the new kernel. Do this by running the command

```
bmake install
```

in the kernel build directory. This will put a copy of your newly-built kernel in the directory `~/os161/root` in a file called `kernel-ASSTX`. It will also set the symbolic link kernel (also in the `~/os161/root` directory) to refer to the newly-installed kernel.



## Building `Userland`: the OS/161 User-Level Programs

OS/161 comes with a variety of user-level programs that can run on top of the OS/161 kernel. These include standard UNIX-style utility programs, like `ls` and `cat`, and a variety of test programs. The source files for the utility programs are located in `~/os161/src/userland/{bin,sbin}`. The source files for the test programs are located in `~/os161/src/userland/testbin`.

Note that many user programs will not run with OS/161 as it is initially distributed, since many *system calls* are not implemented in this version of the operating system.

User-level programs are built and installed from the directory `~/os161/src/`. To build and install all of the user-level programs, simply run:

```shell
bmake
bmake install
```

User-level programs are installed under `~/os161/root/` in the `bin/`, `sbin/`, and `testbin/` directories.

### Running OS/161

The OS/161 kernel, as well as OS/161 user-level programs, run on the sys/161 machine simulator. To run your OS/161 kernel, you start up the simulator and you pass it the name of the file that contains your kernel binary.

When you run OS/161, you should be in the runtime root directory, which is `~/os161/root`. From the runtime root directory, use the command

```shell
sys161 kernel-ASSTX
```

or simply:

```shell
sys161 kernel
```

Both do the same thing, because `bmake install` makes `kernel` a symbolic link to `kernel-ASSTX`.

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

You can type `q` at the command prompt to cause the kernel to shut down. Typing `?` will show you other commands. Note that some menu commands will not work properly at the beginning, because they depend on kernel functionality that you have not yet implemented. One particular thing that you can do from the kernel menu is to launch an initial user-level program, such as a command shell or some test program. (The `p` and `s` commands do this. For more information, see the on-line help for the operations menu.) Again, most of these programs will not work initially because they depend on unimplemented kernel functionality.

One thing you should notice, near the beginning of the kernel's boot messages, is the line:

```
Put-your-group-name-here's system version 0 (ASST1 #5)
```

What the kernel is doing here is printing its "build number" - the same number that was displayed in the bmake output when the kernel was built. This is a great way for you to ensure that the kernel that you are running is actually the kernel that you built, and not some earlier version of your kernel.




