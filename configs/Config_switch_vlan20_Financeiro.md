# Configuração switch de acesso VLAN 20 Financeiro

```bash
vlan 20
name Financeiro
```
**Cria VLAN 20 (Financeiro)**

```bash
interface Ethernet0/1
 no shutdown
 switchport access vlan 20
 switchport mode access
```

```bash
interface Ethernet0/2
 no shutdown
 switchport access vlan 20
 switchport mode access
```

Configura as interfaces **Ethernet0/1** e **Ethernet0/2** conectadas aos hosts da VLAN Financeiro como modo **acess** na VLAN 20

```bash
interface Ethernet1/0
 no shutdown
 switchport access vlan 20
 switchport mode access
```
Configura a interface **Ethernet1/0** conectada ao switch core como **access** na VLAN 20

