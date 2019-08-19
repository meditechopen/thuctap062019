### Linux Boot Process

Understanding the Linux boot and startup processes is important to being able to both configure Linux and to resolving startup issues. 

<img src=https://www.linoxide.com/wp-content/uploads/2013/06/boot-process-chart.jpg>

##### 1. BIOS Initialization

BIOS or the Basic Input Output System is a firmware program that performs a very basic level of interaction with the hardware.
This is the first program that takes control when the computer is switched on.The BIOS performs a test on all the hardware components and peripherals called POST or the “Power On Self Test”. It initializes the required hardware for booting.

After POST executes successfully, the BIOS looks for a boot device from a list of devices. Modern BIOS allow you to configure the order of these devices (sometimes called boot preference) that BIOS checks for booting. These boot devices can either be a floppy drive, CDROM, hard drive, a network interface or other removable media (such as USB flash drive).

The BIOS checks for the boot sector on the bootable device. Boot sector is the first physical sector on the storage device, and contains the code required for booting the machine.

##### 2. The Master Boot Record

In case of hard disks and many other mass storage media, the boot sector is MBR. MBR consists of 512 bytes at the first sector of the hard disk. It is important to note that MBR is not located inside any partition. MBR precedes the first partition. The layout of MBR is as follows:

• First 446 bytes contain bootable code.
• Next 64 bytes contain partition information for 4 partitions (16x4). That is why the hard disks can have only 4 primary partitions as the MBR can store information for 4 partitions only. So if you need more than 4 partitions on the hard disk, one of the primary partition has to be extended, and out of these extended partitions, logical partitions are created.
• The last 2 bytes are for MBR signature, also called magic number. (Thus total of 446 + 64 + 2 = 512 bytes).


| 446 | 16 | 16 | 16 | 16 | 2 |


The first 446 bytes of MBR contains the code that locates the partition to boot from. The rest of the booting process take place from that partition. This partition contains a software program called the 'bootloader' for booting the system.

##### 3. About GRUB

According to gnu.org, “A bootloader is the first software program that runs when a computer
starts”. GRUB or GRand Unified Bootloader is the bootloader program for Linux like operating
systems. There are mainly two versions of Grub is available (Grub version 1 and 2). Now most
linux ditros started using grub version 2. One main feature of grub is that it can be installed
using linux image and no need for running operating system.

GRUB allows you to choose from a list of available operating systems. The different OS’s have
different title in grub.conf. Corresponding to this configuration file, the user at GRUB menu will
be asked to choose from two options: Red Hat Enterprise Linux Server (2.6.18-238.el5), and
Windows XP Pro. 

##### 4. Kernel Initialization

After GRUB stage 2, the location of kernel and necessary modules through initrd are known.
Now the kernel is loaded into memory and initialized. The initrd image is compiled and
mounted into the memory. It serves as a temporary root file system and helps kernel to boot
properly without mounting any root file system. Now that all the drivers are loaded into memory, and kernel has booted, kernel mounts the root filesystem in read only mode, and starts
the first process.

##### 5. The init Proces

The ‘init’ is the first process started by kernel (initialization process). It is the parent of all processes. The PID (Process ID) of init process is always 1. This process persists till the computer halts. It is responsible for the whole state of system. The settings for this process are stored in its configuration file, /etc/inittab (system initialization table). Before diving deeper into the details of this file and proceeding any further with the boot process, let’s discuss runlevels.

##### 6. Runlevels

Runlevel is the state in which a system boots. It can boot in a single user mode, multi-user mode, with networking, and with graphics etc. The following are the default runlevels defined by Linux:

0: Halt or shutdown the system.

1: Single user mode.

2: Multi-user mode, without networking.

3: Full multi user mode, with NFS (typical for servers).

4: Officially not defined; Unused.

5: Full multi user with NFS and graphics (typical for desktops).

6: Reboot.
