# SSHPass

Create a file, `.mypass` and put in your password.
Put all the hostnames in 

```bash
#!/bin/bash

SSHPASS="/usr/bin/sshpass"
COMMAND="ls

while read host; do
    echo "echo $host"
    # echo "$SSHPASS -f .mypass ssh -qt -o \"StrictHostKeyChecking no\" $host \"$COMMAND\""
    # echo "$SSHPASS -f .mypass ssh -o \"StrictHostKeyChecking no\" $host \"$COMMAND\""
    $SSHPASS -f .mypass ssh -o "StrictHostKeyChecking no" $host "$COMMAND"
done < $1
```