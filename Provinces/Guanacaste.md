# GUANACASTE
### ROUTER
```
int f0/0
no shutdown
exit

int f0/0.15
encapsulation dot1q 15
ip add 192.50.100.1 255.255.255.248
exit

int f0/0.25
encapsulation dot1q 25
ip add 192.50.100.9 255.255.255.248
exit

int f0/0.35  
encapsulation dot1q 35 
ip add 192.50.100.17 255.255.255.248
exit 

int f0/0.45  
encapsulation dot1q 45 
ip add 192.50.100.25 255.255.255.248
exit 

int f0/0.55  
encapsulation dot1q 55 
ip add 192.50.100.33 255.255.255.248
exit 

int f0/0.99    
encapsulation dot1q 99 native  
ip add 192.50.100.41 255.255.255.248
exit 
```

```
ip dhcp excluded-address 192.50.100.1
ip dhcp excluded-address 192.50.100.9
ip dhcp excluded-address 192.50.100.17
ip dhcp excluded-address 192.50.100.25
ip dhcp excluded-address 192.50.100.33
ip dhcp excluded-address 192.50.100.41
```

```
ip dhcp pool reparacion
network 192.50.100.0 255.255.255.248
default-router 192.50.100.1
dns-server 192.60.100.34
option 150 ip 192.50.100.1
exit

ip dhcp pool ventas
network 192.50.100.8 255.255.255.248
default-router 192.50.100.9
dns-server 192.60.100.34
option 150 ip 192.50.100.9
exit

ip dhcp pool publicidad
network 192.50.100.16 255.255.255.248
default-router 192.50.100.17
dns-server 192.60.100.34
option 150 ip 192.50.100.17
exit

ip dhcp pool administracion
network 192.50.100.24 255.255.255.248
default-router 192.50.100.25
dns-server 192.60.100.34
option 150 ip 192.50.100.25
exit

ip dhcp pool voz       
Network 192.50.100.32 255.255.255.248
default-router 192.50.100.33
dns-server 192.60.100.34
option 150 ip 192.50.100.33        
exit 
```

```
TELEPHONY-SERVICE
MAX-DN 4
MAX-EPHONES 4
IP SOURCE-ADDRESS 192.50.100.33 PORT 2000
AUTO ASSIGN 1 TO 4
EXIT

EPHONE-DN 1
NUMBER 506100
EXIT

EPHONE-DN 2
NUMBER 506200
EXIT

EPHONE-DN 3
NUMBER 506300
EXIT

EPHONE-DN 4
NUMBER 506400
EXIT
```

```
INTERFACE F0/0
IP ADD 192.50.100.1 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.50.100.9 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.50.100.17 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.50.100.25 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.50.100.33 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.50.100.41 255.255.255.248
NO SHUTDOWN
exit

interface s0/2/0
ip ad 10.11.40.1 255.255.255.252
no shutdown
exit

interface s0/2/1
ip ad 10.11.60.2 255.255.255.252
no shutdown
exit
```

```
router eigrp 64
NETWORK 10.11.40.0 0.0.0.3
NETWORK 10.11.60.0 0.0.0.3
NETWORK 192.50.100.1 0.0.0.7
NETWORK 192.50.100.9 0.0.0.7
NETWORK 192.50.100.17 0.0.0.7
NETWORK 192.50.100.25 0.0.0.7
NETWORK 192.50.100.33 0.0.0.7
NETWORK 192.50.100.41 0.0.0.7
NO AUTO -SUMMARY
EXIT
```

### SWITCHs
```
vlan 15
name reparacion
exit

vlan 25
name ventas
exit

vlan 35
name publicidad
exit

vlan 45
name administracion
exit

vlan 55
name voz
exit

vlan 99
name nativa
exit
```

```
int range fa0/1-5
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 45
exit

int range fa0/6-10
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 35
exit

int range fa0/11-15
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 25
exit

int range fa0/16-21
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 15
exit

int range fa0/1-21  
switchport mode access
switchport voice vlan 55
exit

int range fa0/22-24
SWITCHPORT MODE TRUNK
SWITCHPORT TRUNK NATIVE vlan 99
exit
```