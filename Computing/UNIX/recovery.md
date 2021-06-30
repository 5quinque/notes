# Recovery

## Mount filesystems

Check where the filesystems are

``bash
fdisk -l
lvs
``

Based on the previous information, mount filesystems and chroot

```bash
mkdir rootfs
mount /dev/mapper/fedora_localhost--live-root rootfs
mount /dev/mapper/fedora_localhost--live-home rootfs/home
mount /dev/sda2 rootfs/boot
mount /dev/sda1 rootfs/boot/efi
cd rootfs
mount -o bind /dev dev
mount -o bind /proc proc
mount -o bind /sys sys
mount -t tmpfs tmpfs tmp
chroot .
```
