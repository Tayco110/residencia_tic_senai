# 📊 Atividade Prática — Construção de Data Warehouse com PySpark e Arquitetura Medalhão

Este repositório contém a atividade prática destinada aos bolsistas participantes do projeto de Data Warehouse. O objetivo é uma experiência de ponta a ponta na ingestão, modelagem e análise de dados públicos usando **PySpark**, **Jupyter Notebooks** e a **Arquitetura Medalhão**.

---

## 📚 Conceitos que precisam ser estudados

Antes de iniciar a atividade, os participantes devem compreender os seguintes tópicos:

* **Arquitetura de Dados**:

  * Conceito de Data Lakes e Data Warehouses
  * Arquitetura Medalhão: Landing → Raw → Trusted → Refined
  * Conceito de Tabelas Fato e Dimensão
* **PySpark**:

  * Criação e manipulação de DataFrames
  * Leitura e escrita de arquivos Delta
  * Operações de Join e transformação de dados
* **Delta Lake**:

  * Versionamento de dados
  * Time travel
  * Atualizações e merges
* **Jupyter Notebooks**:

  * Organização modular de notebooks
  * Visualização de resultados com `display()`, `show()` e gráficos básicos
* **Paginação em APIs REST**

  * Consumo de dados públicos via APIs RESTful
  * Tratamento de múltiplas páginas de resultados

---

## 🌐 Endpoints públicos a serem utilizados

Os dados devem ser extraídos dos portais de dados abertos do Governo Federal. Abaixo, estão as listadas as informações que devem compor o mini data warehouse:

1. **Empresas registradas na Receita Federal (base CNPJ):**
2. **Municípios do Brasil:**
3. **Natureza Jurídica:**
4. **Empresas por município (fato):**
5. **Simples Nacional:**

Todos os endpoints exigem paginação ou múltiplas requisições. Deve  ser implementado o controle de página, cursor ou offset conforme a documentação de cada API. **Usar apenas uma amostra dos dados**

---

## 🛠 Requisitos de ferramentas

Deve-se configurar um ambiente local com os seguintes requisitos:

* **Python 3.10+**
* **Apache Spark 3.5+** com suporte a Delta Lake
* **Bibliotecas Python**:

  * `pyspark`
  * `requests`
  * `delta-spark`
* **Jupyter Notebook** ou **JupyterLab**

---

## 🏗 Camadas a serem alimentadas (Arquitetura Medalhão)

A pipeline deve seguir a estrutura:

1. **Landing**: Dados brutos, diretamente como retornado pela API, em formato JSON ou CSV.
2. **Raw**: Conversão dos dados para esquema estruturado e padronizado (DataFrame).
3. **Trusted**: Aplicação de regras de consistência, joins entre fatos e dimensões e enrichments.

---

## 🔗 Dados que devem ser cruzados

Os dados devem ser integrados da seguinte forma:

* A **tabela fato** será composta pelos dados das empresas (CNPJ).
* Tabelas **dimensões**:

  * CNAE (atividade econômica)
  * Município (localidade)
  * Natureza Jurídica
  * Simples Nacional (status tributário)

As relações a serem criadas são:

| Tabela Fato | Chave de Relacionamento    | Tabela Dimensão   |
| ----------- | -------------------------- | ----------------- |
| CNPJ        | `codigo_cnae`              | CNAE              |
| CNPJ        | `codigo_municipio`         | Municípios (IBGE) |
| CNPJ        | `codigo_natureza_juridica` | Natureza Jurídica |
| CNPJ        | `cnpj`                     | Simples Nacional  |

---

## 🧩 Particionamento

* A definição da **estrutura de particionamento** é livre, podendo ser por UF, data de extração ou tipo de empresa.

---

## 💾 Formato e versionamento dos dados

* Todas as camadas devem ser escritas em **formato Delta Lake**.
* As camadas **RAW e TRUSTED** devem possuir **pelo menos duas versões** de escrita para fins de demonstração de versionamento.
* Utilizar `merge` ou `overwrite` no Delta para reprocessamentos controlados.

---

## 📓 Notebooks a serem construídos

1. **`01_coleta_dados.ipynb`**

   * Responsável por consumir os dados dos endpoints e salvar na camada **Landing**.

2. **`02_preparacao_raw.ipynb`**

   * Transformações iniciais e salvamento estruturado na camada **RAW**.

3. **`03_transformacao_trusted.ipynb`**

   * Realização de joins com dimensões e aplicação de regras de qualidade de dados.

4. **`04_analise_resultados.ipynb`**

   * Exibir estatísticas e visualizações dos dados.
   * Mostrar **versões disponíveis das tabelas Delta** com `DESCRIBE HISTORY`.

---

## ✅ Critérios de entrega

* Todos os notebooks devidamente comentados.
* Dados organizados em pastas por camada (LND, RAW, TRS).
* README.

---
