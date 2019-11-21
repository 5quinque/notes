# diskspace

## sort using du

```bash
du -hx --max-depth=1 . | sort -h
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