# 📊 Case Técnico: Analista de Integração de Dados — Systock

Resolução do case técnico para a posição de Analista de Integração de Dados (Implantação). O projeto contempla a modelagem, tratamento de dados, consultas analíticas e automação no PostgreSQL, além da estratégia de validação com o cliente final.

---

## 🛠️ Tecnologias Utilizadas
- Banco de Dados: PostgreSQL
- SGBD / IDE: DBeaver
- Linguagem: SQL / PL/pgSQL

---

## 🚀 Resumo da Solução por Partes

### ✍️ Parte 1 – Documentação do Processo de Importação
- Ferramenta: DBeaver (Task de Importação de Dados) e scripts SQL de staging.
- Estrutura e Tratamento: Importação inicial de campos numéricos/valores como texto (VARCHAR) para higienização. Aplicação de REPLACE para conversão do separador decimal brasileiro (vírgula) para o padrão de banco de dados (ponto), seguido do CAST para NUMERIC e FLOAT8.
- Correções no DDL: Ajuste de inconsistências na estrutura original das tabelas (como vírgula ausente antes de CONSTRAINT na tabela de produtos e compatibilização dos nomes das chaves produto_id).

### ✍️ Parte 2 – Consultas SQL Básicas
- Consumo por Produto (Fevereiro/2025): Agrupamento por produto trazendo SUM(qtde_vendida) e o valor total acumulado em R$ no período.
- Produtos Pendentes: Consulta na tabela pedido_compra identificando itens requisitados onde qtde_pendente > 0 ou qtde_entregue < qtde_pedida.

### ✍️ Parte 3 – Transformações de Dados e Trigger
- Formatos de Exibição: Concatenação de código e descrição (produto_id || ' - ' || descricao_produto) e formatação de datas via TO_CHAR(data, 'DD/MM/YYYY').
- Filtros de Agrupamento: Uso de HAVING COUNT(*) > 10 para identificar produtos de alta frequência de requisição.
- Automação com Trigger: Criação da função fn_gerar_id_fornecedor() e da trigger trg_gerar_id_fornecedor executando BEFORE INSERT para atribuição automática do próximo idfornecedor numérico incremental.

### ✍️ Parte 4 – Estratégia de Validação com o Cliente
1. Pontos de Validação: Batimento de totais de vendas (R$), contagem total de itens em estoque vs. relatório do sistema anterior e checagem de pedidos com entregas parciais.
2. Garantia de Exatidão: Execução de testes de amostragem por curva ABC de produtos e validação de batimento de caixa/fechamento diário do mês de Fevereiro/2025.
3. Queries de Apoio: Consultas consolidadas de totalizadores deixadas prontas para execução em tempo real durante a reunião de validação.

---

## 📁 Arquivos do Repositório

- script_banco.sql: Backup/script DDL e DML completo contendo a criação das tabelas corrigidas, tratamento dos dados, consultas analíticas das partes 2 e 3 e a trigger em PL/pgSQL.

---

## 👤 Candidato

Fernando Santana