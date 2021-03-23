Mount raw image of entire disc

Raw disc images are very common, they include things like images created using dd for backups and virtual machine disk images. To access the disc image content means the disk image needs to be mounted.

Images from a partition can directly be mounted as the reflect only one particular filesystem. Raw images of an entire disk contain potentially multiple partitions with different filesystems on them. To identify the type of the image, blkid(8) can be used.

```
$ blkid partition.img
partition.img: SEC_TYPE="msdos" UUID="1EFE-FEF8" TYPE="vfat"
$ blkid disk.img
disk.img: PTUUID="7ecf171e" PTTYPE="dos"
```

The first image shows an image of a single partition with the fat filesystem on it shown via the TYPE=”vfat”. The second image is an image containing a whole disc with partitions. The PTTYPE=”dos” shows the partition table type, indicating that the image contains a partition layout instead of only the file-system.
Attach the image to a loop device

To mount and work with the image, it needs to be attached to a loop device. To do so, losetup(8) can be used. The -f option will search for the next free loop device to attach the image to. The -P option will trigger a scan for partitions on the attached image and create devices for each partition detected.

```
$ sudo losetup -f -P disk.img
```

To verify that the image was detected and the partition(s) were detected, use the following commands.
```
$ losetup -l
NAME       SIZELIMIT OFFSET AUTOCLEAR RO BACK-FILE
/dev/loop0         0      0         0  0 /home/gerhard/Desktop/SD_card_rescue.img
$ ls -1 /dev/loop0*
/dev/loop0
/dev/loop0p1
```
The first command uses losetup with the -l option to show the attached image to the loop device “loop0”. The second command lists the “loop0” device and the partition(s) found on the disk, “loop0p1”.
Mount the filesystem

With the image attached to the system as a block device, it can be mounted as normal. When the image contains the partition table, the device to mount is not “loop0” as it represents the disc not the partition. The partitions are indicated by “loop0p1”, for example.
```
$ sudo mount /dev/loop0p1 /mnt/test/
```
Detach the image from loop device

Before the disk image can be detached again from the loop device, the mounted filesystem needs to be unmounted. Depending on whether the disk image is from a single partition or an entire disk, the device to be unmounted needs to be given, like in the mount command.
```
$ sudo umount /dev/loop0p1
```
With the filesystem unmounted, the disk image can be detached from the loop device.
```
$ sudo losetup -d /dev/loop0
```
With the “-d” option, losetup is instructed to detach the specified loop device.
