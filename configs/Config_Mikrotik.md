# Configuração MikroTik — VLAN 30 (pfSense)

## Bridge

```bash
/interface bridge
add name=bridge1
```

Esse comando cria um switch virtual (camada 2) dentro do MikroTik para conexão de interfaces.

```bash
/interface bridge port
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=ether3
```

Adiciona à bridge `bridge1` as interfaces **ether2** (conectada aos clientes) e **ether3** (conectada ao switch-core, com a porta configurada na VLAN 30 — Visitantes). Dessa forma, o tráfego da VLAN 30 entra no MikroTik pela interface **ether3**, é processado na bridge e distribuído para os dispositivos conectados à **ether2**. Na prática, isso faz com que o MikroTik funcione como um **ponto de acesso Layer 2**, estendendo a VLAN 30 aos clientes — simulando o comportamento de uma rede sem fio.


```bash
/ip address
add address=192.168.30.2/24 interface=bridge1 network=192.168.30.0
```

Esse comando atribui um endereço IP estático à interface `bridge1`, colocando o MikroTik na mesma sub-rede da VLAN 30. Dessa forma, o equipamento passa a participar da rede como um host com IP fixo, enquanto os dispositivos clientes continuam obtendo endereços IP dinamicamente via DHCP fornecido pelo pfSense na VLAN 30.