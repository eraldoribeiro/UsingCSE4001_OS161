# Debugging an OS/161 Kernel using GDB

To debug OS/161, you should use the OS161 version of GDB, which is called `os161-gdb`. This version of GDB has been configured for the MIPS architecture and has been patched to be able to talk to System/161. The difference between debugging a regular program and debugging an OS/161 kernel is that the kernel is running in a machine simulator. You want to debug the kernel; running the debugger on the machine simulator is not very illuminating and we hope it will not be necessary. If you were to issue the command:

```
os161-gdb sys161
```

from the runtime root directory you would be attempting to debug the simulator (i.e., `sys161`). This will not work, because the simulator is not compiled for MIPS. If you were instead to issue the command

```
os161-gdb kernel
```

to try to debug the kernel, you would find that this also does not work, because the kernel has to be run on System/161.

Instead, what you need to do is start your kernel running in sys/161 and then run `os161-gdb` and tell it to attach to sys161's debugger port. This is easiest to do using two windows, one to run sys/161 in and one to run GDB in. Note that you must be logged in to the same machine in both windows. If you are logged in to `mef-linux018` in one window and `mef-linux002` in another, this will not work. You can use the hostname command in a window to check which machine that window's commands are running on.

To debug, first start OS/161 on sys/161 in one of the windows.

```
sys161 -w kernel
```

Make sure that you are in the runtime root directory when you do this. The `-w` option tells sys/161 to wait for a debugger connection. You should see output that looks something like this:

```
$ sys161 -w kernel
sys161: System/161 release 1.99.05, compiled Feb  4 2011 15:14:48
sys161: Waiting for debugger connection...
```

At this point, sys161 is paused, waiting for a connection from the debugger.

Next, in the other window (your debug window), move into the runtime root directory - the same directory in which you are running sys161 - and run `os161-gdb` on the kernel and tell GDB to connect to sys/161:

```
os161-gdb kernel
```

You should see some output like this from the debugger:

```
$ os161-gdb kernel
GNU gdb 6.6
Copyright (C) 2006 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
Type "show copying" to see the conditions.
There is absolutely no warranty for GDB.  Type "show warranty" for details.
This GDB was configured as "--host=x86_64-unknown-linux-gnu --target=mips-harvard-os161"...
(gdb)
```

The (gdb) is the debugger's command prompt. The debugger is now stopped, waiting for you to enter a command. You want to give it the following commands:

```
(gdb> dir ../src/kern/compile/ASSTX
(gdb) target remote unix:.sockets/gdb
```

The first command just tells gdb where to find the .o files for your kernel. The second command tells gdb to connect to the waiting sys161 program that is running in your other window. (Don't forget the "." before sockets/gdb.) You should see output something like this in the debugger window:

```
(gdb) dir ../src/kern/compile/ASST0
Source directories searched: /u5/kmsalem/cs350-os161/root/../src/kern/compile/ASST0:$cdir:$cwd
(gdb) target remote unix:.sockets/gdb
Remote debugging using unix:.sockets/gdb
__start () at ../../arch/mips/mips/start.S:24
24	   addiu sp, sp, -20
Current language:  auto; currently asm
(gdb)
```

and you should see a message like sys161: New debugger connection in the sys161 window.

At this point, your kernel is running under control of the debugger. Your kernel is waiting to start its execution (in the assembly language function `start.S`) as soon as the debugger allows it to proceed. You may now issue any gdb commands that you would like to, e.g., you may set breakpoints to force kernel execution to halt wherever you want. When you are ready to go, you can use gdb's continue command to allow the kernel's execution to proceed:

```
(gdb) c
```

When you do this, the kernel should start running in the other window. Unless you've set breakpoints, the kernel should print its usual boot messages and eventually provide you with the kernel command prompt.

For more information about using GDB, see [Debugging with GDB](http://www.student.cs.uwaterloo.ca/~cs350/common/gdb.html).

