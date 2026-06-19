# Google Cloud BigQuery (Python) Cheat Sheet

> Biblioteca principal:
>
> ```python
> from google.cloud import bigquery
> ```
>
> Documentação:
>
> https://cloud.google.com/python/docs/reference/bigquery/latest

---

# Inicialização

## Criar cliente

```python
from google.cloud import bigquery

client = bigquery.Client()
```

Parâmetros úteis:

- `project`: ID do projeto (opcional)
- `credentials`: credenciais customizadas (opcional)

Exemplo:

```python
client = bigquery.Client(
    project='meu-projeto'
)
```

---

# Referências de objetos

## Referenciar um dataset

```python
dataset_id = 'meu-projeto.meu_dataset'
```

---

## Referenciar uma tabela

```python
table_id = 'meu-projeto.meu_dataset.minha_tabela'
```

Formato:

```text
projeto.dataset.tabela
```

---

# Executar queries

## query()

Executa SQL.

```python
query_job = client.query(
    query
)
```

Exemplo:

```python
query = """
SELECT *
FROM meu_dataset.minha_tabela
"""

query_job = client.query(query)
```

---

## result()

Espera a execução terminar.

```python
resultado = query_job.result()
```

---

## Iterar resultados

```python
for linha in resultado:
    print(linha)
```

---

## Converter para DataFrame

```python
df = query_job.to_dataframe()
```

ou

```python
df = query_job.result().to_dataframe()
```

---

# QueryJobConfig

Configura parâmetros da query.

```python
job_config = bigquery.QueryJobConfig()
```

---

## destination

Define tabela de destino.

```python
job_config.destination = table_id
```

---

## write_disposition

Controla a escrita.

```python
job_config.write_disposition = (
    bigquery.WriteDisposition.WRITE_APPEND
)
```

Opções:

```text
WRITE_APPEND
WRITE_TRUNCATE
WRITE_EMPTY
```

Significados:

- `WRITE_APPEND`: adiciona linhas
- `WRITE_TRUNCATE`: substitui a tabela
- `WRITE_EMPTY`: falha se a tabela existir

---

## use_legacy_sql

Usa SQL padrão.

```python
job_config.use_legacy_sql = False
```

Sempre prefira:

```python
False
```

---

## Executar query com configuração

```python
query_job = client.query(
    query,
    job_config=job_config
)
```

---

# Carregar DataFrames

## load_table_from_dataframe()

Carrega um DataFrame para o BigQuery.

```python
job = client.load_table_from_dataframe(
    dataframe,
    table_id
)
```

---

## Configurar o carregamento

```python
job_config = bigquery.LoadJobConfig()
```

---

## schema

Define o schema.

```python
job_config.schema = [
    bigquery.SchemaField(
        'canal',
        'STRING'
    ),

    bigquery.SchemaField(
        'investimento',
        'FLOAT64'
    )
]
```

Tipos comuns:

```text
STRING
INTEGER
FLOAT64
BOOLEAN
DATE
DATETIME
TIMESTAMP
NUMERIC
BIGNUMERIC
JSON
ARRAY
```

---

## write_disposition

```python
job_config.write_disposition = (
    bigquery.WriteDisposition.WRITE_APPEND
)
```

Opções:

```text
WRITE_APPEND
WRITE_TRUNCATE
WRITE_EMPTY
```

---

## autodetect

Detecta tipos automaticamente.

```python
job_config.autodetect = True
```

---

## Executar carga

```python
job = client.load_table_from_dataframe(
    dataframe,
    table_id,
    job_config=job_config
)

job.result()
```

---

# Carregar CSV

## load_table_from_file()

```python
with open(
    'arquivo.csv',
    'rb'
) as f:

    job = client.load_table_from_file(
        f,
        table_id
    )

job.result()
```

---

# Carregar JSON

## load_table_from_json()

```python
job = client.load_table_from_json(
    dados,
    table_id
)

job.result()
```

Onde:

```python
dados = [
    {
        'canal':'Google',
        'valor':1000
    }
]
```

---

# Criar tabelas

## Table()

```python
tabela = bigquery.Table(
    table_id
)
```

---

## create_table()

```python
client.create_table(
    tabela
)
```

---

## Criar tabela com schema

