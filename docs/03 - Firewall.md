# 03 - Firewall Básico

Um roteador sem firewall é um alvo aberto. A MikroTik usa as *chains*: **Input** (tráfego destinado ao roteador) e **Forward** (tráfego passando pelo roteador).

Vá em `IP` ➔ `Firewall` ➔ aba `Filter Rules` e adicione as regras na ordem abaixo:

## Regras de INPUT (Protegendo o Roteador)

1. **Aceitar tráfego estabelecido/relacionado**
   * *General:* Chain = `input` | Connection State = `established`, `related`
   * *Action:* `accept`
2. **Dropar pacotes inválidos**
   * *General:* Chain = `input` | Connection State = `invalid`
   * *Action:* `drop`
3. **Aceitar ICMP (Ping)** (Opcional, mas recomendado)
   * *General:* Chain = `input` | Protocol = `icmp`
   * *Action:* `accept`
4. **Bloquear tudo que vem da WAN** (Importante!)
   * *General:* Chain = `input` | In. Interface = `ether1`
   * *Action:* `drop`

## Regras de FORWARD (Protegendo a Rede Interna)

5. **Aceitar tráfego estabelecido/relacionado na LAN**
   * *General:* Chain = `forward` | Connection State = `established`, `related`
   * *Action:* `accept`
6. **Dropar pacotes inválidos na LAN**
   * *General:* Chain = `forward` | Connection State = `invalid`
   * *Action:* `drop`
7. **Bloquear tráfego da WAN para a LAN (exceto redirecionamentos/DstNAT)**
   * *General:* Chain = `forward` | In. Interface = `ether1` | Connection NAT State = `!dstnat` (marque a caixinha "!" para negar)
   * *Action:* `drop`

## Redirecionamento de Portas (Port Forwarding / DstNAT)
Se precisar expor um DVR, servidor Web ou jogo:
1. Vá em `IP` ➔ `Firewall` ➔ aba `NAT` ➔ clique no `+`.
2. *General:* Chain = `dstnat` | Protocol = `tcp` | Dst. Port = `(Porta externa, ex: 8080)` | In. Interface = `ether1`.
3. *Action:* Action = `dst-nat` | To Addresses = `(IP Interno, ex: 192.168.10.50)` | To Ports = `(Porta interna, ex: 80)`.
