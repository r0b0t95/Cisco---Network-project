```
interface s0/2/1
ip ad 10.11.50.1 255.255.255.252
no shutdown
exit

interface s0/2/0
ip ad 10.11.70.2 255.255.255.252
no shutdown
exit

interface s0/0/0
ip ad 12.11.40.2 255.255.255.252
no shutdown
exit
```

```
ROUTER RIP
VERSION 2
NETWORK 10.11.50.0
NETWORK 10.11.70.0
NETWORK 10.11.90.0
NETWORK 12.11.40.0
EXIT
```