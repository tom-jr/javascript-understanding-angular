# Components Overview

Components são os principais blocos de construções para aplicações angular. Cada component consiste de:
- Um HTML template que declara o que será renderizada na página
- Uma classe Typescript que define o comportamento
- Um CSS seletor, sendo opcional

## Criando um component

O melhor caminho para se criar um component é usando o Angular CLI. Tbm podemos criar um component de forma manual.

### Criar usando o CLI
Para criar um component usando Angular CLI 
1. em um terminal aberto dentro do diretório rodamos o comando 
~~~ bash
ng generate component <name-component>
~~~
Onde <name-component> é o nome que definimos do nosso component

Por default o comando cria esses arquivos:
- Um diretório com o nome do component
- Um component file, nome-component.component.ts
- Um template HTML, nome-component.component.html
- Um CSS, nome-component.component.css
- Um arquivo de teste, nome-component.component.spec.ts


### criando um component manualmente

Embora o angular CLI seja a melhor forma de criar components, nos podemos tbm criar components de forma manual.
Para criar manualmente um component:

1. No diretório do nosso projeto criamos um arquivo chamado <component-nome>.component.ts

3. No top do nosso arquivo adicionamos o import 
~~~ javascript
import { Component } from '@angular/core';
~~~

4. Adicionamos um decorator de **@Component**
~~~ javascript
@Component({})
~~~

5. adicionemos um css selector para o component

~~~ javascript
@Component({
    selector: 'app-component'
})
~~~

6. definir um html template que é o path ou inline do html(template) do component que definimos
~~~ javascript
@Component({
    selector: 'app-component.css',
    templateUrl: 'app-component.html'
})
~~~

7. Definimos o styleUrls que é um array com paths ou inline dos CSS's do component que estamos definindo.

~~~ javascript
@Component({
    selector: 'app-component.css',
    templateUrl: 'app-component.html',
    styleUrls: '[app.component.css]'
})
~~~

8. adicionamos a definição da class ts do component
~~~ javascript
export class AppComponent {

}
~~~

## Especificando um CSS selector
Todo component requer um css selector. Um selector é a definição pela qual será definido a chamada do component.
Por exemplo um component com essa definição

~~~ javascript
@Component({
    selector:'name-component'
})
export class NameComponent {}
~~~
caso queiramos fazer uso desse component em outro component utilizaremos o selector como a definição de um elemento:

~~~ html
<root>
    <name-component></name-component>
</root>
~~~

## Definindo um template
O template é um bloco de html que define como o component será renderizado, um component pode ser definido de duas maneiras:
- Pela referencia de um arquivo externo
- Inline, definição do html diretamente em sua especificação no decorator **_@Component_**

ex external file:
~~~ javascript
@Component({
    selector:'name-component',
    templateUrl: 'name.component.html'
})
export class NameComponent {}
~~~

ex inline:

~~~ javascript
@Component({
    selector:'name-component',
    template: '<h1> Heading </h1>'
})
export class NameComponent {}
~~~

podemos usar o template string para termos mais liberdade de edição

~~~ javascript
@Component({
    selector:'name-component',
    template: `
    <h1> Heading </h1>
    <p>Paragraph</p>
    `
})
export class NameComponent {}
~~~

Um template é definido por templateUrl ou template. Não é permite usar ambos em um component

## Declarando um component style

Declaramos os styles de um component por dois caminhos possíveis
- Por referencia de um arquivo externo
- Inline declaration, onde diretamente declaramos os scripts de styles

Por referencia:


~~~ javascript
@Component({
    selector:'name-component',
    templateUrl: 'name.component.html',
    styleUrls: ['name.component.css']

})
export class NameComponent {}
~~~

Inline

~~~ javascript
@Component({
    selector:'name-component',
    templateUrl: 'name.component.html',
    styles: ['h1 {font-weight: normal;}']
})
export class NameComponent {}
~~~

em ambos exemplos é declarado como array, posso ter array com n arquivos de style e n declarações inline de styles
