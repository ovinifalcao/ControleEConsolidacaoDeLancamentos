## Desenho da Arquitetura
### C1 - Contexto
![Contexto](docs/diagramasC4/c1.svg)

### C2 - Container
![Container](docs/diagramasC4/c2.svg)

**Obs:** Não haviam dados suficientes a respeito da volumetria diária total para calcular efetivamente os custos da utilização do sistema em nuvem, a estratégia utilizada foi organizar os componentes em serviços utilizando interfaces que possam substituir as atuais ferramentas no futuro, bem como as presentes ferramentas foram escolhidas com os seguintes critérios seguindo a precedencia apresentada: 
- **Especificações de utilização do projeto:** Como determinada ferramenta resolve as necessidades e problemas apresentados no escopo da aplicação.
 -  **Licenciamento open source**: Ferramentas que possam ser utilizadas sem custo de licenciamento para em ambiente produtivo ou desenvolvimento.
 - **Intercambialidade com serviços de nuvem**: Ferramentas que apresentem comportamentos semelhantes ou que tenham similares na nuvem: Ex. Kubernets (AKS, EKS, GKE).


**Componentes:**
:large_blue_circle: **Aplicação**

:large_blue_circle: **Api Proxy**

:large_blue_circle: **Controle de Lançamentos**

:small_blue_diamond: **Controle de Lançamentos API** - .Net Core API

:small_blue_diamond: **Lançamentos Database** - Postgres 

:small_blue_diamond: **Lançamentos Broker** - Apache Kafka

:large_blue_circle: **Telemetria**

:small_blue_diamond: OpenTelemetry

:large_blue_circle: **Consolidação Financeira**

:small_blue_diamond: **Consolidação Financeira API** - .Net Core API

:small_blue_diamond: **Woker Consolidação financeira**  - .Net Core

:small_blue_diamond: **Consolidação Database** - Mongo Db

:small_blue_diamond: **Cache** - Redis
