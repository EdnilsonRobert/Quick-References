# JavaScript | Referência Rápida

## Valores Padrão

Em Javascript, um parâmetro tem por padrão um valor `undefined`. Isso significa que se um parâmetro não tiver um valor explícito na execução de um método, seu valor sempre será `undefined`.

```javascript
// Função com um parâmetro
function parameter(param) {
  console.log(param);
}
parameter(); // Retorna undefined
parameter('Parâmetro'); // Retorna Parâmetro

// Função com múltiplos parâmetros
function parameters(param1, param2, param3) {
  console.log(`${param1}, ${param2} e ${param3}.`);
}
parameters();
// Retorna undefined, undefined e undefined.
parameters('Parâmetro 1');
// Retorna Parâmetro 1, undefined e undefined.
parameters('Parâmetro 1', 'Parâmetro 2');
// Retorna Parâmetro 1, Parâmetro 2 e undefined.
parameters('Parâmetro 1', 'Parâmetro 2', 'Parâmetro 3');
// Retorna Parâmetro 1, Parâmetro 2 e Parâmetro 3.
```

Uma estratégia é testar se há parâmetros `undefined` e definir um valor ou alterar o fluxo de execução.

```javascript
function parameters(param1, param2) {
  if (param2 === undefined) {
    console.log(`${param1}.`);
  } else {
    console.log(`${param1} e ${param2}.`);
  }
}
parameters();
// Retorna undefined.
parameters('Parâmetro 1');
// Retorna Parâmetro 1.
parameters('Parâmetro 1', 'Parâmetro 2');
// Retorna Parâmetro 1 e Parâmetro 2.
```

### Utilizando valores predefinidos

#### Valores explícitos

```javascript
function parameters(param1, param2, param3 = 'Vazio') {
  console.log(`${param1}, ${param2} e ${param3}.`);
}
parameters('Parâmetro 1', 'Parâmetro 2');
// Retorna Parâmetro 1, Parâmetro 2 e Vazio.
parameters('Parâmetro 1', 'Parâmetro 2', 'Parâmetro 3');
// Retorna Parâmetro 1, Parâmetro 2, Parâmetro 3.
```

#### Valores por referência

##### Exemplo 1

```javascript
function power(base = 2, exp = base) {
  console.log(Math.pow(base, exp));
}
power(); // [1]
power(3); // [2]
power(2,4); // [3]
```

  - [1] Se nenhum argumento é passado a variável `exp` recebe o valor padrão do parâmetro `base`. Retorna `4` (2 ^ 2).
  - [2] Se apenas um argumento é passado, `base` recebe esse valor e passa por referência ao parâmetro `exp`. Retorna `27` (3 ^ 3).
  - [3] Se dois argumentos são passados, cada parâmetro recebe seu argumento correspondente. Retorna `16` (2 ^ 4).

##### Exemplo 2

```javascript
const value = 'Valor 1';
function showValue(param = value) {
  const value = 'Valor 2';
  console.log(value); // [1]
  console.log(param); // [2]
}
showValue();
```

  - [1] Exibe Valor 2 pois `value` teve seu valor definido como `'Valor 2'` dentro da função.
  - [2] Exibe Valor 1 pois quando a função foi invocada o argumento passado foi a variável `value` com valor `'Valor 1'`.

##### Exemplo 3

```javascript
function showName(name, callback = n => {
  console.log(`N: ${n}.`);
}) {
  callback(`Callback: ${name}.`)
};
showName(); // Retorna N: Callback: undefined.
showName('Tommy'); // Retorna N: Callback: Tommy.
showName('Tommy', name => {
  console.log(`Name: ${name}.`);
}); // Retorna Name: Callback: Tommy.
```

##### Exemplo 4

```javascript
function requiredParam(param) {
  throw new Error(`O parâmetro ${param} é obrigatório.`);
}

function doSomething(obj = requiredParam('any')) {
  console.log(`Parâmetro recebido: ${obj}.`);
}

doSomething(); // Retorna Error: O parâmetro any é obrigatório.
doSomething('abc'); // Retorna Parâmetro recebido: abc.
```
