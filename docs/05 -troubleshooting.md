# 05 - Troubleshooting (Resolução de Problemas)

## 1. Perda total de acesso (WinBox não conecta de jeito nenhum)
* **Causa Comum:** Você acidentalmente adicionou a porta da WAN (ex: `ether1`) dentro da Bridge LAN. Isso derruba o acesso na hora.
* **Solução:** Como o sistema não conecta mais via rede, é necessário realizar o **Reset Físico (Hard Reset)** (segurando o botão no equipamento enquanto liga na energia) e recomeçar a configuração do zero. Lembre-se: a Bridge só deve conter as portas da rede interna.

## 2. Não consigo acessar via WinBox pelo IP
* **Causa:** Regra de firewall bloqueando ou IP incorreto na placa de rede do seu PC.
* **Solução:** Acesse via MAC Address pelo WinBox (aba Neighbors) e revise as regras de `IP > Firewall > Filter Rules` na chain `input`.

## 3. Os dispositivos conectam, mas não navegam (Sem Internet)
Siga este checklist:
1. **O roteador tem internet?** Vá em `New Terminal` e faça `ping 8.8.8.8`. Se falhar, o problema é na WAN (DHCP Client sem IP, Rota não criada, etc).
2. **O NAT está criado?** Verifique se a regra `masquerade` está na aba NAT em `IP > Firewall`.
3. **O DHCP Server está entregando DNS?** Veja em `IP > DHCP Server > Networks` se o campo DNS Server está preenchido com `192.168.10.1` ou o DNS do Google.
4. **Allow Remote Requests:** Em `IP > DNS`, a caixa "Allow Remote Requests" deve estar marcada.

## 4. Loop na Bridge / Rede muito lenta
* **Causa:** Cabos ligados incorretamente gerando loop físico de switch.
* **Solução:** Vá em `Bridge`, dê duplo clique na sua bridge e certifique-se de que o protocolo `RSTP` está habilitado na aba STP.

## 5. Ferramentas Integradas Úteis
* **Ping / Traceroute:** Ficam no menu `Tools`.
* **Torch:** Em `Tools > Torch`. Permite ver o tráfego em tempo real passando por uma interface (ideal para ver quem está consumindo banda ou derrubando a rede).
* **Logs:** Em `Log`. Fique de olho em mensagens de erro vermelhas.
