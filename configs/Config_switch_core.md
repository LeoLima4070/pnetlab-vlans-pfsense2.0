## Criação das VLANs no switchcore e porta trunk

```bash
vlan 10
name TI

vlan 20
name Financeiro

vlan 30
name Visitantes

vlan 40
name Servidores
```
Os comandos acima cria as VLANs no switch-core

## Configuração das interfaces de acesso e interface trunk

```bash
interface Ethernet0/0
no shutdown
switchport access vlan 20
switchport mode access
```
Configura a interface **Ethernet0/0** conectada ao switch de acceso do Financeiro no modo **access** e a associa a VLAN 20 (Financeiro)

```bash
interface Ethernet0/1
no shutdown
switchport trunk allowed vlan 10,20,30,40
switchport trunk encapsulation dot1q
switchport mode trunk
```
Configura a interface **Ethernet0/1** conectada ao pfSense em modo **trunk**, permitindo a passagem de tráfego de todas as VLANs configuradas no switch.

```bash
interface Ethernet0/2
no shutdown
switchport access vlan 30
switchport mode access
```
Configura a interface **Ethernet0/2** no modo **access** conectada ao Mikrotik e a associa a VLAN 30 (Visitantes)

```bash
interface Ethernet0/3
no shutdown
switchport access vlan 10
switchport mode access
```
Configura a interface **Ethernet0/3** no modo **access** conectada ao switch de acesso da TI e a associa a VLAN 10 (TI)

```bash
interface Ethernet1/0
no shutdown
switchport access vlan 40
switchport mode access
```
Configura a interface **Ethernet1/0** no modo **access** conectada ao switch de acesso dos servidores e a associa a VLAN 40 (Servidores)
