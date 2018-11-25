# JavaScript | Referência Rápida

## Iteradores e Iteráveis

Um objeto é um iterador quando sabe como acessar itens numa coleção, um por vez, enquanto mantém rastreada a posição atual em uma dada sequência. Iteradores fornecem uma maneira de acessar sequencialmente os elementos de uma coleção sem expor sua representação interna.

Objetos iteráveis são uma generalização dos arrays. É um conceito que permite tornar qualquer objeto utilizável em um laço `for...of`, por exemplo. Arrays são iteráveis por si só, mas não apenas arrays. Strings e alguns outros objetos _built-in_ (como Array, Map ou Set) também são iteráveis pois seus protótipos contém o método `Symbol.iterator`.

## Data

```javascript
// Dados utilizados nos exemplos
var numbers = [1, 2, 3, 4, 5];
var fruits = [
  {name: 'Apple', price: 4},
  {name: 'Grape', price: 9},
  {name: 'Guava', price: 5},
  {name: 'Lemon', price: 3},
  {name: 'Melon', price: 9}
];
var car = {
  name: 'Porsche',
  year: 1974
};
```

## Iterações

### `Symbol.iterator`

```javascript
var iterNumbers = numbers[Symbol.iterator]();
console.log(iterNumbers.next()); // Retorna { value: 1, done: false }
console.log(iterNumbers.next()); // Retorna { value: 2, done: false }
console.log(iterNumbers.next()); // Retorna { value: 3, done: false }
console.log(iterNumbers.next()); // Retorna { value: 4, done: false }
console.log(iterNumbers.next()); // Retorna { value: 5, done: false }
console.log(iterNumbers.next()); // Retorna { value: undefined, done: true }
```

### `for...of`

`for...of` percorre o laço se, e somente se, ele for iterável.

```javascript
for (var number of numbers) {
  console.log(number); // Retorna os 5 elementos do vetor
}

for (var number of numbers) {
  if(number > 3) break;
  console.log(number); // Retorna apenas os 3 primeiros elementos do vetor
}

for (var number of numbers) {
  if(number === 3) continue;
  console.log(number); // Retorna todos elementos do vetor exceto o número 3
}
```

### `for...in`

```javascript
for (var info of car) {
  console.log(info); // TypeError: car is not iterable
}

for (var info in car) {
  console.log(info);
  // Retorna as chaves das propriedades do objeto (name, year)
  console.log(typeof info);
  // Retorna os tipos (string, string)
}

for (var info in car) {
  var data = car[info];
  console.log(data);
  // Retorna os valores das propriedades do objeto (Porsche, 1974)
  console.log(typeof data);
  // Retorna os tipos (string, number)
}
```
