# cron

## Format for cron jobs

`mi h d m w command`

## Silencing a cron job

Append >/dev/null 2>&1 to a cron job to silence all output.

The following example sends `STDOUT` (1) and `STDERR` (2) to `/dev/null`, effectively silencing all output.

`0          0   *  *  *    /bin/bash /opt/somescript.sh >/dev/null 2>&1`

## Examples:

Run at ten minutes past the hour, every hour, day etc.

`10 * * * * ls`

Run every five minutes, on the 6th hour, every day etc.

`*/5 6 * * * ls`

Run on the 14th, 29th, 44th and 59th minute of every hour etc.

`14,29,44,59 * * * * ls`

## Multiple cron processes

```
# ps -ef | grep -i cron
root      3158     1  0  2019 ?        00:04:17 /usr/sbin/crond -n
root     12447  3158  0 Feb24 ?        00:00:00 /usr/sbin/CROND -n
root     13199  3158  0 Feb27 ?        00:00:00 /usr/sbin/CROND -n
root     13710  3158  0 Feb18 ?        00:00:00 /usr/sbin/CROND -n
root     13873  3158  0 Feb21 ?        00:00:00 /usr/sbin/CROND -n
root     32476  3158  0 Feb26 ?        00:00:00 /usr/sbin/CROND -n
root     34344  3158  0 Feb23 ?        00:00:00 /usr/sbin/CROND -n
root     35668  3158  0 Feb17 ?        00:00:00 /usr/sbin/CROND -n
root     36114  3158  0 Feb20 ?        00:00:00 /usr/sbin/CROND -n
root     52439 52400  0 08:33 pts/0    00:00:00 grep --color=auto -i cron
root     54992  3158  0 Feb25 ?        00:00:00 /usr/sbin/CROND -n
root     55445  3158  0 00:05 ?        00:00:00 /usr/sbin/CROND -n
root     56350  3158  0 Feb19 ?        00:00:00 /usr/sbin/CROND -n
root     56649  3158  0 Feb22 ?        00:00:00 /usr/sbin/CROND -n
```

Run `pstree` on the parent cron process to find what's running:

`pstree -a -p 3158`

Possibly find the parent cron process automatically:

`pstree -a -p $(ps -ef | grep '[c]rond' | awk '{ print $2 }')`