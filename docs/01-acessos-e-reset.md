# 01 - Acesso e Reset

Antes de começar a configurar, é fundamental garantir acesso limpo ao equipamento.

## 1. Primeiro Acesso via WinBox
1. Baixe o **WinBox** no site oficial da MikroTik.
2. Conecte o cabo de rede do seu PC em qualquer porta (geralmente da `ether2` em diante).
3. Abra o WinBox, vá na aba **Neighbors**. O roteador deve aparecer na lista.
4. Clique no **MAC Address** (acesso por camada 2, ideal quando o roteador não tem IP).
5. **Login padrão:** `admin` | **Senha:** `(em branco)`
6. Clique em **Connect**.

## 2. Reset de Fábrica (Pelo WinBox)
Para começar do zero, precisamos limpar as configurações padrão da MikroTik:
1. Vá em `System` ➔ `Reset Configuration`.
2. Marque a opção: **No Default Configuration** (Isso evita que a MikroTik aplique regras genéricas).
3. (Opcional) Marque **Do Not Backup**.
4. Clique em **Reset Configuration** e confirme. O roteador vai reiniciar zerado.

## 3. Reset Físico (Hard Reset)
Se você perdeu o acesso ao roteador:
1. Desligue o roteador da energia.
2. Pressione e segure o botão **RES / RESET**.
3. Ligue o roteador na energia **continuando a segurar o botão**.
4. Espere a luz `ACT` ou `USR` começar a piscar (cerca de 5 a 10 segundos) e solte o botão.
5. O roteador voltará aos padrões de fábrica (IP `192.168.88.1`).
