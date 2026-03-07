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

### Text-Mode Login
Near the end of the boot process, **init** starts a number of text-mode login prompts. These enable the user to type their username, followed by a password, and to eventually get a command shell. However, if you are running a system with a graphical login interface, you will not see these at first.

The terminals which run the command shells can be accessed using the **ALT** key plus a **function** key. Most distributions start six text terminals and one graphics terminal starting with **F1** or **F2**. Within a graphical environment, switching to a text console requires pressing **CTRL-ALT** + the appropriate function key (with **F7** or **F1** leading to the GUI).

Usually, the default command shell is **bash** (the GNU Bourne Again Shell), but there are a number of other advanced command shells available. The shell prints a text prompt, indicating it is ready to accept commands; after the user types the command and presses **Enter**, the command is executed, and another prompt is displayed after the command is done.

**init folder** ➡️ **Username and Password Input** ➡️ **Command Shell**

## Kernel, init, and Services
### The Linux Kernel
The boot loader loads both the **kernel** and an initial RAM-based file system (initramfs) into memory, so it can be used directly by the kernel.

When the kernel is loaded in RAM, it immediately initializes and configures the computer's memory and also configures all the hardware attached to the system. This includes all processors, I/O subsystems, storage devices, etc. The kernel also loads some necessary user space applications.

### /sbin/init and Services
Once the kernel has set up all its hardware and mounted the root filesystem, the kernel runs ```/sbin/init```. This then becomes the initial process, which then starts other processes to get the system running. Most other processes on the system trace their origin ultimately to **init**; exceptions include the so-called kernel processes. These are started by the kernel directly, and their job is to manage internal OS details.

Besides starting the system, **init** is responsible for keeping the system running and for shutting it down cleanly. One of its responsibilities is to act when necessary as a manager for all-none kernel processes; it cleans up after them upon completion, and restarts user login services as needed when users log in and out, and does the same for other background system services.

Traditionally, this process startup was done using conventions that date back to the 1980s and the System V variety of UNIX. This serial process (called **SysVinit**) had the system pass through a sequence of **runlevels** containing collections of scripts that start up and stop services. Each runlevel supported a different mode of running the system. Within each runlevel, individual services could be set to run, or to be shut down if running.

However, all major distributions have moved away from this sequential method of system initialization, although they usually can emulate many System V utilities for compatibility purposes.

**Kernel files** ➡️ **/sbin/init folder** ➡️ **Start other processes to launch the full system**

### Startup Alternatives
**SysVinit** viewed things as a serial process, divided into a series of sequential stages. Each stage required completion before the next could proceed. Thus, startup did not easily take advantage of the ***parallel processing*** that could be done with the multiple processors or cores found on modern systems.

Furthermore, starting up and rebooting were seen as relatively rare events; exactly how long they took was not considered important. This is no longer the case, especially with mobile devices and embedded Linux systems. Some modern methods (e.g., the use of containers) can require almost instantaneous startup times. Thus, systems now require methods with faster and enhanced capabilities. Finally, the older methods required rather complicated startup scripts, which were difficult to keep universal across distribution versions, kernel versions, architectures, and types of systems. The two main alternatives developed were:
**Upstart**
* Developed by Ubuntu and first included in 2006
* Adopted in Fedora 9 (in 2008) and in RHEL 6 and its clones
**systemd**
* Adopted first by Fedora (in 2011)
* Adopted by RHEL 7 and SUSE
* Replaced Upstart in Ubuntu 16.04

While the migration to **systemd** was rather controversial, it has been adopted by all major distributions, and so the older System V method or Upstart will not be discussed.

### systemd Features
Systems with **systemd** start up faster than those with **init** methods. This is largely because it replaces a serialized set of steps with aggressive parallelization techniques, which permits multiple services to be initialized simultaneously.

Complicated startup shell scripts are replaced with simpler configuration files, which enumerate what has to be done before a service is started, how to execute service startup, and what conditions the service should indicate have been accomplished when startup is finished. One thing to note is that ```/sbin/init``` now just points to ```/lib/systemd/systemd```; i.e., **systemd** takes over the **init** process.

One **systemd** command (```systemctl```) is used for most basic tasks. While we have not yet talked about working at the command line, here is a brief listing of its use:
* Starting, stopping, restarting a service (using **httpd**, the Apache web server, as an example) on a currently running system:
  ```bash
  $ sudo systemctl start|stop|restart httpd.service
  ```
