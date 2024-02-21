# MANAGUA
### ROUTER
[un servidor en] -> `administracion`
```
int f0/0
no shutdown
exit

int f0/0.11
encapsulation dot1q 11
ip add 192.40.100.1 255.255.255.248
exit

int f0/0.21
encapsulation dot1q 21
ip add 192.40.100.9 255.255.255.248
exit

int f0/0.31  
encapsulation dot1q 31 
ip add 192.40.100.17 255.255.255.248
exit 

int f0/0.41  
encapsulation dot1q 41 
ip add 192.40.100.25 255.255.255.248
exit 

int f0/0.51  
encapsulation dot1q 51 
ip add 192.40.100.33 255.255.255.248
exit 

int f0/0.99    
encapsulation dot1q 99 native  
ip add 192.40.100.41 255.255.255.248
exit 
```

```
ip dhcp excluded-address 192.40.100.1
ip dhcp excluded-address 192.40.100.9
ip dhcp excluded-address 192.40.100.17
ip dhcp excluded-address 192.40.100.25
ip dhcp excluded-address 192.40.100.33
ip dhcp excluded-address 192.40.100.41
ip dhcp excluded-address 192.40.100.26
```

```
ip dhcp pool reparacion
network 192.40.100.0 255.255.255.248
default-router 192.40.100.1
dns-server 192.60.100.34
option 150 ip 192.40.100.1
exit

ip dhcp pool ventas
network 192.40.100.8 255.255.255.248
default-router 192.40.100.9
dns-server 192.60.100.34
option 150 ip 192.40.100.9
exit

ip dhcp pool publicidad
network 192.40.100.16 255.255.255.248
default-router 192.40.100.17
dns-server 192.60.100.34
option 150 ip 192.40.100.17
exit

ip dhcp pool administracion
network 192.40.100.24 255.255.255.248
default-router 192.40.100.25
dns-server 192.60.100.34
option 150 ip 192.40.100.25
exit

ip dhcp pool voz       
Network 192.40.100.32 255.255.255.248
default-router 192.40.100.33
dns-server 192.60.100.34
option 150 ip 192.40.100.33        
exit 
```

```
TELEPHONY-SERVICE
MAX-DN 4
MAX-EPHONES 4
IP SOURCE-ADDRESS 192.40.100.33 PORT 2000
AUTO ASSIGN 1 TO 4
EXIT

EPHONE-DN 1
NUMBER 505500
EXIT

EPHONE-DN 2
NUMBER 505600
EXIT

EPHONE-DN 3
NUMBER 505700
EXIT

EPHONE-DN 4
NUMBER 505800
EXIT
```

```
INTERFACE F0/0
IP ADD 192.40.100.1 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.40.100.9 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.40.100.17 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.40.100.25 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.40.100.33 255.255.255.248
NO SHUTDOWN
exit

INTERFACE F0/0
IP ADD 192.40.100.41 255.255.255.248
NO SHUTDOWN
exit

interface s0/0/0
ip ad 10.11.70.1 255.255.255.252
no shutdown
exit

interface s0/0/1
ip ad 10.11.90.1 255.255.255.252
no shutdown
exit
```

```
ROUTER RIP
VERSION 2
NETWORK 10.11.90.0
NETWORK 10.11.70.0
NETWORK 10.11.50.0
NETWORK 192.40.100.0
NETWORK 192.40.100.8
NETWORK 192.40.100.16
NETWORK 192.40.100.24
NETWORK 192.40.100.32
NETWORK 192.40.100.40
NETWORK 12.11.40.0
EXIT
```

### SWITCHs
[un servidor en] -> `administracion`
```
vlan 11
name reparacion
exit

vlan 21
name ventas
exit

vlan 31
name publicidad
exit

vlan 41
name administracion
exit

vlan 51
name voz
exit

vlan 99
name nativa
exit
```

```
int range fa0/1-5
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 41
exit

int range fa0/6-10
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 31
exit

int range fa0/11-15
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 21
exit

int range fa0/16-21
SWITCHPORT MODE ACCESS
SWITCHPORT ACCESS vlan 11
exit

int range fa0/1-21  
switchport mode access
switchport voice vlan 51 
exit

int range fa0/22-24
SWITCHPORT MODE TRUNK
SWITCHPORT TRUNK NATIVE vlan 99
exit
```