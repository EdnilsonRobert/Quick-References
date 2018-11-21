# JavaScript | Referência Rápida

## Estruturas de Dados

### `Map`

`Map` é uma estrutura de dados constituída por pares chave/valor. As chaves são os nomes dos atributos e podem ser funções, objetos, expressões ou tipos como strings e números.

```javascript
// Criando um Map
var map = new Map();

// Definindo elementos
function myFunction() {};
var myObject = {};

// Adicionando entradas ao Map
map.set('String', 'Primeiro atributo');
map.set(myObject, 'Segundo atributo');
map.set(myFunction, 'Terceiro atributo');

// Retornando valores de atributos
console.log(map.get('String')); // Retorna o valor do primeiro atributo

// Retornando o tipo das chaves dos atributos
console.log(typeof 'String'); // Retorna tipo string

// Retornando o tipo dos valores dos atributos
console.log(typeof map.get('String')); // Retorna tipo string

// Retornando o tamanho do Map
console.log(`Tamanho do mapa: ${map.size}`);

// Verificando a existência de um atributo
console.log(map.has(myObject)); // Retorna true
console.log(map.has('otherObject')); // Retorna false

// Removendo um atributo do Map
map.delete('String');

// Removendo todos os atributos de um Map
map.clear();

// Iterações em um Map
for (var key of map.keys()) {
  console.log(`${key} | Tipo: ${typeof key}`);
  // Retorna o nome do atributo e seu tipo
}
for (var value of map.values()) {
  console.log(`${value} | Tipo: ${typeof value}`);
  // Retorna o valor do atributo e seu tipo
}
for (var entry of map.entries()) {
  console.log(`${entry} | Tipo: ${typeof entry}`);
  // Retorna atributo (chave/valor) e o tipo object
}
```

### `WeakMap`

`WeakMap` é uma coleção de pares chave/valor como o Map, porém suas chaves só podem ser objetos e suas referências dos objetos nas chaves são fracamente mantidas. Isso significa que não há prevenção para que os objetos não sejam removidos pelo Garbage Collector caso não exista alguma referência para o objeto em memória.

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

// Retornando valores de atributos
console.log(weakMap.get(elem1)); // Retorna o valor do primeiro atributo

// Retornando o tipo das chaves dos atributos
console.log(typeof elem1); // Retorna tipo object

// Retornando o tipo dos valores dos atributos
console.log(typeof weakMap.get(elem1)); // Retorna tipo string

// Verificando a existência de um atributo
console.log(weakMap.has(elem1)); // Retorna true
console.log(weakMap.has(elem4)); // Retorna false

// Removendo um atributo do WeakMap
weakMap.delete(elem3);

// Testando perda de referência de atributo
elem2 = null;
setTimeout(function() {
  console.log(weakMap.get(elem2)); // Retorna undefined após 3s
}, 3000);
```

Vantagens:

  - mantém o programa protegido de Memory Leak;
  - mantém os dados privados dentro da aplicação.

Exemplo: Proteger dados privados

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

// Adicionando música
playlist.add(music1);
playlist.add(music2);
playlist.add(music3);

// Removendo música
playlist.delete(music3);

// Removendo todas as músicas
playlist.clear();

// Adicionando uma música que já está na playlist
playlist.add(music1);

// Retornando tamanho da playlist
console.log(playlist.size);

// É possível inicializar o Set com elementos
var playlist = new Set([music1, music2, music3, music4]);

// Checando músicas na playlist
for (var music of playlist) {
  console.log(music);
}
```

### `WeakSet`

`WeakSet` é...

```javascript
```
