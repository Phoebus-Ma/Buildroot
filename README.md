### Buildroot
-------------------------
Buildroot is a tool that simplifies and automates the process of building a complete Linux system for an embedded system, using cross-compilation.

### Build
-------------------------
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
-------------------------
[homepage]
(https://buildroot.org/)

[user manual]
(https://buildroot.org/downloads/manual/manual.html)

[contribute patches]
(https://buildroot.org/manual.html#submitting-patches)

### Example
-------------------------
```
$ cd Buildroot
$ ls ./config/qemu_*
./configs/qemu_aarch64_sbsa_defconfig         ./configs/qemu_mips64r6el_malta_defconfig
./configs/qemu_aarch64_virt_defconfig         ./configs/qemu_nios2_10m50_defconfig
./configs/qemu_arm_versatile_defconfig        ./configs/qemu_or1k_defconfig
./configs/qemu_arm_versatile_nommu_defconfig  ./configs/qemu_ppc64_e5500_defconfig
./configs/qemu_arm_vexpress_defconfig         ./configs/qemu_ppc64_pseries_defconfig
./configs/qemu_arm_vexpress_tz_defconfig      ./configs/qemu_ppc64le_pseries_defconfig
./configs/qemu_csky610_virt_defconfig         ./configs/qemu_ppc_e500mc_defconfig
./configs/qemu_csky807_virt_defconfig         ./configs/qemu_ppc_g3beige_defconfig
./configs/qemu_csky810_virt_defconfig         ./configs/qemu_ppc_mac99_defconfig
./configs/qemu_csky860_virt_defconfig         ./configs/qemu_ppc_mpc8544ds_defconfig
./configs/qemu_m68k_mcf5208_defconfig         ./configs/qemu_riscv32_virt_defconfig
./configs/qemu_m68k_q800_defconfig            ./configs/qemu_riscv64_virt_defconfig
./configs/qemu_microblazebe_mmu_defconfig     ./configs/qemu_s390x_defconfig
./configs/qemu_microblazeel_mmu_defconfig     ./configs/qemu_sh4_r2d_defconfig
./configs/qemu_mips32r2_malta_defconfig       ./configs/qemu_sh4eb_r2d_defconfig
./configs/qemu_mips32r2el_malta_defconfig     ./configs/qemu_sparc64_sun4u_defconfig
./configs/qemu_mips32r6_malta_defconfig       ./configs/qemu_sparc_ss10_defconfig
./configs/qemu_mips32r6el_malta_defconfig     ./configs/qemu_x86_64_defconfig
./configs/qemu_mips64_malta_defconfig         ./configs/qemu_x86_defconfig
./configs/qemu_mips64el_malta_defconfig       ./configs/qemu_xtensa_lx60_defconfig
./configs/qemu_mips64r6_malta_defconfig       ./configs/qemu_xtensa_lx60_nommu_defconfig
$ make qemu_x86_64_defconfig
$ make -j4
```

### Running
-------------------------
```
$ cat ./board/qemu/x86_64/readme.txt
Run the emulation with:

  qemu-system-x86_64 -M pc -kernel output/images/bzImage -drive file=output/images/rootfs.ext2,if=virtio,format=raw -append "rootwait root=/dev/vda console=tty1 console=ttyS0" -serial stdio -net nic,model=virtio -net user # qemu_x86_64_defconfig

Optionally add -smp N to emulate a SMP system with N CPUs.

The login prompt will appear in the graphical window.
$
$
$ qemu-system-x86_64 -M pc -kernel output/images/bzImage -drive file=output/images/rootfs.ext2,if=virtio,format=raw -append "rootwait root=/dev/vda console=tty1 console=ttyS0" -serial stdio -net nic,model=virtio -net user
```
