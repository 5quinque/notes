# RPM

## Listing the Most Recently Installed Packages

```bash
rpm -qa --last | head
```

## Find OS installation date

```bash
rpm -qi basesystem | grep Install
```

## Extract RPM

```bash
rpm2cpio firmware-system-p70-2019.05.24-1.1.i386.rpm | cpio -idmv
```