* Enabling or disabling a system service from starting up at system boot:
  ```bash
  $ sudo systemctl enable|disable httpd.service
  ```
* Checking on the status of a service:
  ```bash
  $ sudo systemctl status httpd.service
  ```

In most cases, the ```.service``` can be omitted. There are many technical differences with older methods that lie beyond the scope of this discussion.

## Linux Filesystem Basics
### Linux Filesystems
Linux Filesystems
Libraries separate books and other media into multiple sections; this organization will depend on the subject matter, audience, media type, and frequency of retrieval. The same concept applies to a filesystem, which is the embodiment of a method of storing and organizing arbitrary collections of data in a human-usable form.

Different types of filesystems supported by Linux:
* Conventional disk filesystems: ext3, ext4, XFS, Btrfs, JFS, NTFS, vfat, exfat, etc.
* Flash storage filesystems: ubifs, jffs2, yaffs, etc.
* Database filesystems
* Special purpose filesystems: procfs, sysfs, tmpfs, squashfs, debugfs, fuse, etc.

This section will describe the standard filesystem layout shared by most Linux distributions.

### Partitions and Filesystems
A partition is a  dedicated subsection of physical storage media.  Historically this meant a physically contiguous portion of a hard disk; today’s storage devices can be more complicated, but we still think of a partition as a fixed area to be treated as a whole.

A filesystem is just a method of storing and accessing files.

One can think of a partition as a container in which a filesystem resides. However, in some circumstances, a filesystem can span more than one partition if one uses **symbolic links**, which will be discussed in greater detail later.

| | Windows | Linux |
| :---: | :---: | :---: |
| Partition | Disk1 | ```/dev/sda1``` |
| Filesystem type | NTFS/VFAT | EXT3/EXT4/XFS/BTRFS... |
| Mounting parameters | DriveLetter | MountPoint |
| Base folder (where OS is stored) | C:\ | / |

### The Filesystem Hierarchy Standard
Linux systems store their important files according to a standard layout: the Filesystem Hierarchy Standard (FHS), which has long been maintained by the Linux Foundation.

