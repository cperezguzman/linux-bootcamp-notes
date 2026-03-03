# Context
Technically speaking, Linux is an **Open-Source Operating System**

## The Kernel vs The OS
Linux, for all intents and purposes, is just the kernel which is the core software that acts as a mediator between the computer's hardware (CPU, RAM, storage) and the applications ran on the computer.
* When people say "Linux", they usually mean a **Linux Distribution** (or "Distro") which bundles the kernel with a desktop interface, a web browser, and other tools.
* **Popular Distros**: Debian (which includes Ubuntu), Red Hat, and SUSE are the main family systems

## It's Everywhere
Linux runs the modern world:
* **The Internet**: The vast majority of the world's web servers run on Linux.
* **Android**: Every Android smartphone is built on top of the Linux kernel.
* **Supercomputers**: 100% of the world's top 500 fastest supercomputers run Linux.
* **Smart Devices**: From a smart fridge to flight controls in a rocket, Linux is the go-to choice.

## Why People Like It
Linux stands out from Windows and macOS for three main reasons:
### Open Source
The source code is public, so anyone can inspect and modify it. This creates a massive community of developers constantly fixing bugs.

### Customization
Users can change *anything*. Want a different taskbar ? Change it. Want a system that uses almost no memory ? Build it.

### Cost & Security
Most versions are completely free. Plus, because of how permissions are handled, it is also significantly less "prone" to traditional Windows viruses.

## The Debian Family
The Debian distribution is upstream (smth like "parent to") Ubuntu. It's a pure open source community project and provides by far the largest and most complete software repository to its users of any Linux distribution.

Ubuntu provides a good compromise between long-term stability and ease of use. Since Ubuntu gets most of its packages from Debian's stable branch, it also has access to a very large software repo.

## Key Facts
* The Debian family uses the DKG-based APT package manager to install, update, and remove packages in the system.
* While Ubuntu is built on top of Debian and is GNOME-based under the hood, it differs visually from the interface on standard Debian.

# Introduction
Linux borrows heavily from the well-established family of UNIX OSs. 

Files are stored in a hierarchical filesystem, with the top node of the system being the root or simply "/". Whenever possible, Linux makes its components available via files or objects that look like files. Processes, devices, and network sockets are all represented by file-like objects and can often be worked with using the same utilities used for regular files.

Linux is a fully multitasking (i.e., multiple threads of execution are performed simultaneously), multiuser OS with built-in networking and service processes known as daemons in the UNIX world.

## Linux Terminology
* **Kernel**: The brain of the Linux OS, it controls the hardware and makes the hardware interact with the applications (ex: Linux kernel)
* **Distribution**: Collection of programs combined with a Linux kernel to make up a Linux-based OS (ex: Red Hat Enterprise Linux, Ubuntu, Fedora)
* **Boot Loader**: Program that boots the OS (ex: GRUB and ISOLINUX)
* **Service**: Program that runs as a background process (ex: httpd (Web Server), ftpd (FTP Server), named (Name Server), dhcpd (DHCP Server))
* **Filesystem**: Method for storing and organizing files in Linux (ex: ext3, ext4, FAT, XFS, NTFS, Btrfs)
* **X Window System**: Provides the standard toolkit and protocol to build graphical user interfaces
* **Desktop Interface**: Graphical user interface on top of the OS (ex: GNOME, KDE, Xfce, and Fluxbox)
* **Command Line**: Interface for typing commands on top of the OS
* **Shell**: Interprets the command line input and instructs the OS to perform any necessary tasks and commands. (ex: bash, tcsh, zsh)

## Linux Distributions
A full Linux distribution consists of the kernel plus a number of other software tools for file-related operations, user management, and software package management. Each tool is often its own separate project, with its own developers working to perfect that piece of the system.

It is important to note that the kernel is not an all-or-nothing proposition. For example, RHEL/CentOS has incorporated many of the more recent kernel improvements into their customized older versions, as have Ubuntu, openSUSE, Fedora, etc.

Examples of other essential tools and ingredients provided by distributions include the C/C++ and Clang compilers, the gdb debugger, the core system libraries applications need to link with in order to run, the low-level interface for drawing graphics on the screen, as well as the higher-level desktop environment, and the system for installing and updating the various components, including the kernel itself.

## Services Associated with Distributions
The vast majority of Linux distributions are designed to caterto many different audiences and organizations according to their specific needs and tastes. However, large organizations, such as companies and government institutions, tend to choose the major commercially-supported distributions from Red Hat, SUSE, and Canonical (Ubuntu).

