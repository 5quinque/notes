# LVM

## 1. Rescan storage

```bash
echo "- - -" > /sys/class/scsi_host/host0/scan
echo "- - -" > /sys/class/scsi_host/host1/scan
echo "- - -" > /sys/class/scsi_host/host2/scan
```

## 2. Create Disk

```bash
# fdisk /dev/sdX

  g   create a new empty GPT partition table

  n   add a new partition

  w   write table to disk and exit
  
n # Create new partition
p
1


t # Change partitions system ID to Linux LVM
8e

p # Print partition table to confirm

w # Write to disk
```

## 3. Create PV


```bash
pvcreate /dev/sdXX
```

## 4. Add to VG

List volume groups to get the volume group name

```bash
# vgs
  VG          #PV #LV #SN Attr   VSize  VFree
  cl            1   2   0 wz--n- 11.00g  4.00m
  volumegroup   1   1   0 wz--n- 20.00g 10.00g
```


```bash
vgextend VolGroupName /dev/sdXX
```

## 5. Extend LV

```bash
# lvs
  LV   VG          Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root cl          -wi-ao----  9.79g
  swap cl          -wi-ao----  1.20g
  flex volumegroup -wi-ao---- 10.00g
```

```bash
lvextend -L+100G /dev/VolGroupName/LogicalVolName
```

## 6. Extend FS

```bash
resize2fs /dev/VolGroupName/LogicalVolName
```

```bash
df -h
```

## Create LV:

```bash
lvcreate -L 10G -nlfs volumegroup

mkfs.ext4 /dev/volumegroup/lfs
```

