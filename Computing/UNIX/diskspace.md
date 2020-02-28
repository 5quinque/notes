# diskspace

## sort using du

```bash
du -hx --max-depth=1 . | sort -h
```

To find large subdirectories, you can grep for directories taking up more than 1GB. 

```bash
du -hx --max-depth=4 . | egrep "^[0-9\.]+G"
```

### rhel 5

```bash
du -x --max-depth=1 . | sort -n | cut -f2- | xargs du -xhs
```

### solaris

```bash
for i in G M K; do du -ah | grep [0-9]$i | sort -nr -k 1; done | head -n 11
```

## Find total size of all files older than 365 days

```bash
find . -mtime +365 -exec du -ch {} + | grep total$
```

## Archive files older than 365 days

```bash
find . -type f -mtime +365 -print0 |  /opt/backup/log/older_than_365.tar.gz --null -T -
find . -type f -mtime +365 -delete
```

Alternative

```bash
find . -name "*-$(date +%Y)*" -not -name "*.tar.gz" -exec tar -cvzf {}.tar.gz {} \; -exec rm -f {} \;
```

## Find deleted files using disk space

```bash
lsof | grep '(deleted)'
```

Example:
```
COMMAND     PID     USER   FD      TYPE             DEVICE  SIZE/OFF       NODE NAME
vmtoolsd   1077     root    3u      REG              253,4      4240         39 /tmp/vmware-root/vmware-apploader-1077.log (deleted)
```

```
# ls -l /proc/1077/fd
lrwx------. 1 root root 64 Feb 14 14:27 3 -> /tmp/vmware-root/vmware-apploader-1077.log (deleted)
# rm /proc/1077/fd/3
```

