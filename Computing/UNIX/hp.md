# HP

## Get HP iLO IP address

(Must be run as root/super user)

```bash
/sbin/hponcfg -w /dev/shm/tmp && grep '<IP_ADDRESS' /dev/shm/tmp
```

## Get Fan status

`hpasmcli -s 'SHOW FANS'`

## HP IML Logs

```bash
hplog -v # This will show the HP IML log and the alerts tied to the fan failures.
hplog -t # This will show the temperature zones.

hplog -f # This will show the fan ID and status.
```

## Generate ADU Report

```bash
hpacucli ctrl all diag file=/tmp/ADUReport.zip
```

## Mount virtual media

Generate iso

```bash
genisoimage -o p70.iso ./firmwarep70
```

```bash
modprobe usb_storage
mkdir /media/cdrom
mount -t iso9660 /dev/sr1 /media/cdrom
```


## Show Disk Info

```bash
hpssacli

=> ctrl all show config

Smart Array P440ar in Slot 0 (Embedded)   (sn: PDNLH0BRH8O2TL)


   12G SAS Exp Card at Port 1I, Box 1, OK

   Port Name: 1I

   Port Name: 2I
   array A (SAS, Unused Space: 0  MB)


      logicaldrive 1 (279.4 GB, RAID 1, OK)

      physicaldrive 1I:1:1 (port 1I:box 1:bay 1, SAS, 300 GB, OK)
      physicaldrive 1I:1:2 (port 1I:box 1:bay 2, SAS, 300 GB, OK)

   array B (SAS, Unused Space: 0  MB)


      logicaldrive 2 (12.0 TB, RAID 1+0, OK)

      physicaldrive 1I:1:4 (port 1I:box 1:bay 4, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:5 (port 1I:box 1:bay 5, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:6 (port 1I:box 1:bay 6, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:7 (port 1I:box 1:bay 7, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:8 (port 1I:box 1:bay 8, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:9 (port 1I:box 1:bay 9, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:10 (port 1I:box 1:bay 10, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:11 (port 1I:box 1:bay 11, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:12 (port 1I:box 1:bay 12, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:13 (port 1I:box 1:bay 13, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:14 (port 1I:box 1:bay 14, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:15 (port 1I:box 1:bay 15, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:16 (port 1I:box 1:bay 16, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:17 (port 1I:box 1:bay 17, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:18 (port 1I:box 1:bay 18, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:19 (port 1I:box 1:bay 19, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:20 (port 1I:box 1:bay 20, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:21 (port 1I:box 1:bay 21, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:22 (port 1I:box 1:bay 22, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:23 (port 1I:box 1:bay 23, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:24 (port 1I:box 1:bay 24, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:25 (port 1I:box 1:bay 25, SAS, 1200.2 GB, OK)
      physicaldrive 1I:1:3 (port 1I:box 1:bay 3, SAS, 1200.2 GB, Failed, spare)

   Enclosure SEP (Vendor ID HPE, Model 12G SAS Exp Card) 377  (WWID: 500143803525DDBC, Port: 1I, Box: 1)

   Expander 378  (WWID: 500143803525DDBD, Port: 1I, Box: 1)

```