# 📊 Dashboard de Avaliação de Produtos

![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)
![Ferramentas](https://img.shields.io/badge/Metabase-DNC-blue)
![Banco](https://img.shields.io/badge/Database-SQL%20Server%20%7C%20MySQL-lightgrey)
![Linguagem](https://img.shields.io/badge/SQL-Queries-orange)

## 📌 Visão Geral

Este projeto consiste em uma **análise de dados desenvolvida no Metabase**, utilizando **SQL Server e MySQL** como SGBDs, como parte da formação em **Análise de Dados da Escola DNC**.

O objetivo do dashboard é analisar **avaliações de produtos**, explorando métricas como quantidade de reviews, média de avaliações, desempenho por categoria e ranking dos produtos mais bem avaliados.

---

## 🛠️ Ferramentas e Tecnologias Utilizadas

* **Metabase** (criação de dashboards e visualizações)
* **SQL Server**
* **MySQL**
* **SQL (Queries analíticas)**
* **Dataset relacional (Orders, Products e Reviews)**

> ⚠️ **Observação:** Durante o projeto, o banco de dados foi migrado de **SQL Server para MySQL**, por isso algumas consultas seguem sintaxes específicas de cada SGBD.

---

## 🗂️ Estrutura dos Dados

O projeto utiliza três tabelas principais:

* **Products** → informações dos produtos (ID, título e categoria)
* **Reviews** → avaliações e notas atribuídas aos produtos
* **Orders** → pedidos realizados, utilizados para análise de volume

Essas tabelas foram relacionadas para permitir análises agregadas e comparativas.

---

## 📈 Métricas e Análises Desenvolvidas

### 🔢 Quantidade Total de Reviews

Mede o volume total de avaliações registradas na base.

```sql
SELECT COUNT(*) FROM Reviews;
```

---

### 📦 Quantidade de Produtos Avaliados por Categoria

Analisa quantos produtos distintos receberam avaliações em cada categoria.

```sql
SELECT
    COUNT(DISTINCT Products.id) AS Qtd,
    Category
FROM Reviews
LEFT JOIN Products ON Reviews.Product_ID = Products.id
WHERE Products.id IS NOT NULL
GROUP BY Category
ORDER BY Qtd DESC;
```

---

### 🏆 TOP 10 Produtos com Melhor Média de Avaliação

Ranking dos produtos com as **maiores médias de avaliação**.

```sql
SELECT
    AVG(Reviews.Rating) AS "Média",
    Products.ID,
    Title
FROM Reviews
LEFT JOIN Products ON Reviews.Product_ID = Products.id
GROUP BY Products.id
ORDER BY AVG(Reviews.Rating) DESC
LIMIT 10;
```

---

### 📋 Tabela de Média e Quantidade de Avaliações por Produto

Exibe os produtos mais avaliados, considerando **volume de pedidos** e **nota média**.

```sql
SELECT
   COUNT(Orders.id) AS Qtd,
   AVG(Rating) AS Nota,
   Products.id,
   Title,
   Category
FROM Orders
LEFT JOIN Products ON Orders.Product_ID = Products.id
GROUP BY Products.id
ORDER BY COUNT(Orders.id) DESC
LIMIT 15;
```

---

### 🎯 Média Geral das Avaliações (Radar)

Métrica geral que representa a **nota média global** dos produtos.

```sql
SELECT AVG(Rating) FROM Reviews;
```

---

### 📊 Média de Avaliações por Categoria

Permite comparar o desempenho médio entre as categorias.

```sql
SELECT
    AVG(Reviews.Rating) AS Media,
    Category
FROM Reviews
LEFT JOIN Products ON Reviews.Product_ID = Products.id
WHERE Products.Category IS NOT NULL
GROUP BY Category;
```

---

## 📌 Dashboard Final

O dashboard reúne todas essas análises em um painel visual interativo no **Metabase**, facilitando a interpretação dos dados e a tomada de decisão baseada em métricas.

🔗 Ambiente de dados:
> https://dex.dnc.group/browse

## 🖼️ Dashboard de Avaliação de Produtos

![Dashboard de Avaliações](dashboard_avaliacao_produtos.png)

Principais insights gerados:

* Volume total de avaliações registradas
* Categorias com maior número de produtos avaliados
* Produtos com melhor desempenho em avaliações
* Comparação de médias entre categorias

---

## 🚀 Aprendizados

* Construção de queries analíticas em SQL
* Diferenças práticas entre **SQL Server e MySQL**
* Modelagem de métricas para dashboards
* Análise de dados orientada a negócio
* Criação de visualizações claras e objetivas

---

## 📎 Status do Projeto

✅ **Concluído**

---

📌 *Projeto desenvolvido para fins educacionais durante a formação em Análise de Dados pela Escola DNC.*
