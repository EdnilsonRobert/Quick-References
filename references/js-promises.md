# JavaScript | Referência Rápida

## Promises

_Promises_ são objetos que auxiliam o trabalho com operações assíncronas. Esse tipo de objeto aguarda a operação ser concluída e oferece uma resposta positiva (resolvida) em caso de sucesso, ou negativa em caso de erro no processo (rejeitada).

### Callback Hell

```javascript
function assincFunction(args, callback) {
  // Código que faz algo incrível

  callback();
}
assincFunction('Argumento', () => {
  console.log('Fim da execução.');
})

// Efeito cascata
obj.assincFunction(function(response) {
  response.assincFunction(function(response2) {
    response2.assincFunction(function(response3) {
      response3.assincFunction(function(response4) {
        return response4;
      });
    });
  });
});
```

### Promise

Uma _promise_, em essência, possui três estados:

  1. **Não resolvido**: estado inicial, quando está esperando algo ser finalizado.
  2. **Resolvido**: estado no qual a operação foi concluída, sem erros.
  3. **Rejeitado**: estado no qual a operação foi concluída, porém, com erros.

Por padrão, o construtor da _promise_ recebe uma função com dois argumentos: `resolve` e `reject`. Esses parâmetros são utilizados dentro da lógica da _promise_ para indicar quando ela foi resolvida ou rejeitada. Quando um _promise_ é resolvida sem problemas, o `then` é automaticamente ativado, assim como acontece com o `catch` quando a _promise_ é rejeitada.

```javascript
let promise = new Promise((resolve, reject) => {
  let result = true;
  (result) ? resolve('Sucesso!') : reject('Falha.');
});
promise
  .then((data) => console.log(`${data}`))
  .catch((data) => console.log(`${data}`));
```

#### Simulando operações assíncronas

```javascript
let promise = new Promise((resolve, reject) => {
  let result = true;
  let tempo = 3000;

  setTimeout(() => {
    (result) ? resolve('Sucesso!') : reject('Falha.');
  }, tempo);
});

promise
  .then((data) => console.log(`${data}`))
  .catch((data) => console.log(`${data}`));

console.log('Essa linha é executada antes do final da Promise.');
```
