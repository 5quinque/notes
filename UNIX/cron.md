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

