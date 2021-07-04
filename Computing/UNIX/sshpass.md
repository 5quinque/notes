# SSHPass

Create a file, `.mypass` and put in your password.
Put all the hostnames in a file

```bash
#!/bin/bash

SSHPASS="/usr/bin/sshpass"
COMMAND="ls"

while read host; do
    echo "echo $host"
    # echo "$SSHPASS -f .mypass ssh -qt -o \"StrictHostKeyChecking no\" $host \"$COMMAND\""
    # echo "$SSHPASS -f .mypass ssh -o \"StrictHostKeyChecking no\" $host \"$COMMAND\""
    $SSHPASS -f .mypass ssh -o "StrictHostKeyChecking no" $host "$COMMAND"
done < $1
```

## SSHPass with key passphrase

```bash
sshpass -f .mypass -P 'Enter passphrase for key' ssh -o "StrictHostKeyChecking no" $host "$COMMAND"
```