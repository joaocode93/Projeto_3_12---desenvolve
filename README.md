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

## 🖥️ View Criada

A `v_relatorio_vendas_detalhado` simplifica a análise diária:

```sql
SELECT *
FROM `seu-projeto.seu_dataset.v_relatorio_vendas_detalhado`
WHERE Estado_Cliente = 'RJ';
