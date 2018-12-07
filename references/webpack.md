# Webpack | Referência Rápida

## Instalação

```bash
npm i --save-dev webpack webpack-cli
```

## Arquivos de exemplo

**Estrutura de exemplo**

    |
    |_ build/
    |  |_ bundle.js
    |
    |_ src/
    |  |_ js/
    |     |_ components/
    |     |  |_ hello.js
    |     |
    |     |_ index.js
    |
    |_ index.html
    |_ package.json
    |_ webpack.config.js

`./src/js/components/hello.js`

```javascript
const sayHelloTo = name => `Hello, ${name}`;
module.exports = {
  sayHelloTo
}
```

`./src/js/index.js`

```javascript
const { sayHelloTo } = require('./components/hello.js');
const greeting = document.createElement('h1');
greeting.innerText = sayHelloTo('JS Dev');
document.body.appendChild(greeting);
```

`./package.json`

```json
{
  "name": "webpack-example",
  "version": "0.0.1",
  "description": "Webpack: module bundler",
  "main": "webpack.config.js",
  "scripts": {
    "build:dev": "NODE_ENV=development webpack",
    "build:prod": "webpack"
  },
  "devDependencies": {
    "webpack": "x.x.x",
    "webpack-cli": "x.x.x"
  }
}
```

`./webpack.config.js`

```javascript
const path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'src/js/index.js'),
  output: {
    path: path.resolve(__dirname, 'build'),
    file: 'bundle.js'
  }
}
```

`./index.html`

```html
<!DOCTYPE html>
<html lang="pt-br" dir="ltr">
  <head></head>
  <body></body>
  <script src="./build/bundle.js"></script>
</html>
```

## Empacotamento

```bash
webpack .src/js/index.js ./build/bundle.js
```
