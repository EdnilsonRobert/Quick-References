# JavaScript | Referência Rápida

## Estruturas de Dados

### `Map`

`Map` é uma estrutura de dados constituída por pares chave/valor. As chaves são os nomes dos atributos e os valores podem ser funções, objetos, expressões ou tipos como strings e números.

```javascript
var map = new Map();
function myFunction() {};
var myObject = {};

map.set('String', 'Primeiro atributo');
map.set(myObject, 'Segundo atributo');
map.set(myFunction, 'Terceiro atributo');

console.log(map.get('String')); // Retorna o valor do primeiro atributo
console.log(map.get(myObject)); // Retorna o valor do segundo atributo
console.log(map.get(myFunction)); // Retorna o valor do terceiro atributo

console.log(typeof 'String'); // Retorna tipo string
console.log(typeof myObject); // Retorna tipo object
console.log(typeof myFunction); // Retorna tipo function

console.log(typeof map.get('String')); // Retorna tipo string
console.log(typeof map.get(myObject)); // Retorna tipo string
console.log(typeof map.get(myFunction)); // Retorna tipo string

console.log(`Tamanho do mapa: ${map.size}`);

console.log(map.has(myObject)); // Retorna true
console.log(map.has('otherObject')); // Retorna false

console.log(`Tamanho do mapa: ${map.size}`); // Retorna 3
map.set('String2', 'Quarto atributo'); // Adiciona item ao mapa
console.log(`Novo item adicionado. Tamanho do mapa: ${map.size}`); // Retorna 4
map.delete('String2'); // Remove item do mapa
console.log(`Item removido. Tamanho do mapa: ${map.size}`); // Retorna 3

map.clear(); // Remove todos os itens do mapa

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
