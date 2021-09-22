### Buildroot
Buildroot is a tool that simplifies and automates the process of building a complete Linux system for an embedded system, using cross-compilation.

### Build
To build and use the buildroot stuff, do the following:

1) run 'make menuconfig'
2) select the target architecture and the packages you wish to compile
3) run 'make'
4) wait while it compiles
5) find the kernel, bootloader, root filesystem, etc. in output/images

You do not need to be root to build or run buildroot.  Have fun!

Buildroot comes with a basic configuration for a number of boards. Run
'make list-defconfigs' to view the list of provided configurations.

### Link
homepage
https://buildroot.org/

user manual
https://buildroot.org/downloads/manual/manual.html

If you would like to contribute patches, please read
https://buildroot.org/manual.html#submitting-patches
