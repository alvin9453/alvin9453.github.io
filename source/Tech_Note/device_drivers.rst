Device drivers
========================

Overview
----------

In UNIX, hardware devices are accessed by the user through special device files. These files are grouped into the /dev directory, and system calls ``open``, ``read``, ``write``, ``close``, ``lseek``, ``mmap`` etc. are redirected by the operating system to the device driver associated with the physical device. The device driver is a kernel component (usually a module) that interacts with a hardware device.

In the UNIX world there are two categories of device files and thus device drivers: **character** and **block**. This division is done by the speed, volume and way of organizing the data to be transferred from the device to the system and vice versa. For the two types of device drivers, the Linux kernel offers different APIs.

Character device drivers
```````````````````````````
- Slow devices
- Manage a small amount of data
- Access to data does not require frequent seek queries
- Operations (read, write) are performed sequentially byte by byte.
- Such as keyboard, mouse, serial ports, sound card, joystick.
- **[Linux kernel APIs]** System calls go directly to device drivers.

Block device drivers
``````````````````````
- Fast devices
- Data volume is large
- Search data is common.
- Data is organized on blocks
- Such as hard drives, cdroms, ram disks, magnetic tape drives.
- **[Linux kernel APIs]** The drivers do not work directly with system calls. Communication between the user-space and the block device driver is mediated by the file management subsystem and the block device subsystem.

Reference
-----------

- Linux Kernel Teaching : https://linux-kernel-labs.github.io/refs/heads/master/labs/device_drivers.html