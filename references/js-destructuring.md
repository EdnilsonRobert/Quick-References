# JavaScript | Referência Rápida

## Desestruturamento

Desestruturamento e uma maneira de extrair vários valores armazenados em objetos e arrays.

```javascript
const User = {
  name: 'CSS',
  surname: 'Cafe',
  email: 'have.fun@css.cafe',
  website: 'https://css.cafe/'
}

// Modo sem desestruturamento
const email = User['email'];
console.log(email); // Retorna have.fun@css.cafe

// Modos com desestruturamento
const {email} = User;
console.log(email); // Retorna have.fun@css.cafe

const {name, surname} = User;
console.log(`${name} ${surname}`); // Retorna CSS Cafe

const {...props} = User;
console.log(props); // Retorna um objeto com todas as propriedades
```

### Rótulos (_label_)

Se o nome de uma variável não for suficientemente claro para utilizá-lo no código é possível atribuir um apelido para essa variável. Esse apelido é chamado de _label_ (rótulo). **Importante**: ao receber um rótulo a variável original se torna inacessível.

```javascript
const User = {
  name: 'CSS Cafe',
  page: 'https://css.cafe/'
}
const {page:website} = User;

console.log(page); // Retorna ReferenceError: page is not defined
console.log(website); // Retorna https://css.cafe/
```

### Desestruturamento dentro de funções

```javascript
const beverage = {
  name: 'cerveja',
  style: 'premium lager',
  brand: 'Heineken'
}
const dish = {
  name: 'queijo',
  type: 'emmental'
}

function harmonization({name:beverage, style, brand}, {name:dish, type}) {
  return `A ${beverage} ${style} ${brand} harmoniza com ${dish} ${type}.`;
}
harmonization(beverage, dish);
// Retorna A cerveja premium lager Heineken harmoniza com queijo emmental.
```

### Desestruturamento em arrays

```javascript
const Ramones = ['Dee Dee', 'Joey', 'Johnny', 'Tommy'];
const [member1, , member3, ] = Ramones;
console.log(`${member1} e ${member3}`); // Retorna Dee Dee e Johnny
```

```javascript
const Ramones = [
  {
    name: 'Dee Dee',
    job: 'baixista'
  },
  {
    name: 'Joey',
    job: 'vocalista'
  },
  {
    name: 'Johnny',
    job: 'guitarrista'
  },
  {
    name: 'Tommy',
    job: 'baterista'
  }
];

function showMember([,{name, job}]) {
  console.log(`${name} é ${job} na banda Ramones.`);
}
showMember(Ramones); // Retorna Joey é vocalista na banda Ramones.
```
