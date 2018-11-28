# JavaScript | Referência Rápida

## Módulos

Modularizar significa dividir o código em partes que representam uma abstração funcional e reaproveitável da aplicação. Em outras palavras, um módulo deve ser auto-suficiente e sua utilização (misturar, adicionar, remover) não deve impactar um sistema como um todo.

Em Javascript cada módulo deve ser armazenado em apenas um arquivo javascript. Os benefícios obtidos com o uso dessa prática giram em torno da manutenibilidade e reusabilidade. Em resumo, a modularização permite, além de organização, o uso mais eficiente de pedaços de código.

Trabalhar com módulos exige o uso de duas palavras reservadas: `export` e `import`.

### `export`

Existem duas formas de exportar módulos: **padrão** e **nomeada**.

```javascript
// File: circle.js
export const PI = 3.14;

function circleCircunference(radius) {
  return 2 * PI * radius;
}

function circleArea(radius) {
  return PI * (radius * radius);
}

// Exportação padrão
export default circleCircunference;

// Exportação nomeada
export {circleCircunference, circleArea};
```

### `import`

```javascript
// File: main.js

// Importação de apenas um elemento
import circleCircunference from './circle';
console.log(circleCircunference(5));

// Importação de vários elementos
import {circleCircunference, circleArea, PI} from './circle';
console.log(circleCircunference(5));

// Importação de todos os elementos
import * as circle from './circle';
console.log(circle.circleCircunference(5));
```

### Rótulos

É possível rotular uma variável (_label_) para atribuir um nome diferente.

```javascript
import {circleCircunference as circunference} from '.circle';
console.log(circunference(5));
```

### Características dos módulos

  1. **Módulos são singletons**: isso significa que mesmo que um módulo seja importado múltiplas vezes dentro de um projeto, somente uma “instância” dele vai existir.
  2. **Módulos podem importar coisas de outros módulos**: isso significa que é possível utilizar dentro de um módulo coisas que foram importadas de outros módulos que ele usa.
  3. **Importações de módulos são _hoisted_**: tudo o que é importado é movido internamente para o topo do escopo atual. Em outras palavras, tudo o que é importado estará disponível em qualquer momento, ainda que a declaração do `import` no módulo aconteça posteriormente no código.

```javascript
console.log(circleCircunference(5));
import circleCircunference from './circle';
```
