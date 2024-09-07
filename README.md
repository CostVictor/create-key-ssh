# Criando uma chave SSH e adicionando ao GitHub
## Sobre o SSH
O SSH (Secure Shell) é um protocolo de rede que permite a comunicação segura entre dois dispositivos por meio de uma conexão criptografada. Ele é amplamente utilizado para acesso remoto a servidores, transferência de arquivos e execução de comandos em sistemas distribuídos.

Esse protocolo foi projetado para substituir métodos inseguros de acesso remoto, como o `Telnet` e `rlogin`, que transmitiam dados (incluindo senhas) em texto puro. Com o SSH, todos os dados são criptografados durante o trânsito, garantindo que mesmo que sejam interceptados, não possam ser lidos sem a chave de decriptação correta.

## Como funciona

O SSH usa criptografia assimétrica para proteger a comunicação. Isso significa que ele utiliza um par de chaves: uma `chave pública` e uma `chave privada`.

- `Chave pública`: usada para criptografar os dados.
- `Chave privada`: usada para descriptografar os dados e é mantida em segredo pelo usuário.

Quando um cliente (como o seu computador) se conecta a um servidor via SSH, as chaves criptográficas são trocadas, garantindo que a comunicação entre o cliente e o servidor seja segura e autêntica.

## Criando uma chave SSH

### 1. Gerando uma nova chave
No terminal, execute o seguinte comando para criar uma nova chave SSH usando o algoritmo RSA de 4096 bits:

```bash
ssh-keygen -t rsa -b 4096 -C "seu_email@exemplo.com"
```

- `-t rsa`: especifica o tipo de chave a ser criada (RSA).
- `-b 4096`: define o tamanho da chave (4096 bits para mais segurança).
- `-C "seu_email@exemplo.com"`: um comentário para identificar sua chave, geralmente seu e-mail.

### 2. Definindo o local de armazenamento da chave
Após executar o comando acima, você verá um prompt para confirmar o local de armazenamento da chave. Por padrão, a chave será salva no diretório `~/.ssh/id_rsa`.

Se quiser usar o local padrão, simplesmente pressione `Enter`.

### 3. Definindo uma senha para a chave
Em seguida, o sistema pedirá para você definir uma senha para proteger sua chave. Você pode optar por deixar esse campo em branco pressionando `Enter`, mas é recomendado criar uma senha forte para aumentar a segurança.

### 4. Iniciando o agente SSH
Antes de adicionar a chave ao agente SSH, é necessário iniciar o `ssh-agent`. Isso pode ser feito com o seguinte comando:

```bash
eval "$(ssh-agent -s)"
```

Este comando inicializa o agente SSH, que gerenciará suas chaves privadas enquanto você estiver logado.

### 5. Adicionando a chave criada ao agente
Agora, adicione a chave privada que você acabou de criar ao ssh-agent com o comando abaixo:

```bash
ssh-add ~/.ssh/id_rsa
```

Se você salvou a chave em um local diferente, altere o caminho `~/.ssh/id_rsa` para o caminho correto.

### 6. Copiando a chave pública
Para adicionar sua chave SSH ao GitHub, você precisará copiar a chave pública gerada. Use o seguinte comando para exibir o conteúdo da sua chave pública:

```bash
cat ~/.ssh/id_rsa.pub
```
O comando mostrará a chave pública no terminal. Copie o conteúdo exibido.
Se você salvou a chave em um local diferente, altere o caminho `~/.ssh/id_rsa` para o caminho correto.

### 7. Adicionando a chave SSH ao GitHub

1. Acesse sua conta do GitHub.
2. Vá para Configurações (Settings).

![Imagem de como chegar nas configurações](image1.png)

3. No menu lateral, clique em SSH and GPG keys.

![Imagem de como chegar nas chaves SSH](image2.png)

4. Clique em New SSH Key.
5. Cole a chave pública copiada no campo `Key` e dê um nome em `Title` para identificar a chave.
6. Clique em Add SSH Key.

### 8. Testando a conexão SSH com o GitHub
Para verificar se a chave foi configurada corretamente, execute o seguinte comando em seu terminal para testar a conexão:

```bash
ssh -T git@github.com
```

Se tudo estiver correto, você verá uma mensagem de sucesso indicando que a autenticação via SSH foi concluída com êxito.
