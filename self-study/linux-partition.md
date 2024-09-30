# Creating Linux partitions with `fdisk`.

### Introduction
Partitioning a disk is a fundamental task in setting up a Linux system. It involves dividing a disk into separate sections, each of which can be managed independently. This allows for better organization, improved performance, and easier management of data. The `fdisk` utility is a powerful tool for creating and managing disk partitions in Linux. It is especially useful for managing MBR (Master Boot Record) partitions but can also handle GPT (GUID Partition Table) partitions.

### MBR Scheme
The Master Boot Record (MBR) is an older partitioning scheme that has been widely used since the early days of personal computing. It supports disks up to 2 TB in size and allows up to four primary partitions. If more partitions are needed, one of the primary partitions can be designated as an extended partition, which can contain multiple logical partitions.

- **Structure**: The MBR is located at the very beginning of the disk and contains the bootloader, the partition table, and a signature. The partition table can hold entries for up to four primary partitions.
- **Limitations**: MBR's main limitations are its 2 TB disk size limit and the restriction to four primary partitions. To overcome the latter, one primary partition can be converted into an extended partition, which can then hold multiple logical partitions.

### GPT Scheme
The GUID Partition Table (GPT) is a modern partitioning scheme that is part of the UEFI (Unified Extensible Firmware Interface) standard. It supports disks larger than 2 TB and allows for an almost unlimited number of partitions. GPT provides better data integrity and recovery options compared to MBR.

- **Structure**: GPT stores multiple copies of the partition table across the disk, which improves the chances of recovery in case of corruption. It also includes CRC32 checksums to detect errors.
- **Advantages**: GPT supports larger disks, more partitions, and includes redundancy and error-checking features. It is the preferred partitioning scheme for modern systems.

### VirtualBox
VirtualBox is a popular virtualization software that allows you to run multiple operating systems on a single physical machine. When setting up a Linux virtual machine (VM) in VirtualBox, you can use `fdisk` to partition the virtual disk just as you would with a physical disk.

- **Creating a VM**: When creating a new VM in VirtualBox, you can specify the size of the virtual disk. This disk can then be partitioned using `fdisk` within the VM.
- **Partitioning**: The process of partitioning a virtual disk in VirtualBox is identical to partitioning a physical disk. This makes VirtualBox a great tool for learning and experimenting with disk partitioning.

### Fdisk
`fdisk` is a command-line utility for managing disk partitions. It is menu-driven and allows you to create, delete, and manipulate partitions on a disk. `fdisk` is suitable for both MBR and GPT partitioning schemes, although it is more commonly associated with MBR.

- **Usage**: `fdisk` is invoked with the disk device as an argument (e.g., `sudo fdisk /dev/sda`). It then presents a menu of options for managing partitions.
- **Commands**: Common commands in `fdisk` include `n` for creating a new partition, `d` for deleting a partition, `p` for printing the partition table, and `w` for writing changes to the disk.

### MBR
As mentioned earlier, MBR is an older partitioning scheme. When using `fdisk` with MBR, you can create up to four primary partitions or three primary partitions and one extended partition. The extended partition can contain multiple logical partitions.

- **Creating Partitions**: To create a new partition, you use the `n` command in `fdisk`. You will be prompted to choose between a primary or extended partition and to specify the size and location of the partition.
- **Managing Partitions**: You can delete partitions with the `d` command and change partition types with the `t` command.

### Create a New Partition
To create a new partition using `fdisk`, follow these steps:

1. **Open `fdisk`**: Open a terminal and run `sudo fdisk /dev/sdX`, replacing `/dev/sdX` with the appropriate disk identifier (e.g., `/dev/sda`).

2. **List Partitions**: Type `p` to list the current partitions on the disk. This helps you understand the current layout of the disk.

3. **Create a New Partition**: Type `n` to create a new partition. You will be prompted to choose between a primary or extended partition. Choose `p` for primary or `e` for extended.

4. **Specify Partition Number**: Enter the partition number (1-4 for primary partitions).

5. **Specify First Sector**: Press `Enter` to accept the default first sector, or specify a different starting point.

6. **Specify Last Sector**: Press `Enter` to accept the default last sector, or specify the size of the partition (e.g., `+10G` for a 10 GB partition).

7. **Write Changes**: Type `w` to write the changes to the disk and exit `fdisk`. This step is crucial as it saves the partition table to the disk.

### Change Partition Type
To change the type of a partition using `fdisk`, follow these steps:

1. **Open `fdisk`**: Open a terminal and run `sudo fdisk /dev/sdX`, replacing `/dev/sdX` with the appropriate disk identifier.

2. **List Partitions**: Type `p` to list the current partitions on the disk.

3. **Select Partition**: Type `t` to change the partition type.

4. **Specify Partition Number**: Enter the partition number you want to change.

5. **Enter Hex Code**: Enter the hex code for the desired partition type (e.g., `83` for a Linux filesystem, `82` for Linux swap). You can list all available types by typing `L`.

6. **Write Changes**: Type `w` to write the changes to the disk and exit `fdisk`.

By following these steps, you can effectively manage disk partitions in Linux using `fdisk`. This utility is powerful and flexible, making it a valuable tool for system administrators and users alike.