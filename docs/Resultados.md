
# Resultados de Performance
Nessa sessão são discutidos os resultados de performance para verificar a conformidade do sistema com os requisitos: `RNF01` `RNF02`. Para a realização foi utilizado o seguinte ambiente: 
- Todas as dependências criadas nos repositórios rodavam simultaneamente, bem como todas as aplicações. 
- O servidor de autenticação também estava rodando para fornecer requisições com assinatura de Token.
- Os testes sobre as três aplicações rodaram simultaneamente orquestrados pela aplicação: Jmeter.

### Configurações de Máquina
- 11th Gen Intel(R) Core(TM) i7 @ 2.80GHz
- 12gb de Ram
- SO: Windows 11 24h2

### Configurações de Requisições
A `ControleLancamentosAPI` foi parametrizada com um body capaz de produzir diferentes valores para as propriedades principais afim de gerar comportamentos diferentes na aplicação `ConsolidacaoFinanceiraWorker`.
 

    {  
      "natureza":  ${__Random(1,  4)},  
      "operador":  "102030",  
      "descricao":  "Teste Entrada",  
      "valor":  ${__Random(1,  1000)}  
    }

A `ControleLancamentosAPI` foi parametrizada com a data fixa de hoje, uma vez que todos os registros lançados pela aplicação de lançamentos serão feitos no mesmo dia.

    /ObterRelatorio/2025-11-03

Ambas as aplicações tiveram os headers configurados com o token para considerar no teste de performance a implicação do tempo de Autorização.

## Resultados
| Qtd. de Requisições|`ControleLancamentosAPI`  | `ControleLancamentosAPI`|
|--|--|--|
| 50/100 | 450ms  / 0% | 15ms  / 0% |
| 50/100 | 245ms  / 0% | 15ms  / 0% |
| 300/150| 1086ms  / 0% | 172ms  / 0% |
| 1000/500 | 2543ms  / 0% | 147ms  / 0% |

*Considere os valores de `Qtd. de Requisições` na mesma respectiva ordem das colunas.
*Considere nas demais colunas a seguinte ordem: Tempo médio / Taxa de erros.

## Conclusão
A estrutura proposta atende os requisitos de performance apresentados. Para esse testes são excluídos prejuízos que possam haver em relação a redes virtuais ou conexão com o cliente. Vale também dizer que para o caso do requisições simultâneas da aplicação `ControleLancamentosAPI` ser superior a 1000 é necessário pensar estratégias de escalonamento, os PAAS apresentados na solução possuem algumas configurações porém o Kubernetes poderia ser uma solução mais adequada. 