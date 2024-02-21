```
INTERFACE S0/3/1
IP AD 12.11.20.2 255.255.255.252
NO SHUTDOWN
exit

INTERFACE S0/3/0
IP AD 12.11.10.1 255.255.255.252
NO SHUTDOWN
exit
```

```
router eigrp 64
NETWORK 12.11.20.0 0.0.0.3
redistribute ospf 10 metric 1500 1000 255 1 1500
exit
```

```
router ospf 10
NETWORK 12.11.10.0 0.0.0.3 area 0
redistribute eigrp 64 metric 10 subnets
exit
```