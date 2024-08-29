# The OS/161 Source Tree
 

## Understanding the OS/161 source tree


Most of the OS/161 sources are C source (`.c`) and header (`.h`) files. Your kernel does also contain a bit of assembly code (`.S`) files. You will not need to understand or modify the assembly code, but it does contain some fairly interesting pieces of code executed during boot and during context switches. So you may want to take a look at it at some point. The assembly code is also extremely well commented.

## The Top of the Source Directory
Your OS/161 source directory contains the following files:

- `CHANGES`: describes the evolution of OS/161 and changes in previous versions.
- `configure`: the top-level configuration script that you ran previously.
- `Makefile`: the top-level `Makefile` used to build the user space binaries.

The source directory contains the following subdirectories:

`common/`: code used both by the kernel and user programs, mostly standard C library functions.
design/`: contains design documents describing several OS/161 components.
kern/: the kernel source code, and the subdirectory where you will spend most of your time.
man/: the OS/161 man pages appear here. The man pages document (or specify) every program, every function in the C library, and every system call. The man pages are HTML and can be read with any browser.
mk/: fragments of Makefiles used to build the system.
userland/: user space libraries and program code.
If you have previously configured and built in this directory there are also some additional files and directories that have been created, such as defs.mk and build/.

User Land
In the userland/ source subdirectory, you will find:

bin/: all the utilities that are typically found in /bin/—cat, cp, ls, etc. Programs in /bin/ are considered fundamental utilities that the system needs to run.
include/: these are the include files that you would typically find in /usr/include (in our case, a subset of them). These are user include files, not kernel include files.
lib/: library code lives here. We have only two libraries: libc, the C standard library, and hostcompat, which is for recompiling OS/161 programs for the host UNIX system. There is also a crt0 directory, which contains the startup code for user programs.
sbin/: this is the source code for the utilities typically found in /sbin on a typical UNIX installation. In our case, there are some utilities that let you halt the machine, power it off, and reboot it, among other things.
testbin/: these are pieces of test code that we will use to test and grade your assignments.
You don’t need to understand the files in userland/bin/, userland/sbin/, and userland/testbin/ now, but you certainly will later on. Eventually, you will want to modify these or write your own utilities and these are good models. Similarly, you need not read and understand everything in userland/lib and userland/include but you should know enough about what’s there to be able to get around the source tree easily. The rest of our code walk-through is going to focus on kern/.

Kernel Sources
Now let’s navigate to the kern/ source subdirectory. Once again, there is aMakefile. This Makefile installs header files but does not build anything. In addition, we have more subdirectories for each component of the kernel as well as some utility directories and configuration files.

kern/arch
This is where architecture-specific code goes. By architecture-specific, we mean the code that differs depending on the hardware platform on which you’re running. There are two directories here: mips which contains code specific to the MIPS processor and sys161 which contains code specific to the System/161 simulator.

kern/arch/mips/conf/conf.arch: this file tells the kernel configuration script where to find the machine-specific, low-level functions it needs (throughout kern/arch/mips/).
kern/arch/mips/include/: this folder and its subdirectories include files for the machine-specific constants and functions.
kern/arch/mips/: The other directories contain source files for the machine-dependent code that the kernel needs to run. Most of this code is quite low-level.
kern/arch/sys161/conf/conf.arch: Similar to mips/conf/conf.arch.
kern/arch/sys161/include: These files are include files for the System/161-specific hardware, constants, and functions.
kern/compile/
This is where you build kernels. In the compile directory, you will find one subdirectory for each kernel configuration target you have used you want to build. For example, if you configure your kernel with the DUMBVM configuration to turn on dumbvm, a DUMBVM subdirectory will be created in kern/compile where you can compile your dumbvm kernel. This directory and build organization is typical of UNIX installations and is not universal across all operating systems.

kern/conf/config: is the script that takes a configuration file, like GENERIC, and creates the corresponding build directory.
kern/test/
This directory contains kernel tests that evaluate multiple parts of your system. Some of these will work right away (km1, km2, sy1), others will not (sy2, sy3), and others you will have to write (sy5). You are more than welcome—encouraged even—to add your own kernel tests. However, please note that during automated tests we will replace the contents of this directory to ensure that your kernel runs the right tests.

kern/dev/
This is where all the low level device management code is stored. Unless you are really interested, you can safely ignore most of this directory.

kern/include/
These are the include files that the kernel needs. The kern subdirectory contains include files that are visible not only to the operating system itself, but also to user programs. Consider why it’s named "kern" and where the files end up when installed.

kern/lib/
These contain library code used throughout the kernel: arrays, kernel printf, etc.

kern/main/
This is where the kernel is initialized and where the kernel main function and menu are implemented.

kern/thread/
This directory contains the code implementing the thread abstraction and synchronization primitives.

kern/synchprobs/
This is the directory that contains the starter code for synchronization tasks.

kern/syscall/
This is where you will add code to create and manage user level processes. As it stands now, OS/161 runs only kernel threads—there is no support for user level code. (Try running the shell from the OS/161 menu and see what happens.)

kern/vm/
This directory is also fairly vacant. This is the place where you would implement most of the code for virtual memory management.

kern/vfs/
The file system implementation has two directories which we’ll present in turn. kern/vfs is the file system independent layer—vfs stands for virtual file system. It establishes a framework into which you can add new file systems easily. You will want to go look at vfs.h and vnode.h before looking at this directory.

kern/fs/
This is where the actual file system implementations go. The subdirectory sfscontains the implementation of the simple file system.
