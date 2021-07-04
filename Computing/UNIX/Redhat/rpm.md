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

## Downgrade package using yum

https://access.redhat.com/solutions/29617

If you know the exact version you want to downgrade to

```bash
yum downgrade package-version
```

On Red Hat 6+ you can run the following what some more information

```bash
yum history list all
yum history info <transaction_ID>
```

Or you can check the logs

```bash
grep -i packagename /var/log/yum.log*
```