# JavaScript | Referência Rápida

## Classes

### Herança de objetos

A herança em Javascript não acontece da forma como normalmente é aprendido em Orientação a Objetos. Herança em Javascript acontece por **prototipagem** (_Prototypal Inheritance_). Dependendo das circunstâncias o desenvolvimento pode se tornar extremamente confuso.

```javascript
// Prototipando um objeto e seus métodos
function Car(brand, style, year) {
  this.brand = brand;
  this.style = style;
  this.year = year;
}
Car.prototype.move = function() {
  console.log('O carro está se movendo.');
}

// Instanciando um objeto
var car = new Car('Volvo', 'sedan', 2018);
console.log(car.brand, car.style, car.year);
car.move();

// Estendendo um objeto
function Porsche(brand, style, year) {
  Car.call(this, brand, style, year);
}
Porsche.prototype = Object.create(Car.prototype);
Porsche.prototype.constructor = Porsche;

// Adicionando um método ao objeto estendido
Porsche.prototype.runFaster = function() {
  console.log('Porsche é mais rápido que o Papa-léguas.');
}

// Instanciando um objeto estendido
var porsche = new Porsche('Porsche', 'sport', 1974);
console.log(porsche.brand, porsche.style, porsche.year);
porsche.move();
porsche.runFaster();
```

### Classes

As classes em Javascript são como uma camada de abstração sobre a prototipagem, tornando o código mais simples (_syntax sugar_) e próximo ao paradigma de Orientação a Objetos.

```javascript
// Modelando uma classe e seus métodos
class Car {
  constructor(brand, style, year) {
    this.brand = brand;
    this.style = style;
    this.year = year;
  }

  move() {
    console.log('O carro está se movendo.');
  }
}

// Instanciando um objeto a partir de uma classe
const car = new Car('Volvo', 'sedan', 2018);
console.log(car.brand, car.style, car.year);
car.move();

// Estendendo uma classe
class Porsche extends Car {
  constructor(brand, style, year, color) {
    super(brand, style, year);
    this.color = color;
  }

  runFaster() {
    console.log('Porsche é mais rápido que o Papa-léguas.');
  }
}

// Instanciando uma objeto a partir de uma classe estendida
var porsche = new Porsche('Porsche', 'sport', 'amarelo', 1974);
console.log(porsche.brand, porsche.style, porsche.color, porsche.year);
porsche.move();
porsche.runFaster();
```

#### Definindo classes com expressões

Apesar de ser incomum, também é possível declarar classes por expressões, assim como é feito com funções. Do mesmo modo, elas podem ser anônimas.

O _snippet_ abaixo...

```javascript
class Car {
  constructor(brand) {
    this.brand = brand;
  }
}
const car = new Car('Porsche');
console.log(car);
```

É equivalente a...

```javascript
const Car = class {
  constructor(brand) {
    this.brand = brand;
  }
}
const car = new Car('Porsche');
console.log(car);
```

#### Métodos estáticos

Definir métodos estáticos com a palavra reservada `static` permite que não seja necessário instanciar um objeto para utilizar um método.

```javascript
class Car {
  static runFaster() {
    console.log('Porsche é mais rápido que o Papa-léguas.');
  }
}
Car.runFaster();
```

#### Trabalhando com atributos privados

Utilizar `WeakMap` permite esconder atributos dentro de uma classe. Esses atributos só estarão acessíveis através de funções para retorná-los.


```javascript
// O snippet abaixo demonstra que não é possível acessar os atributos
const props = new WeakMap();

class Person {
  constructor(name, email) {
    props.set(this, {name, email});
  }
}

const person = new Person('CSS Cafe', 'have.fun@css.cafe');
console.log(`${person.name} | ${person.email}`);
// Retorna undefined | undefined
```

```javascript
// O método getProp torna possível o acesso ao atributo
const props = new WeakMap();

class Person {
  constructor(name, email) {
    props.set(this, {name, email});
  }

  getProp(prop) {
    return props.get(this)[prop];
  }
}

const person = new Person('CSS Cafe', 'have.fun@css.cafe');
console.log(`${person.getProp('name')} | ${person.getProp('email')}`);
// Retorna CSS Cafe | have.fun@css.cafe
```