Linux uses the '/' character to separate paths (as is UNIX unlike Windows, which uses '\') and does not have drive letters. Multiple drivers and/or partitions are mounted as directories in the single filesystem. Removable media such as USB drives and CDs, and DVDs wil show up as mounted at ```/run/media/yourusername/disklabel``` for recent Linux systems or under ```/media``` for older distributions. 

Ex:
If the username is **student**, a USB pen drived labeled FEDORA might end up being found at ```/run/media/student/FEDORA```, and a file ```README.txt``` on that disc would be at ```/run/media/student/FEDORA/README.txt```
| Directory | What it's for |
| :---: | :---: |
| ```/bin/```   | Essential user command binaries |
| ```/boot/```  | Static files of the boot loader |
| ```/dev/```   | Device files                    |
| ```/etc/```   | Host-specific system configuration (Required directories: opt, x11, sgml, xml) |
| ```/home/```  | User home directories |
| ```/lib/```   | Essential shared libraries and kernel modules |
| ```/media/``` | Mount point for removable media |
| ```/mnt/```   | Moint point for a temporarily mounted filesystems |
| ```/opt/```   | Add-on application software packages |
| ```/sbin/```  | System binaries |
| ```/srv/```   | Data for services provided by this system |
| ```/tmp/```   | Temporary files |
| ```/usr/```   | (Multi-)User utilities and applications (Secondary Hierarchy) (Required directories: bin, include, lib, local, sbin, share |
| ```/var/```   | Variable files |
| ```/root/```  | Home directory for the roor user |
| ```/proc```   | Virtual filesystem documenting kernel and process status as text files |

### More About the Filesystem Hierarchy Standard
All Linux filesystem names are case-sensitive, so ```/boot```, ```/Boot```, and ```/BOOT``` represent three different directories (folders). 

Many distributions distinguish between core utilities needed for proper system operation and other programs, and place the latter in directories under ```/usr``` directory in the diagram from the previous page and compare the subdirectories with those that exist directly under the system root directory (```/```).

### Viewing the Filesystem Hierarchy from the Graphical Interface
[WATCH VIDEO AND TAKE NOTES] (Linux Filesystem Basics, last part)

# Graphical Interface
## Graphical Desktop
A user can either use a Command Line Interface (CLI) or a Graphical User Interface (GUI) when using Linux. 

To work in the CLI, it's important to remember which programs and commands are used to perform tasks, and how to quickly and accurately obtain more information about their use and options. Comparatively, using the GUI is often quick and easy, allowing the user to interact with the system through graphical icons and screens. 

For repetitive tasks, the CLI is often more efficient, while the GUI is easier to navigate if you do not remember all the details or do something only rarely.

### X Window System
Loading the graphical desktop is one of the final steps in the boot process of a Linux desktop. Historically, this was known as the X Windows System, often just called X.

A service called the **Display Manager** keeps track of the displays being provided and loads the X server (so-called, because it provides graphical services to applications, sometimes called X clients). The display manager also handles graphical logins and starts the appropriate desktop environment after a user logs in.

X is an old software (dating back to mid-1980s), as such, it has certain deficiencies on modern systems (e.g., with security), as it has been stretched rather far from its original purposes. A newer system, known as Wayland, is gradually superseding X and is the default display system for Fedora, RHEL, and other recent distributions.

For the most part, it looks just like X to the user, although under the hood it is quite different.

### More About the Graphical Desktop
A desktop environment consists of a session manager, which starts and maintains the components of the graphical session, and the window manager, which controls the placement and movement of windows, window title-bars, and controls.

Although these can be mixed, generally a set of utilities, session manager, and window manager are used together as a unit, and together provide a seamless desktop environment.

If the display manager is not started by default in the default runlevel, the user can start the graphical desktop a different way, after logging on to a text-mode console, by running ```startx``` from the command line. Or, the user can start the display manager (gdm, kdm, xdm, etc.) manually from the command line. This differs from running ```startx``` as the display managers will project a sign in screen.

### GUI Startup
When installing a desktop environment, the display manager starts at the end of the boot process. It is responsible for starting the graphics system, logging in the user, and starting the user's desktop environment. 

The default display manager for GNOME is called **gdm**. Another popular display manager is **kdm**, associated with KDE.

### GNOME Desktop Environment
GNOME is a popular desktop environment with an easy-to-use graphical user interface. It is bundled as the default desktop environment for most LINUX distributions, including Red Hat Enterprise Linux (RHEL), Fedora, CentOS, SUSE Linux Enterprise, Ubuntu, and Debian.

GNOME has menu-based navigation and is sometimes an easy transition to accomplish for Windows users. However, the look and feel can be quite different across distributions, even if they are all using GNOME.

Another common desktop environment very important in the history of Linux and also widely used is KDE, which has often been used in conjuction with SUSE and openSUSE. Other alternatives for a desktop environment include Unity (present on older Ubuntu but still based on GNOME), XFCE, and LXDE. 

As previously mentioned, most desktop environments follow a similar structure to GNOME, and we will restrict ourselves mostly to it to keep things less complex.

### System Startup and Logging In and Out
[WATCH VIDEO AND TAKE NOTES]

### Graphical Desktop Background
Each Linux distribution comes with its own set of desktop backrounds. You can change the default by choosing a new wallpaper or selecting a custom picture to be set as the desktop background. If you do not want to use an image as the background, you can select a color to be displayed on the desktop instead.

In addition, you can also change the desktop theme, which changes the look and feel of the Linux system. The theme also defines the appearance of application windows.

### Customizing the Desktop Background
To change the background, you can right-click anywhere on the desktop and choose _Change Background_

### gnome-tweaks
Most common settings, both personal and system-wide, are to be found by clicking in the upper right=-hand corner, on either a gear or other obvious icon, depending on your Linux distribution.

However, there are many settings which many users would like to modify which are not thereby accessible; the default settings utility is unfortunately rather limited in modern GNOME-based distributions. Unfortunately, the quest for simplicity has actually made it difficult to adapt your system to your tastes and needs.

Fortunately, there is a standard utility, **gnome-tweaks**, which exposes many more setting options. It also permits you to easily install extensions by external parties. Not all Linux distributions install this tool by default, but it is always available (older distributions used the name **gnome-tweak-tool**). You may have to run it by hitting ```Alt-F2``` and then typing in the name.

Some recent distributions have taken most of the functionality out of this tool and placed it in a new one called **gnome-extensions-app**.

### Changing the Theme
The visual appearance of applications (the buttons, scroll bars, widgets, and other graphical components) are controlled by a **theme**. GNOME comes with a set of different themes which can change the way your applications look.

## Session Management
### Locking the Screen
It is a good idea to lock the screen to prevent other people from accessing the computer.

_**NOTE:** This does not suspend the computer; all the applications and processes continue to run while the screen is locked._ 

Two ways to lock the screen:
* Using the graphical interface
  Clicking the upper-right corner of the desktop, and then clicking the lock icon.
* Using the keyboard shortcut ```SUPER-L``` (or ```SUPER-Escape```)
  (The ```SUPER``` key is also known as the ```Windows``` key).

The keyboard lock shortcut can be modified by altering keyboard settings.

### Switching Users
Linux is a true multi-user OS, allowing more than one user to be simutlaneously logged in.
If more than one person uses the system, each person must have their own user account and password.

## Basic Operations
### File Manager
Each distribution implements the **Nautilus** (**File Manager**) utility, which is used to navigate the file system.

It can locate files and, when a file is clicked upon, either it will run if it is a program, or an associated application will be launched using the file as data. This is completely familiar to anyone who has used other OSs.

### Home Directories
By default, files the user saves will be placed in a directory tree starting at the ```/home``` directory. Account creation, whether during system installation or at a later time, when a new user is added, also induces default directories to be created under the user's ```Home``` directory, such as ```Documents```, ```Desktop```, and ```Downloads```.

### Viewing Files
The File Manager allows the user to view files and directories in more than one way.

The user can switch between the Icons and List formats, either by clicking the familiar icons in the top bar, or pressing ```CTRL-1``` or ```CTRL-2```  respectively.

Another useful option is to show _hidden files_ (sometimes imprecisely called system files), which are usually configuration files that are hidden by default and whose name starts with a dot. To show hidden files, select _Show Hidden Files_ from the menu or press ```CTRL-H```.

### Searching for Files
The File Manager includes a search tool inside the file browser window.
* Click _Search_ in the toolbar (to bring up a text box)
* Enter the key word in the text box. This causes the system to perform a recursive search from the current directory for any file or directory which contains a part of this keyword.

To open the _File Manager_ from the command line, on most systems type ```nautilus```.

The shortcut key to get to the search text box is ```CTRL-F```. To exit the search box view, click the _Search_ button or ```CTRL-F``` again.

Another quick way to access a specific directory is to press ```CTRL-L```, which will give the user a _Location_ text box to type in a path to a directory.

### Editing a File
The default text editor in GNOME is **gedit**. Although **gedit** is designed as a general-purpose text editor, it offers additional features spell-checking, highlighting, file listings, and statistics.

### Removing a File
Deleting a file in Nautilus will automatically move the deleted files to the ```.local/share/Trash/files/``` directory (a trash can of sorts) under the user's home directory. There are several ways to delete files and directories using Nautilus.
1. Select all the files and directories that are to be deleted.
2. Press ```CTRL-Delete``` on your keyboard, or right-click the file.
3. Select _Move to Trash_.

To _permanently_ delete a file:
1. On the left panel inside a Nautilus file browser, right-click on the ```Trash``` directory.
2. Select _Empty Trash_.

Alternatively, select the file or directory and press ```Shift-Delete```.

As a precaution, the _Home_ directory should never be deleted, as doing so will most likely erase all the GNOME configuration files and possibly prevent the user from logging in. Many personal system and program configurations are stored under the user's home directory.

# System Configuration from the Graphical Interface
## System, Diplay, Date and Time Settings
### gnome-tweaks
A lot of personalized configuration settings do not appear on the settings menus. Instead, the user has to launch a tool called either **gnome-tweaks** (or **gnome-tweaks-tool** on older Linux distros). The user can launch the program by pressing ```Alt-F2``` and typing in the command.

Important things that can be done with this tool include selecting a **theme**, configuring **gnome-tweaks**; extensions now have to be configured using a new app called **gnome-extensions-app**. 

### Setting Resolution and Configuring Multiple Screens
The user can change the screen resolution using the _Displays_ panel. The switch to the new resolution will be effective when the user clicks _Apply_. 

In most cases, the configuration for multiple displays is set up automatically as one big screen spanning all monitors, using a reasonable guess for screen layout. If the screen layout is not as desired, a check box can turn on mirrored mode, where the display is seen on all monitors. Clicking on a particular monitor images lets you configure the resolution of each one, and whether they make one big screen, or mirror the same video, etc.

_**NOTE:** The user can ascertain their current resolution by typing at the command line:_
```bash
student:/temp> $ xdpyinfo | grep dim
```

### Date and Time Settings
By default, Linux always uses Coordinated Universal Time (UTC) for its own internal timekeeping. Displayed or stored time values rely on the system time zone setting to get the proper time. UTC is similar to, but more accurate than, Greenwich Mean Time (GMT).

### Network Time Protocol
The Network Time Protocol (NTP) is the most popular and reliable protocol for setting the local time by consulting established Internet servers. 

Linux distros always come with a working NTP setup, which refers to specific time servers run or relied on by the distros. This means that no setup, beyond "on" or "off", is generally required for network time synchronization.

## Network Manager
### Network Configuration
All Linux distros have network configuration files, but file formats and locations can differ from one distro to another. Hand editing of these files can handle quite complicated setups, but is not very dynamic or easy to learn and use. 

**Network Manager** was developed to make things easier and more uniform across distros. It can list all available networks (both wired and wireless), allow the choice of a wired, wireless, or mobile broadband network, handle passwords, and set up Virtual Private Networks (VPNs). Except for unusual situations, it is generally best to let Network Manager establish your connections and keep track of your settings.

### Wired and Wireless Connections
Wired connections usually do not require complicated or manual configuration. The hardware interface and signal presence are automatically detected, and then Network Manager sets the actual network settings via Dynamic Host Configuration Protocol (DHCP).

For **static** configurations that do not use DHCP, manual setup can also be done easily through Network Manager. You can also change the Ethernet Media Access Control (MAC) address if your hardware supports it. The MAC address is a unique hexadecimal number of your network card.

## Configuring Wireless Connections
To configure a wireless network in any recent GNOME-based distribution:
Click on the upper-right corner of the top panel, which brings up a settings and/or network window. While the exact appearance will depend on the Linux distro and version, it will always be possible to click on a _WI-FI_ submenu, as long as the hardware is present.

### Mobile Broadband and VPN Connections
The user can set up a mobile broadband connection with Network Manager, which will launch a wizard to set up the connection details for each connection.

Once the configuration is done, the network is configured automatically each time the broadband network is attached.

Network Manager can also manage your VPN connections.
It supports many VPN technologies, such as native IPSec, Cisco OpenConnect (via either the Cisco client or a native open source client), Microsoft PPTP, and OpenVPN.

### Installing and Updating Software
Each package in a Linux distro provides one piece of the system, such as the Linux kernel, the **C** compiler, utilities for manipulating text or configuring the network, or for the user's favorite web browsers and email clients.

Packages often depend on each other. For example, since the user's email client can communicate using SSL/TLS, it will depend on a package that provides the ability to encrypt and decrypt SSL and TLS communication and will not install unless that package is also installed at the same time.

All systems have a lower-level utility that handles the details of unpacking a package and putting the pieces in the right places. However, most of the time, you will be working with a higher-level utility that knows how to download and install packages directly from the internet and can manage dependencies and groups for the user. 

### Debian Packaging
Let's look at the package management for the Debian family system.

**dpkg** is the underlying package manager for these systems. It can install, remove, and build packages. Unlike higher-level package management systems, it does not automatically download and install packages and satisfy their dependencies.

For Debian-based systems, the higher-level package management system is the Advanced Package Tool (APT) system of utilities. Generally, while each distro within the Debian family uses APT, it creates its own interface on top of it (e.g., apt and apt-get, synaptic, gnome-software, Ubuntu Software Center, etc). Although apt repositories are generally compatible with each other, the software they contain generally is not. Therefore, most repositories target a particular distro (like Ubuntu), and often software distributors ship with multiple repositories to support multiple distributions.

### Red Hat Package Manager (RPM)
RPM is the other package management system popular on Linux distros. It was developed by Red Hat and adopted by a number of other distributions, including Fedora, CentOS, SUSE/openSUSE, Oracle Linux, and others.

The higher-level package manager differs between distros. Red Hat distros historically use RHEL/CentOS, and Fedora uses dnf, while SUSE family distros such as openSUSE also use RPM but use the zypper interface.

### openSUSE's YaST Software Management
The Yet another Setup Tool (YaST) software manager is similar to other graphical package managers. It is an RPM-based application. The user can add, remove, or update packages using this application very easily. To access the YaST software manager:
1. Click _Activities_
2. In the _Search_ box, type "YaST"
3. Click the YaST icon
4. Click _Software Management_

The user can also find YaST by clicking on _Applications > Other-YaST_, which is a strange place to put it.
