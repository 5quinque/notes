# sar

```bash
sar -u 
sar -u # 1 3 Displays real time CPU usage every 1 second for 3 times.
sar -u # ALL Same as “sar -u” but displays additional fields.
sar -u # ALL 1 3 Same as “sar -u 1 3” but displays additional fields.
sar -u -f /var/log/sa/sa10 # Displays CPU usage for the 10day of the month from the sa10 file.Memory Free and Used (sar -r)
sar -r
```

## Swap Space Used (sar -S)

```bash
sar -S
```


## Overall I/O Activities (sar -b)

```bash
sar -b
```

Following fields are displays in the example below.
 - tps – Transactions per second (this includes both read and write)
 - rtps – Read transactions per second
 - wtps – Write transactions per second
 - bread/s – Bytes read per second 
 - bwrtn/s – Bytes written per second

## Individual Block Device I/O Activities (sar -d)

To identify the activities by the individual block devices (i.e a specific mount point, or LUN, or partition), use `sar -d`

```bash
$ sar -d 1 1
Linux 2.6.18-194.el5PAE (dev-db)        03/26/2011      _i686_  (8 CPU)

01:59:45 PM       DEV       tps  rd_sec/s  wr_sec/s  avgrq-sz  avgqu-sz     await     svctm     %util
01:59:46 PM    dev8-0      1.01      0.00      0.00      0.00      0.00      4.00      1.00      0.10
01:59:46 PM    dev8-1      1.01      0.00      0.00      0.00      0.00      4.00      1.00      0.10
01:59:46 PM dev120-64      3.03     64.65      0.00     21.33      0.03      9.33      5.33      1.62
01:59:46 PM dev120-65      3.03     64.65      0.00     21.33      0.03      9.33      5.33      1.62
01:59:46 PM  dev120-0      8.08      0.00    105.05     13.00      0.00      0.38      0.38      0.30
01:59:46 PM  dev120-1      8.08      0.00    105.05     13.00      0.00      0.38      0.38      0.30
01:59:46 PM dev120-96      1.01      8.08      0.00      8.00      0.01      9.00      9.00      0.91
01:59:46 PM dev120-97      1.01      8.08      0.00      8.00      0.01      9.00      9.00      0.91
```

In the above example “DEV” indicates the specific block device.
For example: “dev53-1” means a block device with 53 as major number, and 1 as minor number.
The device name (DEV column) can display the actual device name (for example: sda, sda1, sdb1 etc.,), if you use the -p option (pretty print) as shown below.

```bash
$ sar -p -d 1 1
Linux 2.6.18-194.el5PAE (dev-db)        03/26/2011      _i686_  (8 CPU)

01:59:45 PM       DEV       tps  rd_sec/s  wr_sec/s  avgrq-sz  avgqu-sz     await     svctm     %util
01:59:46 PM       sda      1.01      0.00      0.00      0.00      0.00      4.00      1.00      0.10
01:59:46 PM      sda1      1.01      0.00      0.00      0.00      0.00      4.00      1.00      0.10
01:59:46 PM      sdb1      3.03     64.65      0.00     21.33      0.03      9.33      5.33      1.62
01:59:46 PM      sdc1      3.03     64.65      0.00     21.33      0.03      9.33      5.33      1.62
01:59:46 PM      sde1      8.08      0.00    105.05     13.00      0.00      0.38      0.38      0.30
01:59:46 PM      sdf1      8.08      0.00    105.05     13.00      0.00      0.38      0.38      0.30
01:59:46 PM      sda2      1.01      8.08      0.00      8.00      0.01      9.00      9.00      0.91
01:59:46 PM      sdb2      1.01      8.08      0.00      8.00      0.01      9.00      9.00      0.91
```