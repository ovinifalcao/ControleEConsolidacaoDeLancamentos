# :moneybag: Custos de Implementação
Como foi apresentado na sessão de Arquitetura, não foram apresentados dados de volumentria diária, ou segregada por qualquer outro período. Não sendo possível deduzi-la sem informações adicionais sobre a natureza do negócio tornasse importante propor ao cliente um rodada de refinamento onde essas métricas possam ser obtidas ou no caso de um ambiente completamente novo, obter informações de outras naturezas que ajudem a dimensionar o serviço corretamente. Para o presente estudo está sendo considerado o menor custo de implantação para serviços de nuvem que possam escalar dentro do necessário para atender o negócio. Foram considerados os principais provedores de nuvem para a análise a seguir: GCP, Azure e AWS. 

## Considerações sobre o relatório
- O relatório de cotação apresentado aqui é uma estimativa.
- O relatório considera que alguns serviços de nuvem proveem *Free Tiers*, camadas gratuitas que são destinadas a aplicações de teste, não recomendas para produção.
- Todos os serviços aqui simulam a localização mais barata para operação. Os valores podem ser diferentes se a operação fiscal exigida pela legislação do país impedir a remoção dos dados do território nacional.
- Se o cliente já tiver algum outro serviço ou contrato ativo com um dos provedores de nuvem os custos podem ficar diferentes na disperção do tempo de computação utilizado por alguns PAAS.
- Os serviços de frontend e telemetria foram deixados de fora dessa análise por estatem em aberto nas definições de ADRs.
- Alguns valores são aproximados.
- Os valores são apresentados em dólares.


| Serviço | Azure | GCP | AWS |
|--|--|--|--|
| Serviço de Aplicativo | - | - | - |
| Funções | -| - | - |
| Mensageria | $0.60 / 1MOp | $40,00 / Tb | $0,50 / 1MOp |
| Banco Relacional | $60 ^10gb  | $60 ^10gb  | $60 ^10gb |
| Banco de Documentos | $15/mês  | $11/mês   | $22/mês  |
| Cache | $15/mês  | $35/mês   | $13/mês  |
| Maquina Virtual  | $15/mês  | $4/mês  |  $7/mês  |
| **Total**  | $91/mês  | $110/mês  |  $103/mês  |

**Legenda:** 
 - MOp - Por Milhão de Operações.
 - ^ - Acima de.

 **Mapa de serviços e Produtos**
- Serviço de Aplicativo - `Controle de Lançamentos API` `Consolidacao Financeira API`
- Funções - `Consolidacao Financeira Worker`
- Mensageria - `Lançamentos Broker`
- Banco Relacional - `Lançamentos DB`
- Banco de Documentos - `Consolidação DB`
- Cache - `Consolidado Cache`
- Maquina Virtual - `Api Proxy` `Servidor de Identidade`