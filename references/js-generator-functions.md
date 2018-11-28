# JavaScript | Referência Rápida

## Funções geradoras

```javascript
function* webdevPath() {
  console.log('Aprender HTML.');
  yield 'Passo 1.';
  console.log('Aprender CSS.');
  yield 'Passo 2.';
  console.log('Aprender Javascript.');
  yield 'Passo 3.';
  console.log('Aprender boas práticas.');
  yield 'Avançar ao próximo nível.';
}

const path = webdevPath();

for (let step of path) {
  console.log(step);
}
```
