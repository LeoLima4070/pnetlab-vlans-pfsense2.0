# Configuração switch de acesso VLAN 40 Servidores

```bash
vlan 40
name Servidores
```
**Cria VLAN 40 (Servidores)**

```bash
interface Ethernet0/0
 no shutdown
 switchport access vlan 40
 switchport mode access
```
Configura a interface **Ethernet0/0** conectada ao switch core como **access** na VLAN 40

```bash
interface Ethernet0/1
 no shutdown
 switchport access vlan 40
 switchport mode access
```

```bash
interface Ethernet0/2
 no shutdown
 switchport access vlan 40
 switchport mode access
```

Configura as interfaces **Ethernet0/1** e **Ethernet0/2** conectadas aos hosts da VLAN Servidores como modo **acess** na VLAN 20
