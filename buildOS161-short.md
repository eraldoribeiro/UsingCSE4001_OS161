# Building an OS/161 Kernel (Short Version)

The OS/161 kernel has been already configured, built, and installed on your CSE4001 Docker container. However, as you modify the OS/161 source code during your assignments, you will want to prepare 
new kernels so that you can test the modified version.

## Building and running the kernel: 

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

Once the building process is completed, you can test your kernel:

```shell
cd ~/os161/root
sys161 kernel
```


