# SCSS | Referência Rápida

- Referência: [http://sass-lang.com/](http://sass-lang.com/)


## Index

1. [Convenções CSS](#convenções-css)
2. [Instalação](#instalação)
3. [SASS em linha de comando](#sass-em-linha-de-comando)
  - [Conversão e transpilação](#conversão-e-transpilação)
  - [Shell interativo SASS Script](#shell-interativo-sass-script)
4. [Comentários](#comentários)
5. [Importação e arquivos partials](#importação-e-arquivos-partials)
6. [Aninhamento de regras e propriedades](#aninhamento-de-regras-e-propriedades)
  - [Regras aninhadas](#regras-aninhadas)
  - [Propriedades com namespaces](#propriedades-com-namespaces)
7. [Variáveis](#variáveis)
8. [Tipos de dados](#tipos-de-dados)
  - [Definições](#definições)
  - [Tipos de dados no shell interativo](#tipos-de-dados-no-shell-interativo)
9. [Interpolação](#interpolação)
10. [Mixins](#mixins)
11. [Extend](#extend)
12. [Operações com strings](#operações-com-strings)
13. [Estrutura de decisão](#estrutura-de-decisão)
  - [@if](#@if)
14. [Estruturas de repetição](#estruturas-de-repetição)
  - [@for](#@for)
  - [@each](#@each)
  - [@while](#@while)
15. [Funções](#funções)
16. [Features não testadas](#features-não-testadas)
  - [Funções internas do SASS](#funções-internas-do-sass)

----------

## Convenções CSS

Uma regra ou ruleset é definida pelo conjunto seletor e declaração.
Uma declaração é definida pelo par propriedade-valor.

``` css
/* Regra (Ruleset) */
selector {
  /* Declaração */
  property: value;
}
```

## Instalação

``` bash
# Necessário instalar linguagem Ruby
dnf install ruby

# Instalar gem da biblioteca SASS
gem install sass
```

## SASS em linha de comando

### Conversão e transpilação

``` bash
# Conversão entre arquivos .scss e .sass
sass-convert stylesheet.sass stylesheet.scss
sass-convert stylesheet.scss stylesheet.sass

# Transpila manualmente um arquivo .sass para um arquivo .css
sass stylesheet.sass

# Transpila manualmente um arquivo .scss para um arquivo .css
sass stylesheet.scss stylesheet.css

# Transpila a cada novo comando save no arquivo .scss
sass --watch stylesheet.scss:stylesheet.css

# Modifica o estilo de saída do arquivo
sass stylesheet.scss stylesheet.css --style compressed
# --style: nested, expanded, compact, compressed
```

### Shell interativo SASS Script

``` bash
# Iniciar shell interativo
sass --interative
# ou
sass -i
```

## Comentários

``` scss
// Comentário de uma linha

/* Comentário de bloco */

/*!
Comentário de bloco com exclamação
Esse tipo de comentário não será excluído em arquivos minificados
*/
```

## Importação e arquivos partials

``` scss
// Extensões: .sass, .scss ou .css;
@import 'variables.scss';
@import 'reset.css';

// URLs: urls com HTTP
@import url('https://fonts.googleapis.com/css?family=Roboto');
```

Um arquivo parcial inicia seu nome com _**underscore**_: `_variables.scss`.
Os arquivos parcais são importados dentro do arquivo `.sass` ou `.scss` principal.

Para importação de uma parcial pode-se omitir seu **underscore** bem como sua extensão.

``` scss
// Importa um arquivo parcial por vez
@import 'variables';
@import 'mixins';
@import 'reset';
@import 'normalize';

// Importa vários arquivos parciais com apenas um declaração de importação
@import 'variables',
        'mixins',
        'reset',
        'normalize';
```

## Aninhamento de regras e propriedades

### Regras aninhadas
``` scss
body {       // body        {}
  header {}  // body header {}
  main   {}  // body main   {}
  footer {}  // body footer {}
}

// Operador de referência: &
.message {      // .message         {}
  &-success {}  // .message-success {}
  &-error   {}  // .message-error   {}
}

.content {     // .content        {}
  .title & {}  // .content .title {}
}
```

### Propriedades com namespaces

``` scss
// Propriedades aninhadas
.el {
  font: {
    weight: 700;
    size: 24px;
    family: sans-serif;
  }
}

.el {
  font: 24px/36px sans-serif {
    weight: 700;
  }
}
```

## Variáveis

``` scss
$var: 100%;                // variável global
html, body { width: $var; height: $var; }

main {
  $width: 100%;            // variável local
  $height: 100% !global;   // variável global

  $margin: null;           // variável nula
  $margin: auto !default;  // variável default
  margin: $margin;         // auto

  $margin: 10%;
  $margin: auto !default;
  margin: $margin;         // 10%
}
```

## Tipos de dados

### Definições

``` scss
// Número
$number: 1;
$number: 1px;

// String
$string: String;
$string: 'String';
$string: "String";

// Lista: conjunto de valores separados por vírgulas ou espaços
$list: 'Helvetica', 'Arial', sans-serif;
$list: 10px auto 0;

// Lista de listas: sublistas separadas por vírgulas
$list: 10px 20px, 30px 40px;
// Lista de listas: sublistas separadas por espaços
$list: (10px auto) (20px auto);

// Mapa
$map: (
  'key1': value1,
  'key2': value2,
  'key3': value3
);
.el {
  color: map-get( $map, key1);
}

// Cor
color: rgba(orange, .25);

// Boolean e Null
$var-t: true;
$var-f: false;
$var-n: null;
```

### Tipos de dados no shell interativo

Para verificar um tipo de dados usa-se a sintaxe: type_of(dado); # ou type-of(dado);

``` bash
>> sass -i
>> $var: 'Texto'
>> type-of($var)
"string"

>> type-of(2)
"number"

>> $var: #f00
>> type-of($var)
"color"
```

## Interpolação

``` scss
$property = 'width';
$PATH     = 'assets/images';

.el {
  #{$property} : auto;
  background-image: url('#{$PATH}/gradient.png');
}
```

## Mixins

``` scss
@mixin clearfix {
  &::after {
    content: '';
    clear: both;
    display: block;
  }
}
.row { @include clearfix; }

@mixin transition( $property: all, $duration: 300ms, $easing: linear ) {
  transition: $property $duration $easing;
}
.link { @include transition(); }
```

## Extend

``` scss
%message {
  border: 1px solid #c4c4c4;
}
.error, .success, .warning {
  @extend %message;
}
.error   { border-color: red; }
.success { border-color: green; }
.warning { border-color: yellow; }
```

## Operações com strings

``` scss
.string {
  &::before {
    content: 'Sans-' + serif;        // 'Sans-serif'
    font-family: sans- + 'serif';    // sans-serif
    margin: 12px + 12px auto;        // 24px auto
  }
  &::after {
    content: "#{12 + 12} pixels";    // 24 pixels
  }
}
```

## Estrutura de decisão

### @if

``` scss
@mixin message( $type: default ) {
  @if $type == error        { border-color: red; }
  @else if $type == success { border-color: green; }
  @else                     { border-color: gray; }
}
// É possível usar todos os operadores relacionais: <, >, !, ...
```

## Estruturas de repetição

### @for

``` scss
// 1 through 3: executa 3 vezes (inclusive)
@for $i from 1 through 3 {
  .item-#{$i} { z-index: $i; }
}

// 1 to 3: executa 2 vezes (exclusive)
@for $i from 1 to 3 {
  .item-#{$i} { z-index: $i; }
}
```

### @each

``` scss
@each $state in info, success, warning, error {
  .icon-#{$state} {
    background-image: url('assets/images/icon-#{$state}.png');
  }
}

$rgb-list: red, green, blue;
@each $color in $rgb-list {
  .rgb.#{$color} { color: $color; }
}
```

### @while

``` scss
$i: 5;
@while $i > 0 {
  .item-#{$i} { z-index: $i; }
}
$i: $i - 1;
```

## Funções

``` scss
// Função difere de mixin pois sempre retorna um valor
@function font-extra($value, $un: px) {
  $res: $value * 2;
  @return $res + $un;
}
.el {
  font-size: font-extra(24);  // 48px
}
```

----------

## Features não testadas

### Funções internas do SASS

``` scss
// Funções para cores HSL
$color: adjust-hue($color);
$color: lighten($color);
$color: darken($color);
$color: saturate($color);
$color: desaturate($color);
$color: hue($color);
$color: saturation($color);
$color: lightness($color);

// Mix de cores
$color: mix($color1, $color2, $percent);

// Alterações de cores
$color: grayscale($color);
$color: complement($color);
$color: invert($color);

// Opacidade
$color: alpha($cor);
$color: opacity($color);
$color: rgba($color, $alpha);
$color: opacify($color, $value);
$color: fade-in($color, $val);
$color: transparentize($color, $val);
$color: fade-out($color, $val);

// Funções para números
$var: percentage($num);
$var: round($round);
$var: ceil($prox-int);
$var: floor($ant-int);
$var: min($numbers-list);
$var: max($numbers-list);
$var: random($limit);

// Funções para strings
$var: quote($string);
$var: unquote($string);
$var: str-length($string);
$var: to-upper-case($string);
$var: to-lower-case($string);

// Funções para listas
$var: length($list);
$var: nth($list, $pos-item);
$var: set-nth($list, $pos-item, $new-value);

// Funções para mapas
$var: map-get($map, $key);
$var: map-merge($map1, $map2);
$var: map-remove($map, $keys);
```
