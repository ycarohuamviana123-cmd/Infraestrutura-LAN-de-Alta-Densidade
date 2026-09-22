# Infraestrutura-LAN-de-Alta-Densidade

# Projeto de Infraestrutura de Rede – GlobalCorp

#Orientador
Hudson Neves 


#Instituição 
(Uniceplac) Centro Universitário do Planalto Central Apparecido dos Santos

## Identificação do Grupo

Davi Santana Alves Alecrim

Ian Victor Viana de Jesus

Ícaro Ruan Viana de Jesus

Lucas Gabriel Alves de Souza

Luiza Silva Freitas Hortelão

---

# Descrição do Cenário

A **GlobalCorp** é uma empresa que necessita de uma infraestrutura de rede corporativa capaz de conectar computadores, dispositivos móveis e servidores, permitindo comunicação entre os diferentes equipamentos da organização.

O projeto foi desenvolvido no **Cisco Packet Tracer**, utilizando uma estrutura de rede composta por equipamentos de camada 3 e camada 2, conexão cabeada, rede sem fio e servidores locais.

A infraestrutura possui um **Multilayer Switch** central responsável pelo roteamento e pelo Gateway Padrão da rede. Os **Switches de acesso** conectam os computadores e servidores, enquanto um **WRT300N** disponibiliza a rede Wi-Fi para notebooks e smartphones.

Também foram configurados serviços de **DHCP, DNS e HTTP**, permitindo que os dispositivos obtenham configurações de rede automaticamente, resolvam o domínio da empresa e acessem sua página institucional.

A comunicação da rede é validada por meio de testes de conectividade, acesso ao servidor Web e resolução do domínio `globalcorp.com`.

---

# Objetivos

O projeto tem como objetivo desenvolver e demonstrar uma infraestrutura de rede corporativa funcional, permitindo:

* Comunicação entre os dispositivos da empresa;
* Conexão de computadores por rede cabeada;
* Conexão de notebooks e smartphones por Wi-Fi;
* Distribuição automática de endereços IP através do DHCP;
* Resolução de nomes utilizando o DNS;
* Hospedagem de uma página institucional através do servidor HTTP;
* Comunicação entre diferentes segmentos da rede;
* Roteamento através do equipamento de camada 3;
* Validação da conectividade através de testes ICMP;
* Demonstração da disponibilidade e funcionamento dos serviços de rede.

---

# Topologia da Rede

A infraestrutura foi organizada de forma hierárquica.

### Núcleo/Distribuição

* 1 Multilayer Switch;
* Responsável pelo roteamento da rede;
* Gateway Padrão: `192.168.20.1`.

### Acesso Cabeado

* Switch0;
* Switch1;
* Computadores de mesa;
* Servidores locais.

### Acesso Sem Fio

* WRT300N;
* Notebooks;
* Smartphones;
* SSID: `GlobalCorp_LAN_Wifi`.

### Servidores

* **Server0:** servidor Web/HTTP;
* **Server1:** servidor DNS.

---

# Tabela de Endereçamento IP

A rede principal utiliza a faixa privada `192.168.20.0/24`.

| Dispositivo/Serviço | Função               | Endereço IP      | Máscara         | Gateway        |
| ------------------- | -------------------- | ---------------- | --------------- | -------------- |
| Multilayer Switch   | Gateway/Roteamento   | `192.168.20.1`   | `255.255.255.0` | —              |
| Server0             | Servidor Web/HTTP    | `192.168.20.14`  | `255.255.255.0` | `192.168.20.1` |
| Server1             | Servidor DNS         | `192.168.20.250` | `255.255.255.0` | `192.168.20.1` |
| PCs                 | Estações de trabalho | DHCP             | `255.255.255.0` | `192.168.20.1` |
| Notebooks           | Dispositivos Wi-Fi   | DHCP             | `255.255.255.0` | `192.168.20.1` |
| Smartphones         | Dispositivos Wi-Fi   | DHCP             | `255.255.255.0` | `192.168.20.1` |

**Rede:** `192.168.20.0/24`
**Máscara:** `255.255.255.0`
**Gateway:** `192.168.20.1`

---

# VLANs e Segmentação

A estrutura utiliza equipamentos de acesso conectados ao equipamento central de camada 3.

Caso sejam utilizadas VLANs na configuração final do projeto, elas podem ser verificadas através do seguinte comando no switch:

```bash
enable
show vlan brief
```

Para verificar interfaces configuradas como trunk:

```bash
show interfaces trunk
```

> **Observação:** os IDs e nomes das VLANs devem corresponder exatamente à configuração existente no arquivo `.pkt`.

---

# Configuração da Rede Wi-Fi

A rede sem fio é disponibilizada pelo roteador **WRT300N**.

| Configuração       | Valor                   |
| ------------------ | ----------------------- |
| Equipamento        | WRT300N                 |
| SSID               | `GlobalCorp_LAN_Wifi`   |
| Autenticação       | Aberta                  |
| Distribuição de IP | DHCP                    |
| Dispositivos       | Notebooks e smartphones |

Os dispositivos móveis podem se associar à rede e receber automaticamente suas configurações de endereço IP.

---

# Serviços de Rede

## DHCP

