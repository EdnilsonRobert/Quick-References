# VueJS | Referência Rápida

## Início rápido

``` html
<div id="app"></div>

<script src="./resources/js/vue-2.5.16/vue.js"></script>
<script>
var app = new Vue({
    el: '#app'
});
</script>
```

## Renderização de dados

``` html
<h1 v-bind:title="title">{{ title }}</h1>
<h2 :title="tagline">{{ tagline }}</h2>

<script>
var app = new Vue({
    data: {
        title: 'Hello, Vue.js!',
        tagline: 'Introdução ao VueJS.'
    }
});
</script>
```

## Estrutura de decisão

``` html
<p v-if="ifTrue">{{ returnIf }}</p>

<script>
var app = new Vue({
    data: {
        ifTrue: true,
        returnIf: 'Verdadeiro.'
    }
});
</script>
```

## Estrutura de repetição

``` html
<ul>
    <li v-for="each in loopLines">{{ each.line }}</li>
</ul>

<script>
var app = new Vue({
    data: {
        loopLines: [
            { line: 'Linha 1.' },
            { line: 'Linha 2.' },
            { line: 'Linha 3.' }
        ]
    }
});
</script>
```

## Tags HTML como valores

``` html
<p v-html="html"></p>

<script>
var app = new Vue({
    data: {
        html: '<span>Texto dentro da tag Span.</span>'
    }
});
</script>
```

## Componentes

``` html
<awesome-component v-bind:someProperty="someText"></awesome-component>

<script>
Vue.component('awesome-component', {
    props: ['someProperty'],
    template: '<p>{{ someProperty }}</p>'
});

var app = new Vue({
    el: 'app',
    data: {
        someText: 'Um componente incrível.'
    }
});
</script>
```

## Filtros

``` html
<p>{{ 99.4598763 | floatToBRL }}</p>

<script>
var app = new Vue({
    filters: {
        floatToBRL: function(value) {
            return ('R$ ' + (value).toFixed(2)).replace('.',',');
        }
    }
});
</script>
```

## Métodos

``` html
<ul>
    <li v-for="each in loopLines">
        {{ each.title }} ({{ each.description}}): {{ each.value | floatToBRL }}
    </li>
</ul>
<p>Valor total: {{ totalValue() | floatToBRL }}</p>
<p>Iterações: {{ counterMethod }}</p>

<script>
var app = new Vue({
    data: {
        loopLines: [
            { title: 'Título 1.', description: 'Descrição 1', value: 25.34576 },
            { title: 'Título 2.', description: 'Descrição 2', value: 35.45458 },
            { title: 'Título 3.', description: 'Descrição 3', value: 78.45454 }
        ],
        counterMethod: 0
    },
    methods: {
        totalValue: function() {
            this.counterMethod++;
            var total = 0;
            for( item of this.loopLines) {
                total += item.valor;
            }
            return total;
        }
    }
});
</script>
```

## Métodos computados

``` html
<ul>
    <li v-for="each in loopLines">
        {{ each.title }} ({{ each.description}}): {{ each.value | floatToBRL }}
    </li>
</ul>
<p>Valor total: {{ totalValue | floatToBRL }}</p>
<p>Iterações: {{ counterComputed }}</p>

<script>
var app = new Vue({
    data: {
        loopLines: [
            { title: 'Título 1.', description: 'Descrição 1', value: 25.34576 },
            { title: 'Título 2.', description: 'Descrição 2', value: 35.45458 },
            { title: 'Título 3.', description: 'Descrição 3', value: 78.45454 }
        ],
        counterComputed: 0
    },
    computed: {
        totalValue: function() {
            this.counterComputed++;
            var total = 0;
            for( item of this.loopLines) {
                total += item.valor;
            }
            return total;
        }
    }
});
</script>
```

## Campos de formulários

``` html
<input type="text" v-model="inputText">
<p>Entrada no campo: {{ inputText }}</p>

<textarea v-model="textarea" rows="8" cols="80"></textarea>
<p>Entrada no campo: {{ textarea }}</p>

<input type="checkbox" v-model="inputCheckbox"> Input tipo Checkbox
<p>Checkbox: {{ inputCheckbox }}</p>

<input type="checkbox" v-model="inputCheckboxes" value="checkValues1"> Input 1 tipo Checkbox
<input type="checkbox" v-model="inputCheckboxes" value="checkValues2"> Input 2 tipo Checkbox
<input type="checkbox" v-model="inputCheckboxes" value="checkValues3"> Input 3 tipo Checkbox
<p>Checkbox: {{ inputCheckboxes }}</p>

<script>
var app = new Vue({
    data: {
        inputText: '',
        textarea: '',
        inputCheckbox: false,
        inputCheckboxes: []
    }
});
</script>
```

<!--
``` html
<script>
var app = new Vue({
    el: 'app'
});
</script>
```
-->
