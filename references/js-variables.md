# JavaScript | Referência Rápida

## Variáveis

### Exemplo de escopo de variáveis

No Exemplo 1 há uma variável definida dentro do mesmo contexto e mesmo escopo. Desta forma a segunda declaração sobrescreve a primeira.

No Exemplo 2 há duas variáveis de mesmo nome definidas dentro do mesmo contexto, todavia em escopos diferentes. Desta forma a segunda declaração não sobrescreve a primeira.

```javascript
// Exemplo 1
var message = 'String 1';
{
  var message = 'String 2';
}
console.log(message); // Retorna String 2

// Exemplo 2
var message = 'String 1';
function message() {
  var message = 'String 2';
}
console.log(message); // Retorna String 1
```

### Exemplo de escopo de função e escopo de bloco

```javascript
// Exemplo 1
var varArr = [];
for (var i = 1, length = 5; i < length; i++) {
  varArr.push(function() {
    console.log(i);
  });
}
varArr.forEach(function(func) {
  func();
});
// Retorna 5 5 5 5
// Variáveis declaradas com var tem escopo de função.
// Cada nova atribuição de valor dentro do loop é apenas uma nova atribuição a uma mesma referência.
```

```javascript
// Exemplo 2
var letArr = [];
for (let i = 1, length = 5; i < length; i++) {
  letArr.push(function() {
    console.log(i);
  });
}
letArr.forEach(function(func) {
  func();
});
// Retorna 1 2 3 4
// Variáveis declaradas com let tem escopo de bloco.
// A cada iteração uma nova variável é criada.
```

### `const`

Deve ser utilizado para variáveis que não devem mudar seu valor dentro de um escopo com o decorrer do tempo durante a execução de um programa.

```javascript
const birthDate = '01-01-2000';
birthDate = '31-12-1999'; // Retorna SyntaxError: Assignment to constant variable
```

### `let`

O `let` é o substituto do `var` e deve ser utilizado para a declaração de variáveis.

```javascript
var varNumber = 0;
var varNumber = 1;
console.log(varNumber);
// Retorna 1

let letNumber = 0;
let letNumber = 1;
console.log(letNumber);
// Retorna SyntaxError: Identifier 'letNumber' has already been declared
// Não é possível declarar duas variáveis com o mesmo nome dentro do mesmo escopo.
```

### Hoisting e TDZ (Temporal Dead Zone)

#### Hoisting e variáveis

Em Javascript, variáveis e funções tem comportamento de _hoisting_. Hoisting é o içamento das variáveis para o topo do bloco de código.

```javascript
// Considerando o snippet abaixo...
name = 'Johnny';
printName(name);

function printName(name) {
  console.log('Name:', name);
}
var nome;

// Durante a execução, as declarações de variável e função são movidas para o topo.
```

#### TDZ e `let`

O _hoisting_ do `let` e `const` são diferentes daquele encontrado com a utilização de `var` e funções. Uma variável que utiliza `let` ou `const` possui um comportamento chamado TDZ (Temporal Dead Zone). Isso significa que dentro do seu escopo, a variável só estará acessível quando a execução do programa chegar até ela.

```javascript
// Exemplo 1
let value = 0;
if (true) {
  console.log(value); // Retorna 0
}
console.log(value); // Retorna 0

// Ambas funções de console utilizam a mesma variável global.
// Não há conflito de variáveis.
```

```javascript
// Exemplo 2
let value = 0;
if (true) {
  console.log(value); // Retorna ReferenceError: value is not defined
  let value;
}
console.log(value); // Retorna 0

// Não há hoisting. Esse é o comportamento do TDZ.
// No escopo de bloco (dentro da função) a variável foi chamada antes de sua declaração.
```

```javascript
// Exemplo 3
let value = 0;
if (true) {
  let value;
  console.log(value); // Retorna undefined
}
console.log(value); // Retorna 0

// A variável é indefinida pois foi declarada, porém sem atribuição de valor.
```

```javascript
// Exemplo 4
let value = 0;
if (true) {
  let value;
  console.log(value); // Retorna undefined
  value = 1;
  console.log(value); // Retorna 1
}
console.log(value); // Retorna 0
```
