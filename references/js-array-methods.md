# JavaScript | Referência Rápida

## Métodos para array

### Conteúdo

 - [`forEach`](#foreach)
 - [`map`](#map)
 - [`filter`](#filter)
 - [`find`](#find)
 - [`every`](#every)
 - [`some`](#some)
 - [`reduce`](#reduce)

### Data

```javascript
var names = ['Name1', 'Name2', 'Name3', 'Name4', 'Name5'];
var numbers = [1, 2, 3, 4, 5];
var matrix = [
  [10, 20, 30, 40, 50],
  [30, 40, 50, 60, 70],
  [50, 60, 70, 80, 90]
];
var people = [
  {name: 'Name1', age: 12},
  {name: 'Name2', age: 14},
  {name: 'Name3', age: 16},
  {name: 'Name4', age: 16},
  {name: 'Name5', age: 18}
];
var fruits = [
  {name: 'Apple', price: 4},
  {name: 'Grape', price: 9},
  {name: 'Guava', price: 5},
  {name: 'Lemon', price: 3},
  {name: 'Melon', price: 9}
];
```

### Métodos para array

#### `forEach`

O método `forEach()` executa uma dada função em cada elemento de um array.

```javascript
// EXEMPLO: LISTAR ELEMENTOS DE UM VETOR

for(var i = 0, length = names.length; i < length; i++) {
  console.log(names[i]); // Exibe os 5 elementos do vetor.
}

names.forEach(function(name) {
  console.log(name); // Exibe os 5 elementos do vetor.
});

names.forEach(function(name) {
  names.push('Name6');
  // Exibe os 5 elementos do vetor e Name6 não será incluído.
  // Motivo: o range de elementos processados é invocado antes da chamada do callback.
  console.log(name);
});

people.forEach(function(person) {
  // Exibe as propriedades name e age de cada objeto do vetor.
  console.log(`Nome: ${person.name} e idade: ${person.age}.`);
});
```

#### `map`

O método `map()` invoca a função callback passada por argumento para cada elemento do array e devolve um novo array como resultado.

```javascript
// EXEMPLO: MULTIPLICAR DADOS DE UM VETOR

var double1 = [];
numbers.forEach(function(number) {
  double1.push(number * 2);
});
console.log(numbers); // Exibe vetor original
console.log(double1); // Exibe vetor processado
console.log(typeof double1); // Retorna tipo object

var double2 = numbers.map(function(number) {
  return number * 2;
});
console.log(numbers); // Exibe vetor original
console.log(double2); // Exibe vetor processado
console.log(typeof double2); // Retorna tipo object
```

#### `filter`

O método `filter()` cria um novo array com todos os elementos que passaram no teste implementado pela função fornecida.

```javascript
// EXEMPLO: ENCONTRAR PESSOAS COM 16 ANOS OU MAIS

var age16a = [];
for (var i = 0, length = people.length; i < length; i++) {
  var person = people[i];
  if (person.age >= 16) age16a.push(person);
}
console.log(age16a); // Retorna vetor de objetos
console.log(typeof age16a); // Retorna tipo object

var age16b = people.filter(function(person) {
  return person.age >= 16;
});
// Retorna vetor de objetos
console.log(age16b);
// Retorna tipo object
console.log(typeof age16b);
// Retorna primeira posição do vetor de objetos
console.log(`Nome: ${age16b[0].name} e idade: ${age16b[0].age}.`);
```

#### `find`

O método `find()` retorna o valor do primeiro elemento do array que satisfizer a função de teste provida. Caso contrário, `undefined` é retornado.

```javascript
// EXEMPLO: ENCONTRAR UMA PESSOA COM 16 ANOS

var age16a;
for (var i = 0, length = people.length; i < length; i++) {
  var person = people[i];
  if (person.age === 16) {
    age16a = person;
    break;
  }
}
console.log(age16a); // Retorna a primeira ocorrência encontrada
console.log(typeof age16a); // Retorna tipo object

var age16b = people.find(function(person) {
  return person.age === 16;
});
console.log(age16b); // Retorna a primeira ocorrência encontrada
console.log(typeof age16b); // Retorna tipo object
```

#### `every`

O método `every()` testa se todos os elementos do array passam pelo teste implementado pela função fornecida.

```javascript
// EXEMPLO: VERIFICAR SE TODAS AS PESSOAS TEM A MESMA IDADE: 16 ANOS

var age16a = true;
for (var i = 0, length = people.length; i < length; i++) {
  var person = people[i];
  if (person.age === 16) {
    age16a = false;
    break;
  }
}
console.log(age16a); // Retorna false
console.log(typeof age16a); // Retorna tipo boolean

var age16b = people.every(function(person) {
  return person.age === 16;
});
console.log(age16b); // Retorna false
console.log(typeof age16b); // Retorna tipo boolean
```

#### `some`

O método `some()` testa se alguns dos elementos no array passam no teste implementado pela função atribuída.

```javascript
// EXEMPLO: VERIFICA SE ALGUMA PESSOA TEM 16 ANOS DE IDADE

var age16a = false;
for (var i = 0, length = people.length; i < length; i++) {
  var person = people[i];
  if (person.age === 16) {
    age16a = true;
    break;
  }
}
console.log(age16a); // Retorna true
console.log(typeof age16a); // Retorna tipo boolean

var age16b = people.some(function(person) {
  return person.age === 16;
});
console.log(age16b); // Retorna true
console.log(typeof age16b); // Retorna tipo boolean
```

#### `reduce`

O método `reduce()` utiliza uma função sobre um acumulador (seria quase um sinônimo para array com elementos numéricos) e cada elemento do array (da esquerda para direita), reduzindo-a a um único valor.

```javascript
// EXEMPLO: SOMAR VALORES DE UM VETOR

var sum1 = 0;
for (var i = 0, length = numbers.length; i < length; i++) {
  sum1 += numbers[i];
}
console.log(sum1); // Retorna soma dos elementos do vetor
console.log(typeof sum1); // Retorna tipo number

var sum2 = numbers.reduce(function(sum, number) {
  return sum + number;
  // sum é um acumulador para a operação aritmética
  // number é o valor a ser adicionado ao acumulador
  // 0 (zero) é o valor inicial do acumulador
}, 0);
console.log(sum2); // Retorna soma dos elementos do vetor
console.log(typeof sum2); // Retorna tipo number
```

```javascript
// EXEMPLO: SOMAR VALORES EM UM VETOR DE OBJETOS

var total = fruits.reduce(function(sum, fruit) {
  return sum + fruit.price
  // sum é um acumulador para a operação aritmética
  // fruit é o objeto com um atributo numérico a ser adicionado ao acumulador
  // 0 (zero) é o valor inicial do acumulador
}, 0);
console.log(total); // Retorna soma dos atributos price de cada objeto do vetor
console.log(typeof total); // Retorna tipo number
```

```javascript
// EXEMPLO: RETORNAR VETOR COM VALOR DE CADA FRUTA

var prices = fruits.reduce(function(list, fruit) {
  list.push(fruit.price);
  return list;
  // list é um acumulador para a receber os preços de cada fruta
  // fruit é o objeto com um valor numérico a ser adicionado ao acumulador
  // [] (vetor vazio) é o valor inicial do acumulador
}, []);
// Retorna vetor com os atributos price de cada objeto do vetor original
console.log(prices);
// Retorna tipo object
console.log(typeof prices);
```

```javascript
// EXEMPLO: REDUZIR UM VETOR DE VETORES

var list1 = matrix.reduce(function(a, b) {
  return a.concat(b);
});
console.log(list1);
// Retorna [10, 20, 30, 40, 50, 30, 40, 50, 60, 70, 50, 60, 70, 80, 90]

// EXEMPLO: REMOVER ITENS DUPLICADOS

var list2 = list1.sort().reduce(function(init, current) {
  if (init.length === 0 || init[init.length - 1] !== current) {
    init.push(current);
  }
  return init;
}, []);
console.log(list2);
// Retorna [10, 20, 30, 40, 50, 60, 70, 80, 90]
```
