# JavaScript | Referência Rápida

## Objetos

Em Javascript, Objeto é uma coleção de propriedades e cada propriedade é um par chave/valor. Cada valor pode ser um tipo primitivo, outro objeto ou até mesmo uma função (que será considerada um método do objeto).

Há duas maneiras de se criar objetos:

  1. funções construtoras;
  2. objetos literais.

### Funções construtoras

Funções construtoras utilizam a palavra reservada `new` e criam uma nova instância de um objeto.

```javascript
function Band(name) {
  this.name = name;
}
var band = new Band('Ramones');
console.log(band); // Retorna o objeto Band e seu atributo name
console.log(typeof band); // Retorna object
console.log(band instanceof Band); // Retorna true
```

  1. Um novo objeto literal é criado.
  2. O construtor do objeto `livro` é definido como `Livro`, assim como seu tipo (que pode ser verificado com `instanceof`).
  3. O protótipo do objeto `livro` é definido como `Livro.prototype`.
  4. É criado um novo contexto de execução para o objeto.

### Objetos literais

```javascript
var band = {
  name: 'Ramones'
}
console.log(band.name); // Retorna Ramones

var otherBand = band;
otherBand.name = 'Sex Pistols'
console.log(band.name); // Retorna Sex Pistols
console.log(otherBand.name); // Retorna Sex Pistols

band.name = 'Dead Kennedys';
console.log(band.name); // Retorna Dead Kennedys
console.log(otherBand.name); // Retorna Dead Kennedys
```

A variável `otherBand` não é um novo objeto, mas uma referência à primeira variável, o objeto `band` e ambas apontam para o mesmo endereço de memória. Sendo assim, modificar o valor de uma variável também modifica o valor da outra.

#### Atribuindo propriedades

```javascript
var band = {
  name: 'Ramones'
}

// Adicionando propriedades ao objeto
band.origin = 'NYC, USA';
band['members'] = 4;
band['showBand'] = function() {
  console.log(this.name + ' (' + this.origin + ')');
}

// Exibindo o objeto
band.showBand(); // Retorna Ramones (NYC, USA)
console.log(band); // Retorna o objeto e suas propriedades
```

### Melhorias em objetos literais

#### Exemplo 1: Propriedades com chave e valor

O exemplo abaixo demonstra um objeto recebe uma variável como valor de cada propriedade.
```javascript
var name = 'Ramones';
var origin = 'NYC, USA';

var band = {
  name: name,
  origin: origin
}
console.log(band.name + ' (' + band.origin + ')');
// Retorna Ramones (NYC, USA)
```

#### Exemplo 2: Propriedades sem chave, apenas valor

O exemplo abaixo demonstra que se o nome da propriedade coincide com o nome da variável não é necessário definir o par chave/valor, basta definir apenas o valor. O interpretador associa o nome da propriedade com o nome da variável e faz o `bind` automático.

```javascript
let name = 'Ramones';
let origin = 'NYC, USA';
let sloogan = function() {
  console.log(`${this.name} diz: Gabba Gabba Hey!`);
}

let band = {
  name, origin, sloogan
}
console.log(`${band.name} (${band.origin})`);
// Retorna Ramones (NYC, USA)
band.sloogan();
// Retorna Ramones diz: Gabba Gabba Hey!
```

#### Exemplo 3: Definindo a função diretamente no objeto literal

O exemplo abaixo demonstra que é possível atribuir uma função diretamente no objeto literal. Essa função será tratada como um método do objeto.

```javascript
let name = 'Ramones';
let origin = 'NYC, USA';

let band = {
  name,
  origin,
  sloogan() {
    console.log(`${this.name} diz: Gabba Gabba Hey!`);
  }
}
console.log(`${band.name} (${band.origin})`);
// Retorna Ramones (NYC, USA)
band.sloogan();
// Retorna Ramones diz: Gabba Gabba Hey!
```

### Propriedades computadas

```javascript
const methodName = 'doSomething';
const obj = {
  [methodName]() {
    console.log('Sucesso!');
  }
}
obj.doSomething(); // Retorna Sucesso!
```

```javascript
const prop = 'Name';
const nameFunction = 'show';

const obj = {
  [prop]: 'Objeto',
  [`${nameFunction}${prop}`]() {
    console.log(this[prop]);
  }
}
obj.showName(); // Retorna Objeto
```
