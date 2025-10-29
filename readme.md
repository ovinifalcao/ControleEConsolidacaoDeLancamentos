# Controle e Consolidação de Lançamentos

Versão: 1.0.0

Data: 2025-10-28

Por:  André Vinícius A. Falcão

## :dart: Objetivo
O presente repositório tem como objetivo fornecer uma Solução de Arquitetura Software adequada para o problema de um comerciante que visa: 
- Gravar todos os lançamentos de Débitos e Créditos de sua movimentação de caixa. 
- Consultar o relatório consolidado da movimentação diária. 

As escolhas arquiteturais e de software visão garantir a escalabilidade, resiliência, segurança e alta disponibilidade aos dados de lançamentos seguindo os requisitos à frente listados. 

## 🚨 Descrição do problema
Um comerciante precisa controlar seu fluxo de caixa diário com lançamentos (débitos e créditos) e gerar um relatório consolidado do saldo diário.  O serviço de  controle de lançamentos não pode ser impactado  caso o sistema de consolidado diário fique indisponível. Em dias de pico, o serviço de consolidado diário recebe  50 requisições por segundo, com  no máximo 5% de perda.

## 📖 Índice

* [Descrição do problema](#descrição-do-problema)
* [Definição de contextos](#definição-de-contextos)
    * [Controle de Lançamentos](#controle-de-lançamentos)
    * [Consolidação Financeira](#consolidação-financeira)
    * [Linguagem Compartilhada](#linguagem-compartilhada)
* [Requisitos](#requisitos)
* [Arquitetura](#arquitetura)

* [Como Executar](#como-executar)


##  :clipboard: Definição de contextos:

### Controle de Lançamentos:
 Responsável por receber, validar, e gravar cada um dos lançamentos feitos, possibilitando um relatório consolidado do movimento diário.

**Entidade Lançamento**
|Campo|Tipo| Descrição |
|--|--|--|
| Id | `Guid` | Identificador unitário de um evento de lançamento |
| Data | `DateTime`| Data e hora de geração do lançamento |
| NaturezaOperacao | `Enumeração` | Define o tipo daquele lançamento |
| Operador | `String` | Código de identificação do operador da lançamento |
| Descricao| `String` | Descrição opcional para o lançamento |
| Valor | `Double` | Valor do lançamento |
| NumeroLancamento| `Long` | Numero sequencial do referido lançamento |


**Enumeração Natureza Operação**
|Campo| Descrição |
|--|--|
| Crédito | Evento de entrada de valores ao Caixa |
| Débito | Evento de saída de valores do Caixa |
| Cancelamento de Crédito | Evento de estorno de valores saindo do Caixa |
| Cancelamento de Débito | Evento de estorno de valores voltando ao Caixa |


**Obs:** O tipo Guid foi utilizado na identificação para mitigar risco relacionados a valores de identificação sequenciais, considerando a devida perda de performance da indexação que será direcionada para o campo do Numero Lançamento, que por sua vez tem o seguinte comportamento: a cada lançamento da natureza: Crédito ou Débito um novo valor é criado, para os Cancelamentos o Numero Lançamento da transação original é repetido nesse campo relacionando os eventos sem sobrescrever o histórico.


### Consolidação Financeira:
 Responsável por gerar relatório consolidado diário com base nas informações recebidas do contexto de Controle de Lançamentos, e dispor deste relatório quando consultado.

**Entidade Consolidado**
|Campo|Tipo| Descrição |
|--|--|--|
| Id | `Guid` | Identificador unitário de um evento de lançamento |
| Data | `Date`| Data referencia da consolidação do relatório |
| DataCriacao | `DateTime`| Data da criação do registro |
| DataAlteracao | `DateTime`| Data da última alteração do registro |
| QuantidadeCredito| `int` | Sumariza a quantidade de eventos de lançamento de Crédito |
| ValorCredito| `Double` | Sumariza o valor de todas os eventos de lançamento de Crédito |
| QuantidadeCancelamentoCredito| `int` | Sumariza a quantidade de eventos de lançamento de cancelamento de Crédito |
| ValorCancelamentoCredito| `Double` | Sumariza o valor de todas os eventos de lançamento de cancelamento de Crédito |
| QuantidadeDebito| `int` | Sumariza a quantidade de eventos de lançamento de Debito |
| ValorDebito| `Double` | Sumariza o valor de todas os eventos de lançamento de Debito |
| QuantidadeCancelamentoDebito| `int` | Sumariza a quantidade de eventos de lançamento de cancelamento de Debito |
| ValorCancelamentoDebito| `Double` | Sumariza o valor de todas os eventos de lançamento de cancelamento de Debito |
| ValorTotal| `Double` | Valor final de todos os lançamentos |

## Linguagem Compartilhada:
  
|Termo | Definição|
|--|--|
|Caixa| Entidade que acumula os valores dos lançamentos|
|Cancelamento| Define evento de lançamento com objetivo de reverter as ações de crédito ou débito, sem sobrescrevê-las.|
|Controle de Lançamentos | Define o contexto acima citado de mesmo nome, como especificado.|
|Consolidação Financeira | Define o contexto acima citado de mesmo nome, como especificado.|
|Crédito| Define evento de lançamento onde há entrada de valores no caixa.|
|Débitos| Define evento de lançamento onde há saída de valores do caixa.|
|Lançamento| Unidade do evento do registro de uma operação da movimentação do caixa. |
|Relatório| Entidade que mostra os valores finais sumarizados de todos os lançamentos de um dia. |

## :memo: Requisitos
Consulte a documentação de Requisitos para a ler a definição completa: [aqui](https://github.com/ovinifalcao/ControleEConsolidacaoDeLancamentos/blob/main/docs/Requisitos.md).

## :classical_building: Arquitetura
Consulte a documentação de Arquitetura para a ler a definição completa: [aqui](https://github.com/ovinifalcao/ControleEConsolidacaoDeLancamentos/blob/main/docs/Arquitetura.md).

Para mais informações sobre as decisões de tecnologia, consulte as ADR (Architecture Decision Record):

- [ADR: 001 - Escolha da arquitetura de Microsserviços](https://github.com/ovinifalcao/ControleEConsolidacaoDeLancamentos/blob/main/docs/ADR/001.md)

- [ADR: 002 - Escolha da arquitetura das Operações Como Eventos Únicos](https://github.com/ovinifalcao/ControleEConsolidacaoDeLancamentos/blob/main/docs/ADR/002.md)

- [ADR: 003 - Ausência da da Escolha da Tecnologia de Interface com o Cliente](https://github.com/ovinifalcao/ControleEConsolidacaoDeLancamentos/blob/main/docs/ADR/003.md)

- [ADR: 004 - Escolha de tecnologia para Controle de Lançamentos API](https://github.com/ovinifalcao/ControleEConsolidacaoDeLancamentos/blob/main/docs/ADR/004.md)


## Como Executar
Consulte os repositórios das soluções, a sessão *read-me* dispõe de todas as informações de necessárias para a execução de cada contexto:

[Controle de Lançamentos](https://github.com/ovinifalcao/ControleLancamentosAPI)

[Consolidação Financeira](https://github.com/ovinifalcao/ConsolidacaoFinanceiraAPI)

