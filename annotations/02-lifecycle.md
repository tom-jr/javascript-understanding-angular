# Component Lifecycle

A instancia de um component tem um ciclo de vida que inicia quando o angular instancia o component.ts
e renderiza-o. O ciclo de vida continua com a detecção de mudanças.
O ciclo do component termina quando o angular destrói o component e remove sua renderização da arvore DOM
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

## Sequencia de eventos lifecycle

Apos sua aplicação instancia um component ou diretiva por chamada de construtor, Angular chama os métodos hooks que
temos implementados em seus pontos apropriados.

Angula executa hooks na seguinte sequencia:

| método hook           | proposito                                                                                                                                                                  | timing                                                                                                                            |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| ngOnchange            | responde quando Angular seta ou reseta dados de inputs properties. O método recebe uma SimpleChange como objeto                                                            | Chamado antes do ngOnInit e sempre que over mudanças em dados vinculados                                                          |
| ngOnInit              | inicializa a diretiva ou component depois do Angular renderizar seus dados vinculados e definir os inputs do component ou diretiva                                         | Chamado uma vez depois da primeira chamada do ngOnchange. Continuará sendo chamado mesmo que o ngOnChange não tenha sido invocado |
| ngDoCheck             | Detecta e agi sobre mudanças que o Angular não pode ou não quer detectar sozinho                                                                                           | Chamado imediatamente apos o ngOnchange em cada detecção de mudança e imediatamente apos o ngOnInit                               |
| ngAfterContentInit    | Responde depois que o Angular projeta conteúdos externos dentro da view do component, ou dentro da view que uma directiva faz parte                                        | Chamada uma vez depois do ngDoCheck                                                                                               |
| ngAfterContentChecked | Responde depois que o Angular checa o conteúdo projetado dentro de uma directive ou component                                                                              | Chamado depois do ngAfterContentInit e cada chamada do ngDoCheck                                                                  |
| ngAfterViewInit       | Responde depois que o Angular inicia a view do component e dos components children ou da view que contém a directive                                                       | Chamado uma vez depois do ngAfterContentChecked                                                                                   |
| ngAfterViewChecked    | Responde depois do Angula checa as views do component e component's children ou views que contém directive                                                                 | Chamado depois de ngAfterViewInit e em cada subsequencia de ngAfterContentChecked                                                 |
| ngOnDestroy           | Limpeza pouco antes do Angular destruir a diretiva ou componente. Cancele assinaturas de Observables e desanexe manipuladores de eventos para evitar vazamentos de memória | Chamado imediatamente antes do Angula destruir o component ou directive                                                           |

