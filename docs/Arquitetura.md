## Desenho da Arquitetura
### C1 - Contexto
![Contexto](./diagramasC4/c1.svg)

### C2 - Container
![Container](./diagramasC4/c2.svg)

**Obs:** Não haviam dados suficientes a respeito da volumetria diária total para calcular efetivamente os custos da utilização do sistema em nuvem, a estratégia utilizada foi organizar os componentes em serviços utilizando interfaces que possam substituir as atuais ferramentas no futuro, bem como as presentes ferramentas foram escolhidas com os seguintes critérios seguindo a precedencia apresentada: 
- **Especificações de utilização do projeto:** Como determinada ferramenta resolve as necessidades e problemas apresentados no escopo da aplicação.
 -  **Licenciamento open source**: Ferramentas que possam ser utilizadas sem custo de licenciamento para em ambiente produtivo ou desenvolvimento.
 - **Intercambialidade com serviços de nuvem**: Ferramentas que apresentem comportamentos semelhantes ou que tenham similares na nuvem: Ex. Kubernets (AKS, EKS, GKE).


|Componente| Tecnologia |
|--|--|
|Aplicação| *.Net Framework, React, Angular* |
|Api Proxy| *Apigee, Ngix* |
| Controle de Lançamentos API | .Net Core API |
| Lançamentos Database | Postgres |
| Lançamentos Broker | Apache Kafka|
| Telemetria | OpenTelemetry |
| Consolidação Financeira API | .Net Core API|
| Woker Consolidação financeira  | .Net Core|
| Consolidação Database | Mongo Db|
| Cache | Redis|