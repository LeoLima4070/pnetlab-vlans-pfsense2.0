# Configuração switch de acesso VLAN 10 TI

```bash
vlan 10
name TI
```
**Cria VLAN 10 (TI)**

```bash
interface Ethernet0/1
 no shutdown
 switchport access vlan 10
 switchport mode access
```

```bash
interface Ethernet0/2
 no shutdown
 switchport access vlan 10
 switchport mode access
```
Configura as interfaces **Ethernet0/1** e **Ethernet0/2** conectadas aos hosts da VLAN TI como modo **acess** na VLAN 10

```bash
interface Ethernet0/3
 no shutdown
 switchport access vlan 10
 switchport mode access
 ```
 
Configura a interface **Ethernet0/3** conectada ao switch core como **access** na VLAN 10
