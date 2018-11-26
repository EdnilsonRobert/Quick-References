# JavaScript | Referência Rápida

## Parâmetros Rest e Operadores Spread

### Objeto `arguments`

> "O objeto arguments é uma variável local disponível dentro de todas as funções. Você pode referenciar os argumentos de uma função dentro da função usando o objeto arguments. Esse objeto contém um registro para cada argumento fornecido para a função, com o índice do primeiro registro começando em 0." - MDN Web Docs

Abaixo há um exemplo de função de soma utilizando o objeto `arguments`. O objeto `arguments` é como um objeto Array correspondendo aos argumentos passados para uma função todavia, não é um Array. É similar a um Array, mas não possui as propriedades de Array, exceto `length`.

```javascript
function sum() {
  var sum = 0;
  for (var i = 0, length = arguments.length; i < length; i++) {
    sum += arguments[i];
  }
  console.log('Soma atual: ' + sum);
}
sum(1); // Retorna 1
sum(1,2); // Retorna 3
sum(1,2,3); // Retorna 6
```

### Parâmetros Rest

> "A sintaxe de _rest parameter_ (parâmetros rest) nos permite representar um número indefinido de argumentos em um array. Se o último argumento nomeado de uma função tiver um prefixo `...`, ele irá se tornar um array em que os elementos serão são disponibilizados pelos argumentos atuais passados à função." - MDN Web Docs

O _rest parameter_ funciona apenas quando é o último argumento passado em uma função. Isso quer dizer que não é possível utilizar dois ou mais _rest parameters_.

#### Exemplo com um parâmetro

```javascript
// Ajustando o exemplo anterior utilizando parâmetros rest
function sum(...values) {
  let sum = 0;
  for (let i = 0, length = values.length; i < length; i++) {
    sum += values[i];
  }
  console.log(`Soma atual: ${sum} | ...values: [${values}]`);
}
sum(1); // Retorna Soma atual: 1 | ...values: [1]
sum(1,2); // Retorna Soma atual: 3 | ...values: [1,2]
sum(1,2,3); // Retorna Soma atual: 6 | ...values: [1,2,3]

// Ajustando o exemplo anterior utilizando parâmetros rest e reduce
function sum(...values) {
  return `Soma atual: ${values.reduce((sum, value) => {
    return sum + value;
  }, 0)}`;
}
console.log(sum(1)); // Retorna Soma atual: 1
console.log(sum(1,2)); // Retorna Soma atual: 3
console.log(sum(1,2,3)); // Retorna Soma atual: 6
```

#### Exemplo com múltiplos parâmetros

Como o _rest parameter_ interpreta unicamente os últimos argumentos passados na função, é possível definir variáveis que fiquem fora do escopo do _rest parameter_. Os parâmetros além do _rest parameter_ são chamados de **parâmetros fixos**.

```javascript
function multiplySum(multiplier, ...values) {
  return `Soma multiplicada: ${values.reduce((sum, value) => {
    return sum + (value * multiplier);
  }, 0)}`;
}
console.log(multiplySum(2,1,2)); // Retorna Soma multiplicada: 6 [1]
console.log(multiplySum(2,4,5)); // Retorna Soma multiplicada: 18 [2]
```

  - [1] 6 = (2 * 1) + (2 * 2)
  - [2] 18 = (2 * 4) + (2 * 5)

Há três diferenças principais entre _rest parameters_ e os objetos `arguments`:

  - _rest parameters_ são os únicos que não foram atribuídos a um nome separado, enquanto os objetos _arguments_ contêm todos os argumentos passados para a função;
  - o objeto `arguments` não é um array, enquanto _rest parameters_ são instâncias Array, isso significa que métodos como `sort`, `map`, `forEach` ou `pop` não podem ser aplicados diretamente;
  - o objeto `arguments` possui a funcionalidade adicional de especificar ele mesmo (como a propriedade `callee`).

### Operadores Spread


Considerando o _snippet_ abaixo...

```javascript
let args = [1, 2, 3];
console.log(args[0], args[1], args[2]); // Retorna 1 2 3
```

O _snippet_ acima pode ser modificado por...

```javascript
let args = [1, 2, 3];
console.log.apply(console, args); // Retorna 1 2 3
```

#### O operador _spread_

O `spread operator` (ou **operador de propagação**) permite uma expressão ser expandida em locais onde múltiplos argumentos (por chamadas de função) ou múltiplos elementos (por array literais) são esperados.

```javascript
let args = [1, 2, 3];
console.log(...args); // Retorna 1 2 3
```

```javascript
const listBreakfast = ['Café', 'Pão'];
const listFruits = ['Morango', 'Uva'];
const listMeal = ['Carne', 'Pimenta'];

const listMarket = listBreakfast.concat(listFruits, listMeal);
console.log(listMarket);
// Retorna ['Café','Pão','Morango','Uva','Carne','Pimenta'];
console.log(typeof listMarket); // Retorna object
```

O operador _spread_ permite propagar os itens de um array, ou seja, espalhar seus itens de forma individual. Cada item é tratado de forma isolada mas sem afetar a estrutura original.


```javascript
const listBreakfast = ['Café', 'Pão'];
const listFruits = ['Morango', 'Uva'];
const listMeal = ['Carne', 'Pimenta'];

const listMarket = [...listBreakfast, ...listFruits, ...listMeal];
console.log(listMarket);
// Retorna ['Café','Pão','Morango','Uva','Carne','Pimenta'];
console.log(typeof listMarket); // Retorna object
```
