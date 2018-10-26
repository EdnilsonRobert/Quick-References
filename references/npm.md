# NPM | Referência Rápida

``` bash
# Verifica a versão instalada no NodeJS
node -v
# Verifica a versão instalada no npm
npm -v
# Atualiza a versão do npm
sudo npm i -g npm
```

``` bash
# Cria um arquivo package.json para iniciar um projeto
npm init
npm init -y
npm init --yes
```

``` bash
# Instala um novo pacote
npm i <pacote>

# Remove um pacote
npm uninstall <pacote>

# Atualiza um pacote
npm update -g <pacote>

# Verifica pacotes desatualizados
npm outdated -g --depth=0
```

``` bash
# Consulta a ajuda sobre um pacote
npm help view

# Mostra as informações de um pacote
npm view <pacote>
# Aliases para o comando view
npm info <pacote>
npm show <pacote>

# Mostra a versão atual de um pacote
npm view <pacote> version
```
