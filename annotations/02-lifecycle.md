# Component Lifecycle

A instancia de um component tem um ciclo de vida que inicia quando o angular instancia o component.ts
e renderiza-o. O ciclo de vida continua com a detecção de mudanças. 
O ciclo do component termina quando o angular destrói o component e remove sua renderização da  arvore DOM
Nossa application pode usar métodos **_lifecycle hooks_** para explorar os eventos de lifecycle de um 
component ou diretiva para iniciar novas instancias, realizar updates de dados quando tal lifecycle for 
ativado e realizar um clean-up quando o component for destruído.

## Respondendo a um evento de lifecycle
Responda a um lifecycle de um component ou diretiva por meio de um método **_lifecycle hook_**. Os **_hooks_**
nos dão a oportunidade de agir em um component ou diretiva no momento de um lifecycle. Podendo criar, atualizar, ler
e deletar.

Os métodos hooks são implementados a partir de interfaces do package do **_@angular/core_**
Cada interface é responsável por um hook. Por exemplo a interface **OnInit** tem o contrato por meio do método
**ngOnInit()**. Se nos implementarmos esse método em nosso component ou diretiva, o angular chama o método logo apos
a checagem das inputs properties do component pela primeira vez

~~~ javascript
import {Directive}from '@angular/core';

@Directive({selector:['appPeekABook']})
export class PeekABook implements OnInit {

    constructor(private logger: LoggerService) {}

    ngOnInit(): void {
        this.logThis('OnInit');
    }

    logThis(value: string) {
        logger.log(value);
    }
}
~~~

Não temos a obrigação de implementar nenhum lifecycle hook em nosso comp/directive. Podemos add de acordo com nossas
necessidades.