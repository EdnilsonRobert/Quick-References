# Gulp | Referência Rápida

- Gulp: [https://gulpjs.com/](https://gulpjs.com/)

## Instalação

``` bash
# Se já existe uma versão anterior do Gulp
npm rm --global gulp

# Instala o gulp globalmente
npm install -g gulp-cli
yarn add gulp
```

## Setup inicial

``` bash
# Cria um arquivo package.json de forma interativa
npm init
yarn init

# Instala módulo localmente para desenvolvimento
# --save-dev grava a definição do módulo no package.json
npm install --save-dev gulp
yarn add gulp --dev

# Instala todas as dependências
npm install --save-dev gulp-sass gulp-autoprefixer
yarn add gulp-sass gulp-autoprefixer

# Desinstala módulos desnecessários
npm uninstall --save-dev gulp-autoprefixer
yarn remove gulp-autoprefixer

# Gera o diretório node_modules
npm install
yarn
yarn install
```

## Arquivo `gulpfile.js`

``` javascript
var gulp = require('gulp');

gulp.task('default', function() {
  // Tasks
});

// Exemplo
gulp.task('hello', function() {
  console.log('Hello, World!');
});
```

## Execução no terminal

``` bash
# Executa todo o arquivo gulpfile.js
gulp

# Executa apenas uma task específica
gulp <task_name>
```
