# JavaScript | Referência Rápida

## Declaração de variáveis

``` javascript
var var1;
let var2;
const VAR3;
```

## Verificando um tipo

``` javascript
var somevar = <SOMEVALUE>;
console.log(typeof somevar);
```

## Métodos auxiliares

### `forEach()`

O método `forEach()` executa uma dada função em cada elemento de um array.

``` javascript
var chars = ['A','B','C','D','E'];
for(var i = 0; i < chars.length; i++) {
    console.log(chars[i]);
}
chars.push('F');
chars.forEach(function(char) {
    console.log(char);
});
```

### `map()`

O método `map()` invoca a função callback passada por argumento para cada elemento do array e devolve um novo array como resultado.

``` javascript
var nums = [1, 2, 3, 4, 5];
var twoTimes = [];
nums.forEach(function(num) {
    twoTimes.push(num * 2);
});
console.log(twoTimes);
var threeTimes = nums.map(function(num) {
    return num * 3;
});
console.log(threeTimes);
```

### `filter()`

O método `filter()` cria um novo array com todos os elementos que passaram no teste implementado pela função fornecida.

``` javascript
var matrix = [
    {char:'A', position:1},
    {char:'B', position:2},
    {char:'C', position:3},
    {char:'D', position:4},
    {char:'E', position:5}
];
var positions1 = [];
for(var i = 0; i < matrix.length; i++) {
    var mat = matrix[i];
    if(mat.position >= 3) positions1.push(mat);
}
console.log(positions1);
var positions2 = matrix.filter(function(mat) {
    return mat.position > 3;
});
console.log(positions2);
```

### `find()`

O método `find()` retorna o valor do primeiro elemento do array que satisfizer a função de teste provida. Caso contrario, `undefined` é retornado.

``` javascript
var findPosition1;
for(var i = 0; i < matrix.length; i++) {
    var mat = matrix[i];
    if(mat.char === 'C') {
        findPosition1 = mat;
        break;
    }
}
console.log(findPosition1);
var findPosition2 = matrix.find(function(mat) {
    return mat.char === 'C';
});
console.log(findPosition2);
```

### `every()`

O método `every()` testa se todos os elementos do array passam pelo teste implementado pela função fornecida.

``` javascript
var all5 = matrix.every(function(mat) {
    return mat.position === 5;
});
console.log(all5);
```

### `some()`

O método `some()` testa se alguns dos elementos no array passam no teste implementado pela função atribuída.

``` javascript
var any5 = matrix.some(function(mat) {
    return mat.position === 5;
});
console.log(any5);
```

### `reduce()`

O método `reduce()` utiliza uma função sobre um acumulador (seria quase um sinônimo para array com elementos numéricos) e cada elemento do array (da esquerda para direita), reduzindo-a a um único valor.

``` javascript
var nums = [1, 2, 3, 4, 5];
var sum1 = 0;
for(var i = 0; i < nums.length; i++) {
    sum1 += nums[i];
}
console.log(sum1);
var sum2 = nums.reduce(function(sum, num) {
    return sum + num;
}, 0);
console.log(sum2);
```