```python
schema = [

    bigquery.SchemaField(
        'canal',
        'STRING'
    ),

    bigquery.SchemaField(
        'valor',
        'FLOAT64'
    )

]

tabela = bigquery.Table(
    table_id,
    schema=schema
)

client.create_table(
    tabela
)
```

---

# Obter tabelas

## get_table()

```python
tabela = client.get_table(
    table_id
)
```

Informações úteis:

```python
tabela.num_rows

tabela.schema

tabela.created

tabela.modified
```

---

# Listar datasets

## list_datasets()

```python
datasets = client.list_datasets()

for dataset in datasets:
    print(dataset.dataset_id)
```

---

# Listar tabelas

## list_tables()

```python
tabelas = client.list_tables(
    dataset_id
)

for tabela in tabelas:
    print(tabela.table_id)
```

---

# Excluir tabelas

## delete_table()

```python
client.delete_table(
    table_id,
    not_found_ok=True
)
```

Parâmetros:

- `not_found_ok=True`: ignora erro se a tabela não existir

---

# Criar datasets

## Dataset()

```python
dataset = bigquery.Dataset(
    dataset_id
)
```

---

## create_dataset()

```python
client.create_dataset(
    dataset
)
```

---

# Excluir datasets

## delete_dataset()

```python
client.delete_dataset(
    dataset_id,
    delete_contents=True
)
```

Parâmetros:

- `delete_contents=True`: remove tabelas internas

---

# Inserir linhas

## insert_rows_json()

```python
erros = client.insert_rows_json(
    table_id,
    dados
)
```

Exemplo:

```python
dados = [

    {
        'canal':'Google',
        'valor':1000
    }

]

client.insert_rows_json(
    table_id,
    dados
)
```

---

# Parâmetros SQL

## ScalarQueryParameter

```python
job_config = bigquery.QueryJobConfig(
    query_parameters=[

        bigquery.ScalarQueryParameter(
            'data_inicio',
            'DATE',
            '2026-01-01'
        )

    ]
)
```

SQL:

```sql
SELECT *
FROM tabela
WHERE data >= @data_inicio
```

---

# Extrair dados

## extract_table()

Exporta para o GCS.

```python
extract_job = client.extract_table(
    table_id,
    destination_uri
)

extract_job.result()
```

Exemplo:

```python
destination_uri = (
    'gs://bucket/arquivo.csv'
)
```

---

# Informações úteis dos jobs

## job_id

```python
job.job_id
```

---

## state

```python
job.state
```

---

## errors

```python
job.errors
```

---

## output_rows

```python
job.output_rows
```

---

# Tratamento de erros

```python
try:

    job.result()

except Exception as e:

    print(e)
```

---

# Fluxo ETL mais comum

## Excel -> Pandas -> BigQuery

```python
import pandas as pd

from google.cloud import bigquery

client = bigquery.Client()

df = pd.read_excel(
    'arquivo.xlsx'
)

job_config = bigquery.LoadJobConfig(

    schema=[

        bigquery.SchemaField(
            'canal',
            'STRING'
        ),

        bigquery.SchemaField(
            'valor',
            'FLOAT64'
        )

    ],

    write_disposition='WRITE_APPEND'

)

job = client.load_table_from_dataframe(

    df,

    'projeto.dataset.tabela',

    job_config=job_config

)

job.result()
```

---

# Métodos para decorar (80% do uso diário)

```text
bigquery.Client()

client.query()

client.load_table_from_dataframe()

client.load_table_from_file()

client.load_table_from_json()

client.get_table()

client.list_tables()

client.list_datasets()

client.create_table()

client.delete_table()

client.create_dataset()

client.delete_dataset()

client.insert_rows_json()

bigquery.QueryJobConfig()

bigquery.LoadJobConfig()

bigquery.SchemaField()

bigquery.Table()

job.result()

query_job.to_dataframe()
```

---

# Objetos que você provavelmente usará no dia a dia

```text
Client
QueryJobConfig
LoadJobConfig
SchemaField
Table
Dataset
WriteDisposition
```

# Valores de WriteDisposition

```text
WRITE_APPEND    -> adiciona linhas
WRITE_TRUNCATE  -> substitui a tabela
WRITE_EMPTY     -> falha se a tabela já existir
```

# Tipos de dados do BigQuery

```text
STRING
INTEGER
FLOAT64
BOOLEAN

DATE
DATETIME
TIMESTAMP

NUMERIC
BIGNUMERIC

JSON

ARRAY
```
