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
// Dados utilizados nos exemplos
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
// Exemplo: Listar elementos de um vetor

for (var i = 0, length = names.length; i < length; i++) {
  console.log(names[i]); // Exibe os 5 elementos do vetor.
}

names.forEach(function(name) {
  console.log(name); // Exibe os 5 elementos do vetor.
});

names.forEach(function(name) {
  names.push('Name6');
  console.log(name);
  // Exibe os 5 elementos do vetor e Name6 não será incluído.
});
// Motivo:
// os elementos que serão processados são invocados antes da chamada do callback.

people.forEach(function(person) {
  console.log(`Nome: ${person.name} e idade: ${person.age}.`);
  // Exibe as propriedades name e age de cada objeto do vetor.
});
```

#### `map`

O método `map()` invoca a função _callback_ passada por argumento para cada elemento do array e devolve um novo array como resultado.

```javascript
// Exemplo: Multiplicar dados de um vetor

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
// Exemplo: Encontrar pessoas com 16 anos ou mais

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
console.log(age16b); // Retorna vetor de objetos
console.log(typeof age16b); // Retorna tipo object
console.log(`Nome: ${age16b[0].name} e idade: ${age16b[0].age}.`);
// Retorna primeira posição do vetor de objetos
```

#### `find`

O método `find()` retorna o valor do primeiro elemento do array que satisfizer a função de teste fornecida. Caso contrário, `undefined` é retornado.

```javascript
// Exemplo: Encontrar uma pessoa com 16 anos

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
// Exemplo: Verificar se todas as pessoas tem a mesma idade (16 anos)

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

O método `some()` testa se algum dos elementos no array passa no teste implementado pela função fornecida.

```javascript
// Exemplo: Verifica se alguma pessoa tem a idade procurada (16 anos)

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

O método `reduce()` utiliza uma função sobre um acumulador e cada elemento do array (da esquerda para direita), reduzindo-a a um único valor.

```javascript
// Exemplo: Somar valores de um vetor

var sum1 = 0;
for (var i = 0, length = numbers.length; i < length; i++) {
  sum1 += numbers[i];
}
console.log(sum1); // Retorna soma dos elementos do vetor
console.log(typeof sum1); // Retorna tipo number

var sum2 = numbers.reduce(function(sum, number) {
  return sum + number;
}, 0);
console.log(sum2); // Retorna soma dos elementos do vetor
console.log(typeof sum2); // Retorna tipo number

// sum é um acumulador para a operação aritmética
// number é o valor a ser adicionado ao acumulador
// 0 (zero) é o valor inicial do acumulador
```

```javascript
// Exemplo: Somar valores em um vetor de objetos

var total = fruits.reduce(function(sum, fruit) {
  return sum + fruit.price
}, 0);
console.log(total);
// Retorna soma das propriedades price de cada objeto do vetor
console.log(typeof total); // Retorna tipo number
```

```javascript
// Exemplo: Retornar vetor com valor de cada fruta

var prices = fruits.reduce(function(list, fruit) {
  list.push(fruit.price);
  return list;
}, []);
console.log(prices);
// Retorna vetor com os atributos price de cada objeto do vetor original
console.log(typeof prices); // Retorna tipo object
```

```javascript
// Exemplo: Reduzir um vetor de vetores

var list1 = matrix.reduce(function(a, b) {
  return a.concat(b);
});
console.log(list1);
// Retorna [10, 20, 30, 40, 50, 30, 40, 50, 60, 70, 50, 60, 70, 80, 90]

// Exemplo: Remover itens duplicados em um vetor

var list2 = list1.sort().reduce(function(init, current) {
  if (init.length === 0 || init[init.length - 1] !== current) {
    init.push(current);
  }
  return init;
}, []);
console.log(list2);
// Retorna [10, 20, 30, 40, 50, 60, 70, 80, 90]
```
