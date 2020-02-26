# Miscellaneous

## Monitor what is accessing/modifying a file

To watch a file for changes, you can do this with auditctl with the following command:

`auditctl -w /path/to/filename -p wa`

All changes will then be shown in the audit log (`/var/log/audit/audit.log`)

`tail -f /var/log/audit/audit.log`

Once you have found what you're looking for, remove the watch with the following:

`auditctl -W /path/to/filename -p wa`
