# RPM

Listing the Most Recently Installed Packages

```bash
rpm -qa --last | head
```

Find OS installation date

```bash
rpm -qi basesystem | grep Install
```