*Stop Router/Switch from translating*
[switch & router]
```
no ip domain-lookup
```


*Start*
```
ena
confi te
```


[switch & router]
```
do show running-config
```
**switch**
- `show ports by vlan`
**router**
- `show ip dhcp excluded-address`
- `pool configurations`
- `show encapsulaption`
- `show serial configurations`
- `show eigrp configurations`
- `show telephony`


[switch]
```
do show vlan
```
**switch**
- `show vlans and ports configurations`


[switch & router]
```
do show ip interface brief
```
**switch**
- `show which ports are in use`
**router**
- `show which ports are in use with IP address relationship`


[router]
```
do show ip dhcp binding
```
**router**
- `show whichs computers and serials references in IP address are connected`


[router]
```
do show ip dhcp pool
```

[router]
```
do show ip route
```
**router**
- `show vlan connected by ospf, rip, eigrp`
	D = *EIGRP*
	R = *RIP*
	O = *OSPF*
	C = *Serials directly connect*



#### EIGRP - RIPV2
```
router eigrp 64
NETWORK 10.10.10.0 0.0.0.3
redistribute rip metric 1658031 514560 255 255 1500
exit
```

```
ROUTE RIP
VERSION 2
NETWORK 12.10.10.0
redistribute eigrp 10 metric 2
exit
```
#### EIGRP - OSPF
```
router eigrp 10
NETWORK 10.20.1.0 0.0.0.3
redistribute ospf 50 metric 1500 1000 255 1 1500
exit
```

```
router ospf 10
NETWORK 12.11.10.0 0.0.0.3 area 0
redistribute eigrp 64 metric 10 subnets
exit
```
#### RIPV2 - OSPF
```
router ospf 10
NETWORK 10.10.40.0 0.0.0.3 area 0
Redistribute RIP METRIC 10 SUBNETS 
exit
```

```
ROUTER RIP
VERSION 2
NETWORK 10.10.30.0
Redistribute OSPF 10 METRIC 4
exit
```


