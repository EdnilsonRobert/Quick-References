# JavaScript | Referência Rápida

## Arrow Functions

### Funções

Há algumas formas de se declarar funções em Javascript.

  - Declaração de função (_function declaration_);
  - expressão de função (_function expression_);
  - construtor de função.

```javascript
// Declaração de função
function doAwesomeThing() {
  // Do awesome thing
}

// Expressão de função
var doAwesomeThing = function() {
  // Do awesome thing
}

// Construtor de função
var doAwesomeThing = new Function();
```

### Arrow Functions

São menos verbosas e tratam de forma diferente o contexto de execução.

```javascript
(param1, param2, ..., paramN) => {
  // Corpo da função
}
// Onde:
// (param1, param2, ..., paramN) são os parâmetros da função;
// o símbolo => é chamado Fat Arrow;
// { } é o corpo da função.
```

#### Exemplos

```javascript
var welcome = function(name) {
  return 'Olá, ' + name + '!';
}
console.log(welcome('Mundo')); // Retorna Olá, Mundo!

// Exemplo 1
let welcome = (name) => {
  return `Olá, ${name}!`;
}
console.log(welcome('Mundo')); // Retorna Olá, Mundo!

// Exemplo 2
let welcome = name => {
  return `Olá, ${name}!`;
}
console.log(welcome('Mundo')); // Retorna Olá, Mundo!
// É possível remover os parênteses dos parâmetros pois há apenas um

// Exemplo 3
let welcome = name => `Olá, ${name}!`;
console.log(welcome('Mundo')); // Retorna Olá, Mundo!
// É possível remover as chaves e o return pois o corpo da função tem apenas uma linha
```

### Contexto de execução

O contexto de exeução possui uma propriedade chamada ThisBinding que pode ser acessada a qualquer momento através da palavra reservada `this`. O valor do `this` (contexto da função) é constante e existe somente enquanto a função existir (enquanto o contexto existir).

```javascript
// Exemplo 1
console.log(this);
// Retorna Window pois o this faz referência ao objeto global Window

// Exemplo 2
function context2() {
  console.log(this);
}
context2();
// Retorna Window pois o this faz referência ao objeto global Window

// Exemplo 3
let obj = {
  context3: function() {
    console.log(this);
  }
}
obj.context3();
// Retorna Objeto pois o this faz referência ao objeto que contém o método
```

#### Misturando contextos

```javascript
const webdev = {
  name: 'Desenvolvimento Web',
  members: ['HTML', 'CSS', 'Javascript'],
  listMembers: function() {
    this.members.forEach(function(member) {
      console.log(`${member} é parte do ${this.name}.`);
    });
  }
}
webdev.listMembers();
```

No exemplo acima `${this.name}` retorna `undefined`. O contexto de execução da função é diferente do contexto de execução do objeto ou seja, o `this` de `this.members` não é o mesmo `this` de `this.name` pois não fazem referência ao mesmo objeto.

```javascript
const webdev = {
  name: 'Desenvolvimento Web',
  members: ['HTML', 'CSS', 'Javascript'],
  listMembers: function() {
    let self = this;
    this.members.forEach(function(member) {
      console.log(`${member} é parte do ${self.name}.`);
    });
  }
}
webdev.listMembers();
```

No exemplo acima `self.name` utiliza o truque de definir o contexto do objeto dentro de uma variável que será utilizada no contexto da função. Essa abordagem não é recomendada.

A solução pode ser dada com o uso de _arrow functions_ pois as funções de seta são capazes de capturar o contexto delimitador (o contexto do objeto pai da função). As arrow functions fazem a associação automática (`bind`) entre o contexto de execução da função com o contexto delimitador.


```javascript
const webdev = {
  name: 'Desenvolvimento Web',
  members: ['HTML', 'CSS', 'Javascript'],
  listMembers: function() {
    this.members.forEach(member => {
      console.log(`${member} é parte do ${this.name}.`);
    });
  }
}
webdev.listMembers();
```

As _arrow functions_ foram projetadas para conseguir capturar o `this` (ou seja, o contexto de execução) do seu contexto delimitador (isso é chamado de escopo léxico da função). Com isso, não é necessário utilizar métodos com o `bind` ou fazer truques como armazenar o valor do contexto em uma variável.
