# JavaScript | Referência Rápida

## Estruturas de Dados

### `Map`

`Map` é uma estrutura de dados constituída por pares chave/valor. As chaves são os nomes das propriedades e podem ser funções, objetos, expressões ou tipos como strings e números.

```javascript
// Criando um Map
var map = new Map();

// Definindo elementos
function myFunction() {};
var myObject = {};

// Adicionando entradas ao Map
map.set('String', 'Primeira propriedade');
map.set(myObject, 'Segunda propriedade');
map.set(myFunction, 'Terceira propriedade');

// Retornando valores de propriedades
console.log(map.get('String')); // Retorna o valor da primeira propriedade

// Retornando o tipo das chaves das propriedades
console.log(typeof 'String'); // Retorna tipo string

// Retornando o tipo dos valores das propriedades
console.log(typeof map.get('String')); // Retorna tipo string

// Retornando o tamanho do Map
console.log(`Tamanho do mapa: ${map.size}`);

// Verificando a existência de uma propriedade
console.log(map.has(myObject)); // Retorna true
console.log(map.has('otherObject')); // Retorna false

// Removendo uma propriedade do Map
map.delete('String');

// Removendo todas as propriedades de um Map
map.clear();

// Iterações em um Map
for (var key of map.keys()) {
  console.log(`${key} | Tipo: ${typeof key}`);
  // Retorna o nome da propriedade e seu tipo
}
for (var value of map.values()) {
  console.log(`${value} | Tipo: ${typeof value}`);
  // Retorna o valor da propriedade e seu tipo
}
for (var entry of map.entries()) {
  console.log(`${entry} | Tipo: ${typeof entry}`);
  // Retorna propriedade (chave/valor) e o tipo object
}
```

### `WeakMap`

`WeakMap` é uma coleção de pares chave/valor como o Map, porém suas chaves só podem ser objetos e as referências dos objetos nas chaves são fracamente mantidas. Isso significa que não há prevenção para que os objetos não sejam removidos pelo _Garbage Collector_ caso não exista alguma referência para o objeto em memória.

```javascript
// Criando um WeakMap
var weakMap = new WeakMap();

// Definindo elementos
var elem1 = {attr: 1}
var elem2 = {attr: 2}
var elem3 = {attr: 3}
var elem4 = {attr: 4}

// Adicionando entradas ao WeakMap
weakMap.set(elem1, 'String 1');
weakMap.set(elem2, 'String 2');
weakMap.set(elem3, 'String 3');

// Retornando valores de propriedades
console.log(weakMap.get(elem1)); // Retorna o valor do primeira propriedade

// Retornando o tipo das chaves das propriedades
console.log(typeof elem1); // Retorna tipo object

// Retornando o tipo dos valores das propriedades
console.log(typeof weakMap.get(elem1)); // Retorna tipo string

// Verificando a existência de uma propriedade
console.log(weakMap.has(elem1)); // Retorna true
console.log(weakMap.has(elem4)); // Retorna false

// Removendo uma propriedade do WeakMap
weakMap.delete(elem3);

// Testando perda de referência de propriedade
elem2 = null;
setTimeout(function() {
  console.log(weakMap.get(elem2)); // Retorna undefined após 3s
}, 3000);
```

Vantagens:

  - mantém o programa protegido de _Memory Leak_;
  - mantém os dados privados dentro da aplicação.

#### Exemplo: Proteger dados privados

```javascript
// Abordagem tradicional
function Person(name) {
  this._name = name;
}
Person.prototype.getName = function() {
  return this._name;
}
var person = new Person('Joey');
console.log(person._name); // Retorna Joey
console.log(person.getName()); // Retorna Joey

// Abordagem com WeakMap
var Person = (function() {
  var dataPrivate = new WeakMap();

  function Person(name) {
    dataPrivate.set(this, { name: name });
  }
  Person.prototype.getName = function() {
    return dataPrivate.get(this).name;
  }

  return Person;
}());
var person = new Person('Dee Dee');
console.log(person._name); // Retorna undefined
console.log(person.getName()); // Retorna Dee Dee
```

### `Set`

`Set` é uma estrutura de dados que não permite duplicatas, ou seja, não é possível adicionar um mesmo elemento duas vezes em uma mesma lista. `Set` mantém a ordem de inserção dos itens.

```javascript
// Exemplo: Playlist de músicas

// Músicas disponíveis
var music1 = { title: 'Sem você meu coração é null', author: 'Oracle' };
var music2 = { title: 'meu coração é componetizado', author: 'React' };
var music3 = { title: 'Tudo isso é tão dinâmico', author: 'JavaScript' };
var music4 = { title: 'Não me chame depois...', author: 'Node' };
var music5 = { title: 'No amor não existe rollback', author: 'SQL' };

// Criando um Set
var playlist = new Set();

// Adicionando músicas
playlist.add(music1);
playlist.add(music2);
playlist.add(music3);

// Removendo elementos
playlist.delete(music3);

// Removendo todos os elementos
playlist.clear();

// Adicionando um elemento que já está no Set
playlist.add(music1); // music1 não será adicionada à playlist

// Retornando tamanho do Set
console.log(playlist.size);

// É possível inicializar o Set com elementos
var playlist = new Set([music1, music2, music3, music4]);

// Iteração em um Set
for (var music of playlist) {
  console.log(music); // Retorna um objeto contendo música e autor
}
```

### `WeakSet`

O `WeakSet` é um Set que não previne os seus elementos de serem coletados pelo _Garbage Collector_. No `WeakSet` só é possível adicionar objetos. O `WeakSet` não é iterável.
