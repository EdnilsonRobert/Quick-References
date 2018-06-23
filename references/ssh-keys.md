# Chaves SSH | Referência Rápida

## SSH Básico
``` bash
# Cria uma chave SSH
ssh-keygen -t rsa -C "user.name@email.com" -b 4096

# Altera a senha de uma chave
ssh-keygen -p <keyname>
```

## Múltiplas chaves SSH

- Referência: [Múltiple SSH Keys](https://coderwall.com/p/7smjkq/multiple-ssh-keys-for-different-accounts-on-github-or-gitlab)

``` bash
# Apaga todo o diretório .ssh e seu conteúdo
sudo rm -rf .ssh

# Cria chaves SSH com nomes diferentes em arquivos diferentes
ssh-keygen -t rsa -C "user.name@personal_email.com" -b 4096
# Quando solicitado...
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user_name/.ssh/id_rsa):
# Entrar com um nome único para a criação da chave
id_rsa_personal

# Cria nova chave com nome diferente
ssh-keygen -t rsa -C "user.name@company_email.com" -b 4096
# Quando solicitado...
Generating public/private rsa key pair.
Enter file in which to save the key (/home/user_name/.ssh/id_rsa):
# Entrar com um nome único para a criação da chave
id_rsa_company

# Entra no diretório .ssh, cria um arquivo de configuração e abre o arquivo
cd .ssh
touch config
nano config
```

** Arquivo config **
```
# Personal account
Host personal.github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_personal

# Company account
Host company.github.com
  HostName github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_company
```

``` bash
# Apaga chaves em cache
ssh-add -D
# Em caso de erro
eval `ssh-agent -s`
# Checa as chaves adicionadas
ssh-add -l
# Se não há chaves adicionadas
ssh-add ~/.ssh/id_rsa_personal
ssh-add ~/.ssh/id_rsa_company

# Checa a conexão
ssh -T git@personal.github.com
ssh -T git@company.github.com
```
