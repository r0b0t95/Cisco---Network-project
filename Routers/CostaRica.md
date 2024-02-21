```
interface s0/2/0
ip ad 10.11.30.2 255.255.255.252
no shutdown
exit

interface s0/2/1
ip ad 10.11.40.2 255.255.255.252
no shutdown
exit

interface s0/3/0
ip ad 12.11.30.1 255.255.255.252
no shutdown
exit

interface s0/3/1
ip ad 12.11.20.1 255.255.255.252
no shutdown
exit
```

```
router eigrp 64
NETWORK 10.11.30.0 0.0.0.3
NETWORK 10.11.40.0 0.0.0.3
NETWORK 12.11.20.0 0.0.0.3
NETWORK 12.11.30.0 0.0.0.3
NO AUTO -SUMMARY
EXIT
```