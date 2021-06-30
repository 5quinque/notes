# mail

## Send test email

```bash
echo "Subject: sendmail test" | sendmail -v address@example.com
```

### View log from email

```bash
ADDRESS='address@example.com'
MID=$(grep -i $ADDRESS /var/log/maillog | sed "s/.\+: \(\w\+\): to=<${ADDRESS}>.\+/\1/")
[[ -z "$MID" ]] && echo "No logs for ${ADDRESS}" || grep $MID /var/log/maillog
```