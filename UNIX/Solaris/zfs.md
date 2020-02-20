# ZFS

## Increase filesystem
`zpool status localpool`

```
  pool: localpool
state: ONLINE
status: The pool is formatted using an older on-disk format.  The pool can
        still be used, but some features are unavailable.
action: Upgrade the pool using 'zpool upgrade'.  Once this is done, the
        pool will no longer be accessible on older software versions.
scan: none requested
config:
        NAME          STATE     READ WRITE CKSUM
        localpool     ONLINE       0     0     0
          mirror-0    ONLINE       0     0     0
            c0t0d0s5  ONLINE       0     0     0
            c0t1d0s5  ONLINE       0     0     0
errors: No known data errors
```


`zpool list localpool`

```
NAME       SIZE  ALLOC   FREE  CAP  HEALTH  ALTROOT
localpool  102G  65.9G  36.1G  64%  ONLINE  -
```

`zfs get quota,reservation localpool/apps-ora`

```
NAME                PROPERTY     VALUE   SOURCE
localpool/apps-ora  quota        30G     local
localpool/apps-ora  reservation  30G     local
```

`zfs set quota=37G localpool/apps-ora`
`zfs set reservation=37G localpool/apps-ora`
`df -h /apps/ora/`

```
Filesystem             size   used  avail capacity  Mounted on
localpool/apps-ora      37G    29G   7.6G    80%    /apps/ora
```

`zfs list | grep ora`

```
localpool/apps-ora             29.4G  7.56G  29.4G  /apps/ora
```
