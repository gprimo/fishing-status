## 📓 FISHING STATUS
O Objetivo do projeto foi trazer milhares de informações de atividade pesqueira pelo mundo. Os dados foram obtidos do sistema Global Fishing. Se quiser acessar diretamente os dados, pode acessar em:
https://globalfishingwatch.org/data-download/datasets/public-training-data-v1 <br>
Caso não queira ter o trabalho eu disponibilizei um drive os csvs que utilizei em:


### 1. `01_stage.ipynb` (Tratamento & Ingestão com PySpark)
* **Objetivo:** Ler múltiplos arquivos CSV de entrada utilizando a API de DataFrame do Spark, padronizando os dados e salvando em formato colunar de alta performance.
* **Principais Etapas:**
  * Leitura e unificação dos CSVs com `spark.read.option("header", "true").csv(...)`.
  * Tratamento de valores nulos, remoção de duplicatas e cast de tipos de dados (`TimestampType`, `DoubleType`, etc.).
  * Filtragem de registros inconsistentes.
  * Exportação para formato **Parquet** (`.parquet`), aproveitando o particionamento e compressão nativos do Spark.

### 2. `02_analytics.ipynb` (SparkSQL, Transformação & Inferências)
* **Objetivo:** Registrar os dados Parquet em views temporárias (`createOrReplaceTempView`), executar consultas complexas via SparkSQL e realizar inferências analíticas.
* **Principais Etapas:**
  * Carga do dataset Parquet pré-tratado na `SparkSession`.
  * Execução de queries **SparkSQL** para criação de tabelas analíticas intermediárias.
  * Modelagem e transformações com window functions, agregações e joins otimizados.
  * Geração de **inferências e análises estatísticas** sobre a atividade pesqueira (ex: volume capturado por espécie, eficiência por embarcação, sazonalidade e análise espacial).

### 3. `03_gold.ipynb` (Base Consolidada & Entrega Final)
* **Objetivo:** Consolidar a camada analítica final em uma base unificada (Gold) pronta para relatórios, dashboards ou consumo por equipes de BI/Data Science.
* **Principais Etapas:**
  * Consolidação final das tabelas/views geradas no SparkSQL.
  * Aplicação das regras de negócio e validações finais de qualidade.
  * Escrita da **Base Consolidada Final** (Gold) em Parquet ou Delta Lake.

---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python
* **Motor de Processamento:** Apache Spark (`pyspark`)
* **Módulo SQL:** SparkSQL (`pyspark.sql`)
* **Armazenamento:** Parquet / Delta Lake
* **Ambiente:** Jupyter Notebooks / PySpark Kernel / Databricks

---

## 🚀 Como Executar o Projeto
Será necessário baixar as bases de dados disponiblizado em:
https://drive.google.com/drive/folders/1jtcFxhjSJqZ8vwpoZGHfeR5cIIMCMNUE?usp=drive_link
<br>
Depois disso será necessário fazer um catálogo  Fishing no ambiente Databricks, deverá ter um schema Raw, e um schema bronze e um schema analytics. No schema raw deve ter um volume fishing com os csv carregados.


