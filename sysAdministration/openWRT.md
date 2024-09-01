# Installation

**!** For install os to hard drive you need to use only **x86-64 generic-ext4-combined-efi.img.gz** verisions.

**!** Use **rufus** for create installation device

**!** Check if lan cable connected to lan port and wlan cable connected to wlan wort

## Folow by steps:

#### - Connect to device by ssh by address 192.168.1.1

#### - Install parted for work with disks

```bash
opkg update
opkg install parted
```

#### - Use this commands for check disks status

```bash
parted -l
```

You ssd disk status shluld be like that

```bash
Model: ATA SSD 64GB (scsi)
Disk /dev/sda: 64.0GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name  Flags

Model: Kingston DataTravel 3.0 (scsi)
Disk /dev/sdb: 31.0GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name  Flags
 1      17.4kB  262KB   245kB                      bios_grub
 2      262kB   17.0GB  16.8MB  fat16              legacy_boot
 2      17.0MB  126MB   109MB   ext2

```

#### - Start the disk modification

```bash
parted /dev/sda
```

Create the new gpt table

```bash
mklabel gpt
```

Create the load the rootfs partitions

```bash
mkpart EFI fat32 1MiB 261MiB
```

turn load partition into the UEFI mod

```bash
set 1 esp on
```

create DATA partitoin

```bash
mkpart DATA ext4 261MiB 100%
```

after that write **q** for save and exit

#### - check disk status again with this command

```bash
parted -l
```

you main disk status should be like that

```bash
Model: ATA SSD 64GB (scsi)
Disk /dev/sda: 64.0GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name  Flags
 1      1049kB  274MB   273MB   fat32        EFI   boot, esp
 2      274MB   64.0GB  63.7GB  ext4         DATA

```

**If** in your case partitions doesn't have the file system, you should follow by steps in this punct
install the dosfstools

```bash
opkg install dosfstools
```

format first partition to FAT32

```bash
mkfs.fat -F 32 /dev/sda1
```

format the second to EXT4

```bash
mkfs.ext4 /dev/sda2
```

#### - now we need to mount the partitions /dev/sda1 , /dev/sda2 , /dev/sdb1 , /dev/sdb2

```bash
mkdir /mnt_efi_old
mkdir /mnt_efi_new
mkdir /mnt_ext4_old
mkdir /mnt_ext4_new
mount /dev/sdb1 /mnt_efi_old
mount /dev/sda1 /mnt_efi_new
mount /dev/sdb2 /mnt_ext4_old
mount /dev/sda2 /mnt_ext4_new
```

#### - Copy everything from /mnt_efi_old to /mnt_efi_new

```bash
cp -a /mnt_efi_old/. /mnt_efi_new
```

#### - now we need to check disk PARTUUID

**?** PARTUUID - is real name of the disk. Yes /dev/sda1 is not exacly the real names of the disks
install blkid

```bash
opkg install blkid
```

check the disks info. You need the /dev/sda2 PARTUUID

```bash
blkid
```

#### - Open the operation system loading file

```bash
vi /mnt_efi_new/boot/grub/grub.cfg
```

You need to change timout setting to "1" and in all loading variants rplace the root=PARTUUID= name to /dev/sda2 PARTUUID

TODO - Add the grub.cfg text to better comprehension

#### - Copy everything from /mnt_ext4_old to /mnt_ext4_new

```bash
cp -a /mnt_ext4_old/. /mnt_ext4_new
```

- reboot the routher and unplug you usb
