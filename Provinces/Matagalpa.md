# MATAGALPA
### ROUTER
```
int f0/0
no shutdown
exit

int f0/0.16
encapsulation dot1q 16
ip add 192.30.100.1 255.255.255.248
exit

int f0/0.26
encapsulation dot1q 26
ip add 192.30.100.9 255.255.255.248
exit

int f0/0.36  
encapsulation dot1q 36 
ip add 192.30.100.17 255.255.255.248
exit 

int f0/0.46  
encapsulation dot1q 46 
ip add 192.30.100.25 255.255.255.248
exit 

int f0/0.56  
encapsulation dot1q 56 
ip add 192.30.100.33 255.255.255.248
exit 

int f0/0.99    
encapsulation dot1q 99 native  
ip add 192.30.100.41 255.255.255.248
exit 
```

```
ip dhcp excluded-address 192.30.100.1
ip dhcp excluded-address 192.30.100.9
ip dhcp excluded-address 192.30.100.17
ip dhcp excluded-address 192.30.100.25
ip dhcp excluded-address 192.30.100.33
ip dhcp excluded-address 192.30.100.41
```

```
ip dhcp pool reparacion
network 192.30.100.0 255.255.255.248
default-router 192.30.100.1
dns-server 192.60.100.34
option 150 ip 192.30.100.1
exit

ip dhcp pool ventas
network 192.30.100.8 255.255.255.248
default-router 192.30.100.9
dns-server 192.60.100.34
option 150 ip 192.30.100.9
exit

ip dhcp pool publicidad
network 192.30.100.16 255.255.255.248
default-router 192.30.100.17
dns-server 192.60.100.34
option 150 ip 192.30.100.17
exit

ip dhcp pool administracion
network 192.30.100.24 255.255.255.248
default-router 192.30.100.25
dns-server 192.60.100.34
option 150 ip 192.30.100.25
exit

ip dhcp pool voz       
Network 192.30.100.32 255.255.255.248
default-router 192.30.100.33
dns-server 192.60.100.34
option 150 ip 192.30.100.33        
exit 
```

```
TELEPHONY-SERVICE
MAX-DN 4
MAX-EPHONES 4
IP SOURCE-ADDRESS 192.30.100.33 PORT 2000
AUTO ASSIGN 1 TO 4
EXIT

EPHONE-DN 1
NUMBER 505100
EXIT

EPHONE-DN 2
NUMBER 505200
EXIT

EPHONE-DN 3
NUMBER 505300
EXIT

EPHONE-DN 4
NUMBER 505400
EXIT
```

```
INTERFACE F0/0
IP ADD 192.30.100.1 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.30.100.9 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.30.100.17 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.30.100.25 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.30.100.33 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.30.100.41 255.255.255.248
NO SHUTDOWN
exit

interface s0/1/0
ip ad 10.11.50.2 255.255.255.252
no shutdown
exit

interface s0/1/1
ip ad 10.11.90.2 255.255.255.252
no shutdown
exit
```

```
ROUTER RIP
VERSION 2
NETWORK 10.11.90.0
NETWORK 10.11.70.0
NETWORK 10.11.50.0
NETWORK 192.30.100.0
NETWORK 192.30.100.8
NETWORK 192.30.100.16
NETWORK 192.30.100.24
NETWORK 192.30.100.32
NETWORK 192.30.100.40
NETWORK 12.11.40.0
EXIT
```

### SWITCHs
```
vlan 16
name reparacion
exit

vlan 26
name ventas
exit

vlan 36
name publicidad
exit

vlan 46
name administracion
exit

vlan 56
name voz
exit

vlan 99
name nativa
exit
```

```
int range fa0/1-5
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 46
exit

int range fa0/6-10
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 36
exit

int range fa0/11-15
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 26
exit

int range fa0/16-21
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 16
exit

int range fa0/1-21  
switchport mode access
switchport voice vlan 56 
exit

int range fa0/22-24
SWITCHPORT MODE TRUNK
SWITCHPORT TRUNK NATIVE vlan 99
exit
```