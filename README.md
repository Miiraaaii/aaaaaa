Banco Digital — Projeto SQL

Projeto de banco de dados relacional simulando um banco digital (estilo Nubank), com contas, cartões, transações e faturas. Desenvolvido em PostgreSQL na plataforma Supabase.

Diagrama Entidade-Relacionamento (DER)

**por a foto do DER**

(Diagrama gerado no dbdiagram.io mostrando o relacionamento entre clientes, contas, cartões, transações e faturas)

Estrutura do banco
clientes: dados cadastrais (nome, CPF, email)
contas: contas correntes e poupança, vinculadas a um cliente
cartoes: cartões de débito/crédito, vinculados a uma conta
transacoes: depósitos, saques, transferências e pagamentos
fatura_cartao: faturas mensais por cartão de crédito
Regras de negócio implementadas
Trigger de saldo automático: toda transação inserida na tabela transacoes atualiza o saldo da conta automaticamente, sem intervenção manual da aplicação (função atualizar_saldo() + trigger trigger_atualizar_saldo).
Constraints de integridade: saldo não pode ficar negativo, tipos de conta/cartão/transação são validados direto no banco via CHECK, e chaves estrangeiras garantem que uma conta só existe se o cliente existir (e o mesmo para cartão → conta).
View de extrato consolidado: extrato_consolidado junta transações, contas e clientes numa única consulta legível, com nomes e números em vez de apenas IDs.
Relatório de fatura por período: query que soma os gastos de cartão de crédito agrupados por mês.
Exemplo: trigger funcionando

Antes de inserir a transação (saldo original):

<img width="1417" height="882" alt="image" src="https://github.com/user-attachments/assets/95dcce96-caf7-436d-9868-93899f0116c1" />

**POR A DEVIDA IMAGEM**

Depois de inserir um depósito de R$100,00 (saldo atualizado automaticamente pela trigger):

**POR A DEVIDA IMAGEM**

Exemplo: extrato consolidado

**POR A DEVIDA IMAGEM**

Tecnologias utilizadas
PostgreSQL (hospedado via Supabase)
Mockaroo para geração de dados fake
dbdiagram.io para modelagem visual (DER)
Estrutura de arquivos
banco-digital-sql/
  ├── README.md
  ├── schema.sql        → criação de todas as tabelas, constraints e índices
  ├── seed-data.sql      → amostra dos dados de teste (INSERTs)
  └── queries.sql        → trigger, função, view e queries de relatório
Como rodar este projeto
Crie uma conta gratuita em supabase.com e crie um novo projeto.
Abra o SQL Editor do Supabase.
Execute o conteúdo de schema.sql para criar as tabelas.
Execute o conteúdo de seed-data.sql para popular o banco com dados de teste.
Execute o conteúdo de queries.sql para criar a trigger, a função e a view, e testar os relatórios.
Possíveis evoluções futuras
API REST sobre este banco (via Supabase Auto API ou FastAPI)
Autenticação de usuários com login por CPF/senha
Dashboard de visualização dos dados (ex: com Metabase ou Grafana)
