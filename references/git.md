# Git | Referência Rápida

- Referência: [http://git-scm.com/docs/](http://git-scm.com/docs/)

## Git workflow

```
|-------------------|           |--------------|              |---------------|
| WORKING DIRECTORY | --------> | STAGING AREA | -----------> | GIT DIRECTORY |
|-------------------|  git add  |--------------|  git commit  |---------------|


|---------------|  git pull  |------------|
|               | <--------- |            |
| GIT DIRECTORY |            | REPOSITORY |
|               | ---------> |            |
|---------------|  git push  |------------|
```

## Configuração

``` bash
# Checa onde foi instalada a versão do Git
whereis git    # Linux
where git      # Windows

# Verifica versão do Git
git --version

# Define configurações de usuário
git config --global user.name "UserName"
git config --global user.email "username@email.com"
# Se a configuração for apenas local o atributo --global pode ser omitido

# Define configuração de exibição de cores em linha de comando
git config --global color.ui true

# Define preferência de finalização de linha (line ending)
# -- Unix/Mac
git config --global core.autocrlf input
git config --global core.safecrlf true
# -- Windows
git config --global core.autocrlf true
git config --global core.safecrlf true

# Mostra as configurações do Git
git config --list
```

## Ajuda

``` bash
git help [comando]
```

## Clonando um projeto

``` bash
# Clona um projeto dentro de um diretório com o mesmo nome do projeto remoto
git clone http://path/to/project.git

# Clona um projeto dentro de um diretório chamado my-project
git clone http://path/to/project.git my-project
```

## Iniciando um acompanhamento de versão

``` bash
# Inicia o versionamento no diretório atual como branch master
git init

# Cria um arquivo de definição para arquivos que não devem ser versionados
touch .gitignore
```

O arquivo .gitignore:
```
dump.txt
tmp/*
*.log
```

- Linha 1: ignorar um arquivo com nome e extensão de arquivo definidos.
- Linha 2: ignorar todos os elementos dentro de um diretório.
- Linha 3: ignorar todos os elementos com a extensão `.log`.

## Branches

``` bash
# Exibe as branches existentes no projeto
git branch

# Cria uma nova branch chamada develop
git checkout -b develop

# Muda o controle do versionamento para a branch develop
git checkout develop

# Elimina a branch develop
git branch -d develop

# Muda a branch master e recebe as alterações de develop
git checkout master
git merge develop
```

## Lidando com arquivos

``` bash
# Verifica o estado atual do controle de versão
git status

# Lista todos os arquivos 'untracked' no controle de versão
git status -u

# Descarta uma alteração feita desde o último commit
git checkout -- file.txt

# Elimina todos os arquivos que estão fora do acompanhamento (untracked)
git clean -df

# Verifica alterações antes de enviar para staging area
git diff

# Verifica alterações depois de enviar para staging area
git diff --staging

# Envia para a staging area uma seleção de arquivos de acordo com um pattern
git add *.md file.html css/*

# Envia para a staging area todos os arquivos (new, modified, deleted)
git add .
git add -A
# -A == --all

# Envia para a staging area arquivos modificados e deletados (ignora novos)
git add -u
# -u == --update

# Envia para a staging area arquivos novos e modificados (ignora removidos)
git add --ignore-removal

# Remove um arquivo da staging area
git reset HEAD tmp/file.txt

# Efetua commit de todos os arquivos da staging area
git commit -m "Mensagem descritiva do commit"

# Altera a mensagem do último commit
git commit -m "Mensagem que irá substituir a anterior" --amend

# Realiza add e commit em apenas um comando
git commit -a -m "Mensagem descritiva do commit"
# Serve apenas para arquivos que já estejam em acompanhamento
# Arquivos 'untracked' deve ser adicionados com git add

# Desfaz último commit
git revert HEAD

# Remove arquivo do acompanhamento (deleta o arquivo do projeto)
git rm file.txt

# Remove arquivo do acompanhamento (mantém o arquivo no projeto)
git rm --cached file.txt

# Remove arquivos do acompanhamento (mantém os arquivos no projeto)
git rm -r --cached folder/
```
<!--
Untracking
git update-index --assume-unchanged [path]
git update-index --no-assume-unchanged [path]
-->

## Tags

``` bash
# Exibe as tags de versões do projeto
git tag

# Cria uma tag para o status atual do projeto
git tag -a v1.0 -m "Versão 1 do projeto"

# Cria uma tag para um estado anterior do projeto
git tag -a v0.0 [hash] -m "Versão 0 do projeto"
# onde [hash] == hash do status a ser etiquetado

# Exibe detalhes de uma tag
git show v1.0

# Altera o ponteiro do controlador para a versão de uma tag específica
git checkout v1.0

# Elimina uma tag da lista
git tag -d v1.0
```

## Histórico

``` bash
# Exibe o histórico do acompanhamento
git log

# Exibe apenas os três últimos itens do histórico
git log -p -3

# Outras formatações
git log --graph
git log --oneline
git log --graph --oneline --decorate
git log --graph --oneline --all
git log --pretty=format:"%h%x09%an%x09%s"

# Pode ser necessário 'sair' do relatório por ser muito extenso
q
```

## Trabalhando remotamente

``` bash
# Mostra o local de trabalho no servidor
git remote
git remote -v

# Define um repositório remoto para o repositório local de trabalho
git remote add origin http://path/to/project.git

# Envia os arquivos para o servidor
git push origin master
git push -u origin master
git -c http.sslVerify=false push -u origin master

# Cria um repositório remoto em servidor próprio
git init --bare
```
