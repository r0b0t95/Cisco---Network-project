```
interface s0/2/0
ip ad 12.11.30.2 255.255.255.252
no shutdown
exit

interface s0/2/1
ip ad 12.11.40.1 255.255.255.252
no shutdown
exit
```

```
router eigrp 64
NETWORK 12.11.30.0 0.0.0.3
redistribute rip metric 1658031 514560 255 255 1500
exit
```

```
ROUTE RIP
VERSION 2
NETWORK 12.11.40.0
redistribute eigrp 64 metric 2
exit
```

