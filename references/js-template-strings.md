# JavaScript | Referência Rápida

## Template Strings

Estruturas de strings são abstrações de alto nível para uma cadeia de caracteres. Há alguns benefícios ao utilizar estruturas de strings.

  - Ler e escrever palavras, frases e textos.
  - Descobrir o tamanho de uma string.
  - Criar substrings.
  - Fazer diferenciação e ordenação.
  - Buscar elementos específicos.
  - Eliminar e transformar caracteres ou palavras.

Considerando o snippet abaixo.

```javascript
const band = {
  name: 'Ramones',
  members: {
    name: 'Dee Dee',
    job: 'baixista'
  }
}

// Exemplo 1
let message = band.members.name + ' é o ' + band.members.job + ' da banda ' +
  band.name + '.';
console.log(message);

// Exemplo 2
console.log(`${band.members.name} é o ${band.members.job} da banda ${band.name}.`);
```

No Exemplo 1 acima há alguns contratempos.

  - Concatenação de várias strings para formar uma frase inserindo diversas variáveis em `message`.
  - A variável `message` além de longa é pouco legível.
  - Há quebras de linha para manter a formatação.

O Exemplo 2 mostra uma forma mais limpa de escrever a string: a interpolação de strings. É importante notar que o segundo exemplo não utiliza um par de apóstrofos ou aspas para envolver a string, mas sim um par de crases. Esse modelo dispensa a concatenação de strings e variáveis.

A interpolação de strings permite, além de variáveis, a utilização de expressões.

```javascript
let n1 = 1;
let n2 = 2;
console.log(`A soma de ${n1} e ${n2} resulta em ${n1 + n2}.`);
```

Template strings mantém a formatação.

```javascript
// Sem template strings
console.log('function log(any) {\n  console.log(any);\n}');

// Com template strings
console.log(`
function log(any) {
  console.log(any);
}
`);
```

## Tagged template strings

Uma forma mais avançada dos template string são os template strings com marcações ou tags, ou tagged template strings. Com eles, você tem a possibilidade de modificar a saída dos template strings usando uma função.

```javascript
const band = {
  name: 'Ramones',
  members: {
    name: 'Dee Dee',
    job: 'baixista'
  },
  sloogan: 'Gabba Gabba Hey!'
}

function tag(strings, ...values) {
  console.log(values[0]);
  console.log(strings[1]);
  console.log(values[1]);
  console.log(strings[2]);
  console.log(values[2]);
  console.log(strings[3]);

  return band.sloogan;
}
let message = tag `${band.members.name} é o ${band.members.job} da banda ${band.name}.`;

console.log(message);
```
