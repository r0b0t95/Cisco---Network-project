# HERRERA
### ROUTER
```
int f0/0
no shutdown
exit

int f0/0.17
encapsulation dot1q 17
ip add 192.10.100.1 255.255.255.248
exit

int f0/0.27
encapsulation dot1q 27
ip add 192.10.100.9 255.255.255.248
exit

int f0/0.37  
encapsulation dot1q 37 
ip add 192.10.100.17 255.255.255.248
exit 

int f0/0.47  
encapsulation dot1q 47 
ip add 192.10.100.25 255.255.255.248
exit 

int f0/0.57  
encapsulation dot1q 57 
ip add 192.10.100.33 255.255.255.248
exit 

int f0/0.99    
encapsulation dot1q 99 native  
ip add 192.10.100.41 255.255.255.248
exit 
```

```
ip dhcp excluded-address 192.10.100.1
ip dhcp excluded-address 192.10.100.9
ip dhcp excluded-address 192.10.100.17
ip dhcp excluded-address 192.10.100.25
ip dhcp excluded-address 192.10.100.33
ip dhcp excluded-address 192.10.100.41
```

```
ip dhcp pool reparacion
network 192.10.100.0 255.255.255.248
default-router 192.10.100.1
dns-server 192.60.100.34
option 150 ip 192.10.100.1
exit

ip dhcp pool ventas
network 192.10.100.8 255.255.255.248
default-router 192.10.100.9
dns-server 192.60.100.34
option 150 ip 192.10.100.9
exit

ip dhcp pool publicidad
network 192.10.100.16 255.255.255.248
default-router 192.10.100.17
dns-server 192.60.100.34
option 150 ip 192.10.100.17
exit

ip dhcp pool administracion
network 192.10.100.24 255.255.255.248
default-router 192.10.100.25
dns-server 192.60.100.34
option 150 ip 192.10.100.25
exit

ip dhcp pool voz       
Network 192.10.100.32 255.255.255.248
default-router 192.10.100.33
dns-server 192.60.100.34
option 150 ip 192.10.100.33        
exit 
```

```
TELEPHONY-SERVICE
MAX-DN 4
MAX-EPHONES 4
IP SOURCE-ADDRESS 192.10.100.33 PORT 2000
AUTO ASSIGN 1 TO 4
EXIT

EPHONE-DN 1
NUMBER 507500
EXIT

EPHONE-DN 2
NUMBER 507600
EXIT

EPHONE-DN 3
NUMBER 507700
EXIT

EPHONE-DN 4
NUMBER 507800
EXIT
```

```
INTERFACE F0/0
IP ADD 192.10.100.1 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.10.100.9 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.10.100.17 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.10.100.25 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.10.100.33 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.10.100.41 255.255.255.248
NO SHUTDOWN
exit

interface s0/1/1
ip ad 10.11.10.2 255.255.255.252
no shutdown
exit

interface s0/1/0
ip ad 10.11.80.1 255.255.255.252
no shutdown
exit
```

```
router ospf 10
network 10.11.80.0 0.0.0.3 area 0
network 10.11.10.0 0.0.0.3 area 0
network 192.10.100.0 0.0.0.7 area 0
network 192.10.100.8 0.0.0.7 area 0
network 192.10.100.16 0.0.0.7 area 0
network 192.10.100.24 0.0.0.7 area 0
network 192.10.100.32 0.0.0.7 area 0
network 192.10.100.40 0.0.0.7 area 0
exit
```

```
int lo2
ip ad 195.100.10.0 255.255.255.255
exit
```

```
int s0/1/0
bandwidth 128
exit
```

### SWITCHs
```
vlan 17
name reparacion
exit

vlan 27
name ventas
exit

vlan 37
name publicidad
exit

vlan 47
name administracion
exit

vlan 57
name voz
exit

vlan 99
name nativa
exit
```

```
int range fa0/1-5
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 47
exit

int range fa0/6-10
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 37
exit

int range fa0/11-15
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 27
exit

int range fa0/16-21
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 17
exit

int range fa0/1-21  
switchport mode access
switchport voice vlan 57  
exit

int range fa0/22-24
SWITCHPORT MODE TRUNK
SWITCHPORT TRUNK NATIVE vlan 99
exit
```

