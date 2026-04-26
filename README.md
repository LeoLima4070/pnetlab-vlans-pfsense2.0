# Projeto de Redes com pfSense

Este projeto tem como objetivo a prática e o aprimoramento de conhecimentos em redes de computadores utilizando o **pfSense**. O foco principal é a implementação de **VLANs** e a criação de **regras básicas de firewall**, permitindo a segmentação da rede e o controle de tráfego entre diferentes setores.

---

## Topologia

![Topologia da rede](topologia/topologia.png)

A rede foi estruturada com um **switch core** como elemento central, responsável por interligar:

- 3 switches de acesso  
- 1 dispositivo MikroTik (simulando uma rede sem fio)

O switch core concentra e gerencia as seguintes VLANs:

- **VLAN 10 – TI**
- **VLAN 20 – Financeiro**
- **VLAN 30 – Visitantes**
- **VLAN 40 – Servidores**

Cada switch de acesso atende a uma VLAN específica (TI, Financeiro e Servidores). A **VLAN de Visitantes** está conectada ao **MikroTik**, sendo utilizada para simular uma rede sem fio e garantir o isolamento de dispositivos externos em relação à rede interna.

---

## Tecnologias utilizadas

- pfSense  
- VLANs (802.1Q)  
- MikroTik (simulação de rede sem fio)  
- PNETLab  
- Switches gerenciáveis  

---

## Endereçamento IP

| Interface            | Rede / IP           | Descrição                    |
|----------------------|---------------------|------------------------------|
| WAN                  | 192.168.112.134/24  | Conectado via NAT no PNETLab |
| LAN                  | 192.168.1.1/24      | Interface interna do pfSense |
| VLAN 10 (TI)         | 192.168.10.0/24     | Setor TI                     |
| VLAN 20 (Financeiro) | 192.168.20.0/24     | Setor Financeiro             |
| VLAN 30 (Visitantes) | 192.168.30.0/24     | Rede de visitantes           |
| VLAN 40 (Servidores) | 192.168.40.0/24     | Servidores                   |

> Cada VLAN está associada a uma interface virtual no pfSense. O tráfego entre VLANs é controlado por regras de firewall.

---

## Configuração do Switch Core

No switch core foram criadas 4 VLANs com os seguintes IDs:

- VLAN 10 – TI  
- VLAN 20 – Financeiro  
- VLAN 30 – Visitantes  
- VLAN 40 – Servidores  

A interface que conecta o switch core ao **pfSense** foi configurada em modo **trunk (802.1Q)**, permitindo o tráfego de múltiplas VLANs através de uma única porta.

Essa configuração permite que o pfSense realize o roteamento entre VLANs e aplique as regras de firewall de forma centralizada.

---

## Configuração dos Switches de Acesso

Nos switches de acesso foi criada apenas a VLAN correspondente a cada setor:

- Switch de TI → VLAN 10  
- Switch de Financeiro → VLAN 20  
- Switch de Servidores → VLAN 40  

As portas foram configuradas em modo **access**, garantindo que cada dispositivo pertença exclusivamente à sua VLAN.

---

## Configuração do MikroTik

O MikroTik foi utilizado para simular uma rede sem fio no ambiente, devido à limitação do PNETLab, que não possui suporte nativo a dispositivos wireless.

Não há configuração de VLAN diretamente no MikroTik. A segmentação é realizada no switch core, que entrega a VLAN de visitantes (VLAN 30) já tratada.

O MikroTik está conectado ao switch core por uma porta configurada em modo **access**, associada à VLAN de visitantes. A interface possui um IP fixo configurado localmente para gerenciamento.

Internamente, foi utilizada uma bridge para interligar as interfaces físicas, permitindo comunicação em camada 2 entre os dispositivos conectados.

Os dispositivos conectados ao MikroTik recebem IP via DHCP diretamente do pfSense.

O MikroTik atua apenas como dispositivo de camada 2, sem roteamento ou filtragem.

---

## Integração com o Switch Core

As portas do switch core conectadas aos switches de acesso foram configuradas em modo **access**, cada uma associada à sua respectiva VLAN:

- TI → VLAN 10  
- Financeiro → VLAN 20  
- Servidores → VLAN 40  

A VLAN de Visitantes (VLAN 30) está conectada ao MikroTik.

---

## Configuração do pfSense

No pfSense foram criadas as VLANs na interface trunk conectada ao switch core.

Para cada VLAN foi criada uma interface lógica e um servidor DHCP:

- VLAN 10 – TI  
- VLAN 20 – Financeiro  
- VLAN 30 – Visitantes  
- VLAN 40 – Servidores  

O pfSense é responsável por:
- Roteamento entre VLANs  
- Distribuição de IP (DHCP)  
- Aplicação das regras de firewall  

---

## Políticas de Firewall

As regras seguem o princípio de **negação por padrão (default deny)** e **menor privilégio**.

- TI: acesso administrativo e diagnóstico  
- Financeiro: acesso controlado à internet e servidores  
- Visitantes: apenas internet  
- Servidores: acesso restrito e controlado  

---

## Conclusão

Este projeto foi desenvolvido com o objetivo de praticar e consolidar conhecimentos em redes, principalmente na criação de VLANs, segmentação de rede e configuração de regras de firewall no pfSense.

Apesar de ser um ambiente simples, ele representa cenários comuns do dia a dia, como separação de setores, controle de acesso e isolamento de redes.

A ideia principal foi aplicar na prática os conceitos estudados e entender como esses componentes funcionam em conjunto em uma rede real.

---

## Autor

**Leandro Lima** – Estudante de Redes