O DHCP é utilizado para fornecer automaticamente as configurações de rede aos dispositivos configurados para obtenção dinâmica de endereço.

Os parâmetros recebidos podem incluir:

* Endereço IP;
* Máscara de sub-rede;
* Gateway;
* Servidor DNS.

---

## Servidor Web

O **Server0** funciona como servidor HTTP.

**Endereço IP:**

```text
192.168.20.14
```

A página institucional apresenta a mensagem:

> Bem-vindo à GlobalCorp!.
> Opening doors to new opportunities.
> Mind Wide Open.

O servidor pode ser acessado diretamente pelo endereço:

```text
http://192.168.20.14
```

---

##  Servidor DNS

O **Server1** é responsável pela resolução de nomes.

**Endereço IP:**

```text
192.168.20.250
```

Foi configurado um registro do tipo **A Record**:

```text
globalcorp.com → 192.168.20.14
```

Dessa forma, o servidor Web pode ser acessado através do domínio:

```text
http://globalcorp.com
```

---

# Guia de Testes de Validação

Esta seção apresenta o procedimento para reproduzir os principais testes no Cisco Packet Tracer.

##  Teste de DHCP

### Passo 1

Selecione um computador da rede.

### Passo 2

Acesse:

```text
Desktop → IP Configuration
```

### Passo 3

Selecione:

```text
DHCP
```

### Passo 4

Verifique se o computador recebeu automaticamente:

* Endereço IP;
* Máscara;
* Gateway;
* DNS.

### Passo 5

Abra:

```text
Desktop → Command Prompt
```

Execute:

```bash
ipconfig
```

O comando deve apresentar as informações de rede recebidas pelo computador.

---

# Teste de Conectividade com o Servidor Web

### Passo 1

Em um computador, abra:

```text
Desktop → Command Prompt
```

### Passo 2

Execute:

```bash
ping 192.168.20.14
```

### Resultado esperado

O servidor deve responder às solicitações ICMP.

O resultado esperado é:

```text
Packets: Sent = 4, Received = 4, Lost = 0
```

Isso representa **0% de perda de pacotes**.

---

# Teste do Servidor Web pelo IP

### Passo 1

Em um computador, abra:

```text
Desktop → Web Browser
```

### Passo 2

Digite:

```text
http://192.168.20.14
```

### Passo 3

Pressione Enter.

### Resultado esperado

A página institucional da GlobalCorp deve ser carregada corretamente.

---

# Teste do DNS e do Domínio

### Passo 1

Abra o navegador de um computador:

```text
Desktop → Web Browser
```

### Passo 2

Digite:

```text
http://globalcorp.com
```

### Passo 3

Pressione Enter.

### Resultado esperado

O domínio deve ser resolvido pelo servidor DNS e a página hospedada no endereço `192.168.20.14` deve ser apresentada.

---

# Teste de DNS pelo Prompt de Comando

Também pode ser realizada uma verificação através do comando:

```bash
ping globalcorp.com
```

O domínio deverá ser associado ao endereço:

```text
192.168.20.14
```

Isso permite verificar a integração entre o serviço DNS e o servidor Web.

---

# Teste de VLAN e Roteamento Inter-VLAN

Caso existam VLANs configuradas no projeto, o funcionamento pode ser verificado através da comunicação entre dispositivos pertencentes a segmentos diferentes.

### Passo 1

No switch, verificar as VLANs:

```bash
enable
show vlan brief
```

### Passo 2

Verificar as interfaces trunk, caso utilizadas:

```bash
show interfaces trunk
```

### Passo 3

Em um computador de uma VLAN, abrir:

```text
Desktop → Command Prompt
```

### Passo 4

Executar:

```bash
ping IP_DO_DISPOSITIVO_DE_OUTRA_VLAN
```

### Resultado esperado

O dispositivo deverá receber respostas do equipamento pertencente ao outro segmento.

No equipamento de camada 3 também pode ser utilizado:

```bash
show ip route
```

para verificar as rotas disponíveis.

---

# Verificação do Roteamento

No equipamento responsável pelo roteamento, executar:

```bash
enable
show ip route
```

O comando permite visualizar as redes conhecidas pelo equipamento e as rotas utilizadas para encaminhamento dos pacotes.

---

# Arquivo do Projeto

O arquivo principal deste repositório é:

```text
Projeto_Redes_Grupo_Final.pkt
```

Para executar o projeto:

1. Instale o **Cisco Packet Tracer**;
2. Baixe o arquivo `.pkt` deste repositório;
3. Abra o arquivo no Cisco Packet Tracer;
4. Aguarde o carregamento da topologia;
5. Verifique os dispositivos e conexões;
6. Execute os testes descritos neste README.

---

# Conclusão

O projeto apresenta uma infraestrutura de rede corporativa simulada para a GlobalCorp, integrando equipamentos cabeados, rede Wi-Fi e servidores de aplicação.

Através dos testes realizados, é possível verificar a distribuição de endereços por DHCP, a resolução de nomes pelo DNS, o funcionamento do servidor HTTP e a comunicação entre os dispositivos da rede.

A utilização do Cisco Packet Tracer permite simular e validar o funcionamento da infraestrutura antes de uma eventual implementação em ambiente real.
