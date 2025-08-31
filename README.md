# 📊 Mini Projeto: Pipeline de Dados e Análise com SQL no BigQuery

Este projeto simula um **pipeline de dados para a Livraria DevSaber**, uma loja online que começou a registrar suas primeiras vendas e agora precisa transformar suas planilhas em um **mini data warehouse no Google BigQuery**.

## 🚀 Objetivo

Construir um pipeline completo de dados no BigQuery, passando por:
1. Estruturação das tabelas.
2. Inserção de dados.
3. Consultas analíticas.
4. Criação de uma VIEW para relatórios.

---

## 📂 Estrutura do Projeto

- **sql/**
  - `01_create_tables_bigquery.sql` → Criação das tabelas `Clientes`, `Produtos` e `Vendas`.
  - `02_insert_data_bigquery.sql` → Inserção dos dados brutos fornecidos.
  - `03_analysis_and_view_bigquery.sql` → Consultas SQL e criação da VIEW `v_relatorio_vendas_detalhado`.

---

## 🗂️ Modelo de Dados

- **Clientes**
  - ID_Cliente (INT64)
  - Nome_Cliente (STRING)
  - Email_Cliente (STRING)
  - Estado_Cliente (STRING)

- **Produtos**
  - ID_Produto (INT64)
  - Nome_Produto (STRING)
  - Categoria_Produto (STRING)
  - Preco_Produto (NUMERIC)

- **Vendas**
  - ID_Venda (INT64)
  - ID_Cliente (INT64)
  - ID_Produto (INT64)
  - Data_Venda (DATE)
  - Quantidade (INT64)

---

## 🔎 Consultas Analíticas

Exemplos de análises realizadas:

1. Clientes que moram em SP.
2. Produtos da categoria **Ficção Científica**.
3. Lista de vendas com nome do cliente, produto e data.
4. Valor total de cada venda.
5. Produto mais vendido por quantidade.

---

### 🔹 3. Com base nos dados brutos, quais outras duas tabelas poderíamos criar?

Além de `Clientes`, `Produtos` e `Vendas`, poderíamos criar:

1. **Tabela Funcionarios**  
   - `ID_Funcionario` (INT64)  
   - `Nome_Funcionario` (STRING)  
   - `Cargo` (STRING)  
   - `Email` (STRING)

2. **Tabela Fornecedores**  
   - `ID_Fornecedor` (INT64)  
   - `Nome_Fornecedor` (STRING)  
   - `Contato` (STRING)  
   - `Categoria_Produtos` (STRING)

Essas tabelas ajudariam a acompanhar **responsáveis pelas vendas** e **origem dos produtos**.

---

### 🔹 4. Se o BigQuery não tem chaves estrangeiras, como garantir integridade?

O BigQuery não valida automaticamente as relações, então a responsabilidade é do **analista/engenheiro de dados**:  
- Conferir consistência dos dados ao inserir registros.  
- Usar `JOIN` corretamente para relacionar as tabelas.  
- Criar processos de ETL ou scripts para validar IDs inexistentes.

---

### 🔹 5. Por que inserir clientes e produtos antes das vendas?

Inserir primeiro os **cadastros base** (clientes e produtos) garante:  
- Que todos os registros de vendas referenciem **entidades existentes**.  
- Facilidade em manter histórico de preços, categorias e dados dos clientes.  
- Melhora a organização e evita duplicações.

---

### 🔹 6. Em um cenário com milhões de vendas por dia, `INSERT INTO` seria ideal?

Não. Para grandes volumes, o ideal é:  
- **Carga em lote (batch load)** com arquivos CSV/Parquet.  
- Integração com pipelines ETL/ELT (Dataflow, Apache Beam, etc.).  
- Isso é muito mais rápido e econômico que inserir linha por linha com `INSERT INTO`.

---

### 🔹 7. Principal vantagem de uma `VIEW` em vez de salvar código em arquivo de texto?

- A `VIEW` **salva a lógica no banco** e sempre executa a consulta com dados atualizados.  
- Evita reescrever ou procurar scripts manualmente.  
- Permite versionamento, segurança e fácil compartilhamento.

---

### 🔹 8. O `Valor_Total` na VIEW será atualizado automaticamente?

Sim! O BigQuery recalcula o `Valor_Total` **toda vez que a view é consultada**.  
Se o preço em `Produtos` mudar, o resultado refletirá automaticamente a alteração, sem precisar reprocessar ou salvar dados manualmente.

---

## 🖥️ View Criada

A `v_relatorio_vendas_detalhado` simplifica a análise diária:

```sql
SELECT *
FROM `seu-projeto.seu_dataset.v_relatorio_vendas_detalhado`
WHERE Estado_Cliente = 'RJ';
