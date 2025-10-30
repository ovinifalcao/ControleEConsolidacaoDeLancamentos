# :clipboard: Requisitos 
Os requisitos a seguir são apresentados segundo a sua ordem de prioridade por contexto ou por especificação. Sendo o menor número de maior prioridade. Essa prioridade foi definida dada a sequinte precedencia: 

 1. Requisitos listados pelo cliente (Presentes no desafio).
 2. Consistencia da natureza da operação. (Consolidação, Auditabilidade, Consistencia dos valores.)
 3. Seguranças das operações.


**Funcionais:**

-  **Controle de Lançamentos:**

	- **RF01 -** Deve possuir uma interface que permita gravar cada lançamento.

	- **RF02** - Deve gravar os lançamentos com os tipos:
		- Crédito
		- Débito
		- Cancelamento de Créditos
		- Cancelamento de Débitos

	- **RF03** - Deve-se garantir que o histórico de lançamentos seja auditável.

  

-  **Consolidação Financeira:**

	- **RF04 -** Deve possuir interface que permita a consulta do relatório diário.

	- **RF05 -** Deve criar um novo registro de Consolidação Financeira para cada dia de movimentação de caixa.

	- **RF06 -** Deve alterar o registro consolidado para cada novo lançamento.

  

**Não Funcionais:**

- **RNF01 -** O contexto Consolidação Financeira deve ser capaz de receber 50 requisições por segundo, com máximo de 5% de falha. Perda máxima de 2.5 requisições a cada 50.

- **RNF02 -** O Contexto de Controle de lançamentos não pode ter sua performance impactada por falhas no contexto de Consolidação Financeira.

- **RNF03 -** O sistema deve ter estratégias de recuperação de falha e escalabilidade horizontal para garantir a disponibilidade.

- **RNF04 -** É necessário que as interações do sistema com usuários sejam protegidas por Autenticação e Autorização granular para cada tipo de evento.

- **RNF05 -** O sistema deve dispor de criptografia para garantir a segurança do dado em trânsito.

- **RNF06 -** O sistema deve possuir alertas baseados em sua observabilidade para garantir a atuação da sustentação se necessário.

