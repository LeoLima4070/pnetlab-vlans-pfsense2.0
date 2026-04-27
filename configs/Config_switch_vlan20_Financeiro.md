vlan 20
name Financeiro

interface Ethernet0/1
 no shutdown
 switchport access vlan 20
 switchport mode access

interface Ethernet0/2
 no shutdown
 switchport access vlan 20
 switchport mode access

interface Ethernet0/3
 no shutdown

interface Ethernet1/0
 no shutdown
 switchport access vlan 20
 switchport mode access
