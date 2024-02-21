```
INTERFACE S0/1/0
IP AD 10.11.10.1 255.255.255.252
NO SHUTDOWN
exit

INTERFACE S0/1/1
IP AD 10.11.20.1 255.255.255.252
NO SHUTDOWN
exit

INTERFACE S0/0/0
IP AD 12.11.10.2 255.255.255.252
NO SHUTDOWN
exit
```

```
router ospf 10
network 10.11.10.0 0.0.0.3 area 0
network 10.11.20.0 0.0.0.3 area 0
network 12.11.10.0 0.0.0.3 area 0
exit
```

```
int lo0
ip ad 192.100.10.0 255.255.255.255
exit
```