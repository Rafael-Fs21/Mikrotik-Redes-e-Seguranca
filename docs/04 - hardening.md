# 04 - Hardening (Segurança)

Não coloque um MikroTik em produção sem estes passos.

## 1. Usuários e Senhas
O usuário `admin` sem senha é o maior vetor de invasões.
1. Vá em `System` ➔ `Users`.
2. Crie um novo usuário (`+`), defina o grupo como `full` e crie uma senha forte.
3. Desconecte do WinBox e logue com o usuário novo.
4. Desative ou apague o usuário padrão `admin` antigo.

## 2. Desativar Serviços Inseguros
A MikroTik vem com Telnet, FTP e Web rodando por padrão.
1. Vá em `IP` ➔ `Services`.
2. Desative (clique no "X") tudo que não usar: `api`, `api-ssl`, `ftp`, `telnet`, `www`, `www-ssl`.
3. Deixe apenas o `winbox` ativo. Se possível, restrinja o campo **Available From** apenas para a sua sub-rede local (`192.168.10.0/24`).

## 3. Proteção no Acesso por MAC (MAC Server)
Por padrão, qualquer porta física permite tentar acesso via MAC ao roteador.
1. Vá em `Tools` ➔ `MAC Server`.
2. Na aba `MAC WinBox Server` e `MAC Telnet Server`, clique em `MAC WinBox Interfaces`.
3. Mude de `all` para a lista de interfaces locais, ou apenas `bridge-lan`. Nunca deixe habilitado na `ether1` (WAN).

## 4. Descoberta de Rede (Neighbor Discovery)
Evita que seu roteador fique "gritando" na porta WAN que ele é um MikroTik.
1. Vá em `IP` ➔ `Neighbor` ➔ aba `Discovery Settings`.
2. Em **Interface**, escolha apenas a `bridge-lan` ou crie uma lista apenas com as portas locais.

## 5. Atualização de Firmware
Mantenha o RouterOS atualizado para corrigir falhas.
1. Vá em `System` ➔ `Packages` ➔ `Check For Updates`.
2. Se houver atualização, clique em `Download & Install`.

## 6. Backup Regular
Sempre faça backup antes de mudar regras de firewall ou roteamento!
* **Backup binário (restaura no mesmo equipamento):** `Files` ➔ `Backup`.
* **Backup texto (exportar regras):** Abra o `New Terminal` e digite: `export file=meubackup`.
