# Find

## Find total size of all files older than 365 days

`find . -mtime +365 -exec du -ch {} + | grep total$`

## Archive files older than 365 days

```bash
find . -type f -mtime +365 -print0 |  /opt/backup/log/older_than_365.tar.gz --null -T -
find . -type f -mtime +365 -delete
```