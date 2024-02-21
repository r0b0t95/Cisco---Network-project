# COLON
### ROUTER
[un servidor en] -> `administracion`
```
int f0/0
no shutdown
exit

int f0/0.12
encapsulation dot1q 12
ip add 192.20.100.1 255.255.255.248
exit

int f0/0.22
encapsulation dot1q 22
ip add 192.20.100.9 255.255.255.248
exit

int f0/0.32  
encapsulation dot1q 32 
ip add 192.20.100.17 255.255.255.248
exit 

int f0/0.42  
encapsulation dot1q 42 
ip add 192.20.100.25 255.255.255.248
exit 

int f0/0.52  
encapsulation dot1q 52 
ip add 192.20.100.33 255.255.255.248
exit 

int f0/0.99    
encapsulation dot1q 99 native  
ip add 192.20.100.41 255.255.255.248
exit 
```

```
ip dhcp excluded-address 192.20.100.1
ip dhcp excluded-address 192.20.100.9
ip dhcp excluded-address 192.20.100.17
ip dhcp excluded-address 192.20.100.25
ip dhcp excluded-address 192.20.100.33
ip dhcp excluded-address 192.20.100.41
ip dhcp excluded-address 192.20.100.26
```

```
ip dhcp pool reparacion
network 192.20.100.0 255.255.255.248
default-router 192.20.100.1
dns-server 192.60.100.34
option 150 ip 192.20.100.1
exit

ip dhcp pool ventas
network 192.20.100.8 255.255.255.248
default-router 192.20.100.9
dns-server 192.60.100.34
option 150 ip 192.20.100.9
exit

ip dhcp pool publicidad
network 192.20.100.16 255.255.255.248
default-router 192.20.100.17
dns-server 192.60.100.34
option 150 ip 192.20.100.17
exit

ip dhcp pool administracion
network 192.20.100.24 255.255.255.248
default-router 192.20.100.25
dns-server 192.60.100.34
option 150 ip 192.20.100.25
exit

ip dhcp pool voz       
Network 192.20.100.32 255.255.255.248
default-router 192.20.100.33
dns-server 192.60.100.34
option 150 ip 192.20.100.33        
exit 
```

```
TELEPHONY-SERVICE
MAX-DN 4
MAX-EPHONES 4
IP SOURCE-ADDRESS 192.20.100.33 PORT 2000
AUTO ASSIGN 1 TO 4
EXIT

EPHONE-DN 1
NUMBER 507100
EXIT

EPHONE-DN 2
NUMBER 507200
EXIT

EPHONE-DN 3
NUMBER 507300
EXIT

EPHONE-DN 4
NUMBER 507400
EXIT
```

```
INTERFACE F0/0
IP ADD 192.20.100.1 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.20.100.9 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.20.100.17 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.20.100.25 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.20.100.33 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.20.100.41 255.255.255.248
NO SHUTDOWN
exit

interface s0/0/0
ip ad 10.11.20.2 255.255.255.252
no shutdown
exit

interface s0/0/1
ip ad 10.11.80.2 255.255.255.252
no shutdown
exit
```

```
router ospf 10
router-id 1.1.1.1
network 10.11.80.0 0.0.0.3 area 0
network 10.11.20.0 0.0.0.3 area 0
network 192.20.100.0 0.0.0.7 area 0
network 192.20.100.8 0.0.0.7 area 0
network 192.20.100.16 0.0.0.7 area 0
network 192.20.100.24 0.0.0.7 area 0
network 192.20.100.32 0.0.0.7 area 0
network 192.20.100.40 0.0.0.7 area 0
exit
```

```
int lo1
ip ad 198.100.10.0 255.255.255.255
exit
```

```
int s0/0/1
bandwidth 128
exit
```

### SWITCHs
[un servidor en] -> `administracion`
```
vlan 12
name reparacion
exit

vlan 22
name ventas
exit

vlan 32
name publicidad
exit

vlan 42
name administracion
exit

vlan 52
name voz
exit

vlan 99
name nativa
exit
```

```
int range fa0/1-5
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 42
exit

int range fa0/6-10
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 32
exit

int range fa0/11-15
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 22
exit

int range fa0/16-21
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 12
exit

int range fa0/1-21  
switchport mode access
switchport voice vlan 52  
exit

int range fa0/22-24
SWITCHPORT MODE TRUNK
SWITCHPORT TRUNK NATIVE vlan 99
exit
```

  

