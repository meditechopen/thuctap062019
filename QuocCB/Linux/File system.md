#### Files and File System




For convenience, the Linux file system is usually thought of in a tree structure. On a standard Linux system
you will find the layout generally follows the scheme presented below.

<img src=https://i.imgur.com/oD9Hkdu.png>

The tree of the file system starts at the trunk or slash, indicated by a forward slash (/). This directory,
containing all underlying directories and files, is also called the root directory or "the root" of the file system.

**Subdirectories of root directory**

|**Directory**|**Content**|
|-------------|-------------|
|/bin|Common programs, shared by the system, the system administrator and the users|
|/boot|The startup files and the kernel, vmlinuz. In some recent distributions also grub data. Grub is the GRand Unified Boot loader and is an attempt to get rid of the many different boot-loaders we know today.|
|/dev|Contains references to all the CPU peripheral hardware, which are represented as files with special properties.|
|/etc|Most important system configuration files are in /etc, this directory contains data similar to those in the Control Panel in Windows|
|/home|Home directories of the common users.|
|/initrd|(on some distributions) Information for booting. Do not remove!|
|/lib|Library files, includes files for all kinds of programs needed by the system and the users.|
|/lost+found|Every partition has a lost+found in its upper directory. Files that were saved during failures are here.|
|/misc|For miscellaneous purposes.|
|/mnt|Standard mount point for external file systems, e.g. a CD-ROM or a digital camera.|
|/net|Standard mount point for entire remote file systems|
|/opt|Typically contains extra and third party software.|
|/proc|A virtual file system containing information about system resources. More information about the meaning of the files in proc is obtained by entering the command man proc in a terminal window. The file proc.txt discusses the virtual file system in detail.|
|/root|The administrative user's home directory. Mind the difference between /, the root directory and /root, the home directory of the root user.|
|/sbin|Programs for use by the system and the system administrator.|
|/tmp|Temporary space for use by the system, cleaned upon reboot, so don't use this for saving any work!|
|/usr|Programs, libraries, documentation etc. for all user-related programs.|
|/var|Storage for all variable files and temporary files created by users, such as log files, the mail queue, the print spooler area, space for temporary storage of files downloaded from the Internet, or to keep an image of a CD before burning it.|

##### The most important files and directories

**1. The kernel.**

The kernel is the heart of the system. It manages the communication between the underlying hardware and the
peripherals. The kernel also makes sure that processes and daemons (server processes) are started and stopped
at the exact right times. The kernel has a lot of other important tasks, so many that there is a special
kernel-development mailing list on this subject only, where huge amounts of information are shared. It would
lead us too far to discuss the kernel in detail. For now it suffices to know that the kernel is the most important file on the system.

**
