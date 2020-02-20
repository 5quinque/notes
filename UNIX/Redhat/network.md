
## Rename the device using the ip command:

```bash
/sbin/ip link set eth1 down
/sbin/ip link set eth1 name eth123
/sbin/ip link set eth123 up
```

ls -l /sys/class/net/

Change name in `etc/udev/rules.d/70-persistent-net.rules`

```
# PCI device 0x14e4:0x1657 (tg3)
SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="98:f2:b3:05:eb:af", ATTR{type}=="1", KERNEL=="eth*", NAME="eth10"

# PCI device 0x14e4:0x1657 (tg3)
SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="98:f2:b3:05:eb:af", ATTR{type}=="1", KERNEL=="eth*", NAME="eth2"
```