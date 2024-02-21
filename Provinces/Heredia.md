# HEREDIA
### ROUTER
[un servidores en] -> `tecnologia`
```
int f0/0
no shutdown
exit

int f0/0.10
encapsulation dot1q 10
ip add 192.60.100.1 255.255.255.248
exit

int f0/0.20
encapsulation dot1q 20
ip add 192.60.100.9 255.255.255.248
exit

int f0/0.30  
encapsulation dot1q 30 
ip add 192.60.100.17 255.255.255.248
exit 

int f0/0.40  
encapsulation dot1q 40 
ip add 192.60.100.25 255.255.255.248
exit 

int f0/0.50  
encapsulation dot1q 50 
ip add 192.60.100.41 255.255.255.248
exit 

int f0/0.60  
encapsulation dot1q 60 
ip add 192.60.100.33 255.255.255.248
exit 

int f0/0.99    
encapsulation dot1q 99 native  
ip add 192.60.100.49 255.255.255.248
exit 
```

```
ip dhcp excluded-address 192.60.100.1
ip dhcp excluded-address 192.60.100.9
ip dhcp excluded-address 192.60.100.17
ip dhcp excluded-address 192.60.100.25
ip dhcp excluded-address 192.60.100.33
ip dhcp excluded-address 192.60.100.34
ip dhcp excluded-address 192.60.100.35
ip dhcp excluded-address 192.60.100.36
ip dhcp excluded-address 192.60.100.41
ip dhcp excluded-address 192.60.100.49
```

```
ip dhcp pool reparacion
network 192.60.100.0 255.255.255.248
default-router 192.60.100.1
dns-server 192.60.100.34
option 150 ip 192.60.100.1
exit

ip dhcp pool ventas
network 192.60.100.8 255.255.255.248
default-router 192.60.100.9
dns-server 192.60.100.34
option 150 ip 192.60.100.9
exit

ip dhcp pool publicidad
network 192.60.100.16 255.255.255.248
default-router 192.60.100.17
dns-server 192.60.100.34
option 150 ip 192.60.100.17
exit

ip dhcp pool administracion
network 192.60.100.24 255.255.255.248
default-router 192.60.100.25
dns-server 192.60.100.34
option 150 ip 192.60.100.25
exit

ip dhcp pool tecnologia
network 192.60.100.32 255.255.255.248
default-router 192.60.100.33
dns-server 192.60.100.34
option 150 ip 192.60.100.33
exit

ip dhcp pool voz       
Network 192.60.100.40 255.255.255.248
default-router 192.60.100.41
dns-server 192.60.100.34
option 150 ip 192.60.100.41       
exit 
```

```
TELEPHONY-SERVICE
MAX-DN 4
MAX-EPHONES 4
IP SOURCE-ADDRESS 192.60.100.41 PORT 2000
AUTO ASSIGN 1 TO 4
EXIT

EPHONE-DN 1
NUMBER 506500
EXIT

EPHONE-DN 2
NUMBER 506600
EXIT

EPHONE-DN 3
NUMBER 506700
EXIT

EPHONE-DN 4
NUMBER 506800
EXIT
```

```
INTERFACE F0/0
IP ADD 192.60.100.1 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.60.100.9 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.60.100.17 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.60.100.25 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.60.100.33 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.60.100.41 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.60.100.49 255.255.255.248
NO SHUTDOWN
exit

interface s0/3/1
ip ad 10.11.30.1 255.255.255.252
no shutdown
exit

interface s0/3/0
ip ad 10.11.60.1 255.255.255.252
no shutdown
exit
```

```
router eigrp 64
NETWORK 10.11.30.0 0.0.0.3
NETWORK 10.11.60.0 0.0.0.3
NETWORK 192.60.100.1 0.0.0.7
NETWORK 192.60.100.9 0.0.0.7
NETWORK 192.60.100.17 0.0.0.7
NETWORK 192.60.100.25 0.0.0.7
NETWORK 192.60.100.33 0.0.0.7
NETWORK 192.60.100.41 0.0.0.7
NETWORK 192.60.100.49 0.0.0.7
NO AUTO -SUMMARY
EXIT
```

### SWITCHs
[un servidores en] -> `tecnoligia`
```
vlan 10
name reparacion
exit

vlan 20
name ventas
exit

vlan 30
name publicidad
exit

vlan 40
name administracion
exit

vlan 50
name voz
exit

vlan 60
name tecnologia
exit

vlan 99
name nativa
exit
```

```
int range fa0/1-4
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 40
exit

int range fa0/5-8
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 30
exit

int range fa0/9-12
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 20
exit

int range fa0/13-16
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 10
exit

int range fa0/1-21  
switchport mode access
switchport voice vlan 50
exit

int range fa0/17-21
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 60
exit

int range fa0/22-24
SWITCHPORT MODE TRUNK
SWITCHPORT TRUNK NATIVE vlan 99
exit
```