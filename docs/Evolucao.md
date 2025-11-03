# Oportunidades de Evolução

  

Por tratar-se de um projeto de demonstração, as implementações não consideram observar todas as melhores práticas de desenvolvimento, ainda que se preocupem com um nível elevado de coesão, reutilização, limpeza de código e de cobertura de testes. No entanto, os seguintes pontos são considerados:

  

-  **Evolução dos testes:** Garantir um ambiente de testes integrados mais próximo daquele que for escolhido para implementação de produção. Caso exista a troca de algum dos presentes serviços para alguma das ferramentas de nuvem intercambiáveis sugeridas é possível trocar a imagem docker para aquela que seja equivalente ao serviço do provedor de nuvem. Essa abordagem ajudaria a aumentar a cobertura e aprofundar os testes de unidade para garantir a coesão da estrutura.

  

-  **Validação combinada:** Aumentar o escopo das validações no serviço de lançamentos para garantir coesão não apenas sistêmica, mas também operacional. Isso significa, garantir via código de válidação os comportamentos esperados do usuário, protegendo o operador de casos comuns de erros conhecidos. Um exemplo poderia ser tratar o caso de receber mais de uma vez uma operação de mesmo valor e mesmo operador em um curtíssimo espaço de tempo.

  

## Melhorias Incrementais

Ficaram de fora da realização no código apresentado nos repositórios alguns itens que foram considerados menos importantes para o objetivo desta construção. O foco da implementação era em provar o conceito da arquitetura escolhida e possibilitar a coleta de resultados de performance que pudessem ser utilizados para sanar os requisitos apresentados. Portanto, consideram-se melhorias incrementais:

  

-  **Criação do frontend:** A criação deste item ficou suspensa devido à discussão apresentada na ADR, onde se põe em pauta a necessidade de obter critérios mais definidos para o levantamento de requisitos.

  

-  **Configuração do NGINX:** A criação deste item foi postergada pois não impactava a apresentação das funcionalidades *core*, - uma vez que esse repositório não deve ser utilizado em produção - entende-se que no ambiente de validação tecnica não mostraria suas vantagens. Mas sua configuração posterior é importante para garantir a conformidade com a `ADR003`.

- **Cache de Token**: A aplicação frontend pode prover um cache implementado com as ferramentas disponíveis na tecnologia escolhida para garantir que o token seja reutilizado durante um tempo equivalente ao tempo de expiração do próprio token, garantindo assim menor tempo em cada requisição.

- **Configuração da Ferramenta de Observabilidade**:  Com os dados fornecidos pelo Open Telemetry algumas métricas e alertas são recomendados com base na sessão de resultados.
	- Métricas
		- Quantidade de requisições com sucesso
		- Quantidade de Requisições com resposta 4XX
		- Quantidade de Requisições com resposta 5XX
		- Quantidade de mensagens com ACK no Tópico
	- Alertas
		- Quantidade de requisições da `ControleLancamentosAPI` acima de 800/segundo, para solicitar avaliação de escala do serviço.
		- Serviços em estado de unhelthly.
		- Aumento da taxa moda de erros 5XX nas APIs.
		-  Aumento da taxa moda de exceções no `ConsolidacaoFinanceiraWoker`