CentOS and CentOS Stream are popular free (as in no cost) alternatives to Red Hat Enterprise Linux (RHEL) and are often used by organizations that are comfortable operating without paid technical support.

The RHEL variants, such as CentOS and AlmaLinux, are designed to be binary-compatible with RHEL; i.e., in most cases, binary software packages will install properly across the distributions.

Ubuntu and Fedora are widely used by developers and are also popular in the educational realm.


# Linux Basics and System Startup
## The Boot Process
The Linux boot process is the procedure for initializing the system. It consists of everything that happens from when the computer is powered on until the user interface is fully operational.

### BIOS - The First Step
These notes will focus on the x86 hardware family, which is the basis of almost all desktop and laptop PCs.

Starting an x86-based Linux system involves a number of steps, the first of which happens right when the computer is powered on: the Basic Input/Output System (BIOS). This initializes the hardware, including the screen and keyboard, and tests the main memory.
This process is also called POST (Power On Self Test).

The BIOS software is stored on a read-only memory (ROM) chip on the motherboard. After this, the remainder of the boot process is controlled by the OS.
(Power On ➡️ BIOS ➡️ Initializes screen and keyboard, tests main memory)

### Master Boot Record (MBR), EFI Partition, and Boot Loader
After POST is completed, system control passes from BIOS to the **boot loader**. 

The boot loader is usually stored on one of the system's storage devices (e.g. hard disk or SSD drive) either in the boot sector (for traditional BIOS/MBR systems) or the EFI partition (for more recent (Unified) Extensible Firmware Interface or EFI/UEFI systems).

Up to this stage, the machine does not access any mass storage media. Then, information on the date, time, and the most important peripherals are loaded from the **CMOS** values (after a technology used for the battery-powered memory store, allowing the system to keep track of the date and time even when it is powered off).

A number of boot loaders exist for Linux; the most common ones are GRUB (for GRand Unified Boot loader), ISOLINUX (for booting from removable media), and DAS U-Boot (for booting on embedded devices/appliances). 

Most Linux boot loaders can present a user interface for choosing alternative options for booting Linux and even other OSs that might be installed. When booting Linux, the boot loader is responsible for loading the kernel image and the initial RAM disk or filesystem (which contains some critical files and device drivers needed to start the system) into memory.

**BIOS BOOT**
BIOS ➡️ MBR ➡️ Boot Loader ➡️ Kernel ➡️ OS
**UEFI BOOT**
UEFI ➡️ EFI (Boot Loader) ➡️ Kernel ➡️ OS

### Boot Loader in Action
The boot loader has two distinct stages:
**1)** For systems using the BIOS/MBR method, the boot loader resides at the first sector of the hard disk, AKA the Master Boot Record (MBR). The size of the MBR is just 512 bytes.

In this stage, the boot loader examines the **partition table** and finds a bootable partition. Once it finds a partition, it then searches for the second stage boot loader (e.g., GRUB) and it loads it into RAM (Random Access Memory).

For systems using the EFI/UEFI method, UEFI firmware reads its Boot Manager data to determine which UEFI application is to be launched and from where (i.e., from which disk and partition the EFI partition can be found). The firmware then launches the UEFI application, (e.g., GRUB) as defined in the boot entry in the firmware's boot manager. This procedure is more complicated but more versatile than the older MBR methods.

The second stage boot loader resides under ```/boot```. A splash screen is displayed, which allows us to choose which OS and/or kernel to boot. After the OS and kernel are selected, the boot loader loads the kernel of the OS into RAM and passes control to it. Kernels are almost always compressed, so the first job they have is to uncompress themselves. After this, the kernel will check and analyze the system hardware and initialize any hardware device drivers built into the kernel.

### The Initial RAM Disk
The **initramfs** filesystem image contains programs and binary files that perform all actions needed to mount the proper root filesystem, including providing the kernel functionality required for the specific filesystem that will be used, and loading the device drivers for mass storage controllers, by taking advantage of the **udev** system (for user device), which is responsible for figuring out which devices are present, locating the device drivers they need to operate properly, and load them. After the root filesystem is found, it is checked for errors and mounted.

The **mount** program instructs the OS that a filesystem is ready for use and associates it with a particular point in the overall hierarchy of the filesystem (the **mount** point). If this is successful, the initramfs is cleared from RAM, and the **init** program on the root filesystem (```/sbin/init```) is executed.

init handles the mounting and pivoting over to the final real root filesystem. If special hardware drivers are needed before the mass storage can be accessed, they must be in the initramfs image.

**initramfs** ⬅️ **Programs, Binary Files** ⬅️ **mount proper root filesystem, providing kernel functionality, locating devices, locating drivers and loading them, checking for errors in root filesystem**
