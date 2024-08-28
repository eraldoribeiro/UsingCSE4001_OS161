# Building OS/161 (Detailed version)

In these notes, the directory `src/` contains the kernel source files. For assignments, you will be provided a different version of the source code and the directory name might be different and, as a result, you will need to change the name `src/` to the name of the directory containing the source code for OS/161.

## Kernel-level building steps 

The OS/161 kernel has been already configured, built, and installed on your computer. However, as you modify the OS/161 source code during your assignments, you will want to prepare new kernels so that you can test your changes.

Preparing a kernel involves several steps: configuration, building, and installation:

### `configure`:

Normally, it is not necessary to re-configure each time you prepare a new kernel. However, there are two exceptions to consider. One exception to this is when you have added new kernel source files or removed kernel source files. In that case, you must edit the kernel configuration file, and reconfigure the kernel before you attempt to build it. The other exception is when you are first starting a new assignment. Kernel configuration is assignment-specific, so you when you start a new assignment you should re-configure before building the kernel for the first time.

The main kernel configuration file is located in the directory `~/os161/src/kern/conf` in a file called `conf.kern`. This file defines various kernel options and devices. Towards the end of conf.kern you will find file declarations like this

```
file      thread/spinlock.c
```

for each section of the kernel code, e.g., the thread section or the file system section. If you add a new file to the kernel code, you must add a corresponding file declaration in kern.conf and then reconfigure the kernel. Once you have changed kern.conf, you re-configure the kernel by running

```
./config ASSTX
```

in the same directory. Here, the `ASSTX` parameter indicates which assignment you are working on. For the first assignment, use `ASST1`, for the second assignment, use `ASST2`, and so on.
build:
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

### `install`:

If everything goes smoothly with the kernel build, you may then install the new kernel. Do this by running the command

```
bmake install
```

in the kernel build directory. This will put a copy of your newly-built kernel in the directory `~/os161/root` in a file called `kernel-ASSTX`. It will also set the symbolic link kernel (also in the `~/os161/root` directory) to refer to the newly-installed kernel.


