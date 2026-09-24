# 02 - Configuração Básica

Com o roteador zerado, vamos colocar a rede no ar. Acessando pelo WinBox via MAC Address:

## 1. Identificação (Identity)
Nomeie seu roteador para facilitar a identificação na rede.
* Vá em `System` ➔ `Identity` e digite o nome (ex: `MK-Borda`).

## 2. Criação da Bridge (LAN)
A Bridge agrupa as portas físicas para agirem como um switch.

> ⚠️ **AVISO CRÍTICO - RISCO DE PERDA DE ACESSO:** 
> **NUNCA** adicione a `ether1` (ou a porta que recebe a conexão principal do provedor) na Bridge. Se você fizer isso, o sistema cai instantaneamente, o WinBox desconecta e não conecta mais. Caso isso aconteça, será necessário fazer um reset físico no equipamento e começar tudo de novo. 
> **A Bridge é exclusivamente para as portas da LAN!**

1. Vá em `Bridge` ➔ Aba `Bridge` ➔ clique no `+`. Nome: `bridge-lan` ➔ **OK**.
2. Vá na aba `Ports` ➔ clique no `+`.
3. Adicione as interfaces `ether2`, `ether3`, `ether4` e `ether5`, selecionando a `bridge-lan` para todas.

## 3. Configuração de IP Local (LAN)
1. Vá em `IP` ➔ `Addresses` ➔ clique no `+`.
2. **Address:** `192.168.10.1/24`
3. **Interface:** `bridge-lan` ➔ **OK**.

## 4. Configuração da WAN (Internet)
**Se o provedor entrega IP via DHCP:**
1. Vá em `IP` ➔ `DHCP Client` ➔ clique no `+`.
2. **Interface:** `ether1`. Deixe marcados `Use Peer DNS` e `Use Peer NTP`.
3. Certifique-se de que `Add Default Route` está como `yes` ➔ **OK**.

*Nota: Se o provedor entrega IP Fixo, configure-o em `IP > Addresses` (na ether1) e adicione a rota em `IP > Routes` (Dst: 0.0.0.0/0, Gateway: IP_do_provedor).*

## 5. Configuração de DNS
1. Vá em `IP` ➔ `DNS`.
2. Em **Servers**, adicione DNS públicos (ex: `8.8.8.8` e `1.1.1.1`).
3. Marque a caixa **Allow Remote Requests** (crucial para o DHCP da LAN funcionar) ➔ **OK**.

## 6. Servidor DHCP (Para a LAN)
Para os dispositivos pegarem IP automaticamente:
1. Vá em `IP` ➔ `DHCP Server` ➔ clique no botão **DHCP Setup**.
2. **Interface:** `bridge-lan` ➔ *Next*.
3. **DHCP Address Space:** `192.168.10.0/24` ➔ *Next*.
4. **Gateway:** `192.168.10.1` ➔ *Next*.
5. **Addresses to Give Out:** `192.168.10.10-192.168.10.254` ➔ *Next*.
6. **DNS Servers:** `192.168.10.1` (o próprio roteador) ou públicos ➔ *Next* até concluir.

## 7. NAT (Masquerade)
Para a rede interna acessar a internet:
1. Vá em `IP` ➔ `Firewall` ➔ aba `NAT` ➔ clique no `+`.
2. Aba **General**: `Chain = srcnat` | `Out. Interface = ether1`.
3. Aba **Action**: `Action = masquerade` ➔ **OK**.

**Neste ponto, quem conectar nas portas 2 a 5 já deve ter internet!**
