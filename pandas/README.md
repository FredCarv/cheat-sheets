
# Pandas Cheat Sheet

## Leitura e Escrita de Arquivos

### pd.read_excel()

Lê uma planilha Excel.

```python
pd.read_excel(
    arquivo,
    sheet_name=0,
    header=0,
    usecols=None
)
```

Parâmetros:

- `arquivo`: caminho do arquivo
- `sheet_name`: nome ou índice da aba
- `header`: linha que contém o cabeçalho
- `usecols`: colunas a serem importadas

Exemplo:

```python
df = pd.read_excel('arquivo.xlsx', sheet_name='Base')
```

---

### pd.read_csv()

```python
pd.read_csv(
    arquivo,
    sep=',',
    encoding='utf-8'
)
```

Parâmetros:

- `sep`: separador
- `encoding`: codificação

---

### to_csv()

```python
df.to_csv(
    'arquivo.csv',
    index=False,
    encoding='utf-8'
)
```

Parâmetros:

- `index=False`: não exporta o índice
- `encoding`: codificação

---

## Inspeção dos Dados

### head()

Primeiras linhas.

```python
df.head(n=5)
```

Parâmetros:

- `n`: quantidade de linhas

---

### tail()

Últimas linhas.

```python
df.tail(n=5)
```

Parâmetros:

- `n`: quantidade de linhas

---

### shape

Quantidade de linhas e colunas.

```python
df.shape
```

Retorna:

```python
(linhas, colunas)
```

---

### columns

Lista os nomes das colunas.

```python
df.columns
```

---

### dtypes

Mostra os tipos das colunas.

```python
df.dtypes
```

---

### info()

Resumo geral.

```python
df.info()
```

---

### describe()

Estatísticas descritivas.

```python
df.describe()
```

---

## Seleção de Dados

### Selecionar uma coluna

```python
df['coluna']

# ou

df.coluna
```

---

### Selecionar múltiplas colunas

```python
df[['coluna1', 'coluna2']]
```

---

### loc[]

Seleciona por nome.

```python
df.loc[linhas, colunas]
```

Exemplos:

```python
df.loc[0]

df.loc[:, 'nome']

df.loc[:, ['nome', 'idade']]
```

---

### iloc[]

Seleciona por índice.

```python
df.iloc[linhas, colunas]
```

Exemplos:

```python
df.iloc[0]

df.iloc[:, 2]

df.iloc[0:10, 3:7]
```

---

## Filtragem

### Condição simples

```python
df[df['idade'] > 18]
```

---

### Múltiplas condições

AND:

```python
df[(df['idade'] > 18) & (df['cidade'] == 'SP')]
```

OR:

```python
df[(df['idade'] > 18) | (df['cidade'] == 'SP')]
```

NOT:

```python
df[~(df['cidade'] == 'SP')]
```

---

### isin()

Verifica se pertence a uma lista.

```python
df[df['canal'].isin(['Google', 'Meta'])]
```

---

### between()

```python
df[df['valor'].between(100, 500)]
```

---

## Manipulação de Colunas

### rename()

Renomeia colunas.

```python
df.rename(
    columns={'antigo':'novo'},
    inplace=True
)
```

Parâmetros:

- `columns`: dicionário `{antigo: novo}`
- `inplace`: altera o dataframe original

---

### Adicionar coluna

```python
df['nova_coluna'] = valor
```

---

### insert()

Insere uma coluna em uma posição específica.

```python
df.insert(
    loc=2,
    column='nova_coluna',
    value=0
)
```

Parâmetros:

- `loc`: posição da coluna (começa em 0)
- `column`: nome da coluna
- `value`: valor, lista ou série

---

### drop()

Remove colunas ou linhas.

```python
df.drop(
    columns=['coluna1'],
    inplace=True
)
```

Parâmetros:

- `columns`: colunas a remover
- `index`: linhas a remover
- `inplace`: altera o dataframe original

---

### astype()

Altera o tipo da coluna.

```python
df['valor'] = df['valor'].astype(float)
```

Tipos comuns:

```python
str
int
float
bool
datetime64[ns]
```

---

## Limpeza de Dados

### fillna()

Substitui valores nulos.

```python
df.fillna(
    value=0,
    inplace=True
)
```

Parâmetros:

- `value`: valor substituto
- `inplace`: altera o dataframe original

---

### dropna()

Remove nulos.

```python
df.dropna(
    axis=0,
    how='any'
)
```

Parâmetros:

- `axis=0`: linhas
- `axis=1`: colunas
- `how='any'`: remove se houver algum nulo
- `how='all'`: remove se todos forem nulos

---

### replace()

Substitui valores.

```python
df.replace(
    'Tik Tok',
    'TikTok'
)
```

---

### duplicated()

Identifica duplicados.

```python
df.duplicated()
```

---

### drop_duplicates()

Remove duplicados.

```python
df.drop_duplicates(
    subset=['id'],
    keep='first'
)
```

Parâmetros:

- `subset`: colunas consideradas
- `keep`: `'first'`, `'last'` ou `False`

---

## Manipulação de Strings

### str.strip()

Remove espaços.

```python
df['nome'].str.strip()
```

---

### str.lower()

Converte para minúsculas.

```python
df['nome'].str.lower()
```

---

### str.upper()

Converte para maiúsculas.

```python
df['nome'].str.upper()
```

---

### str.contains()

```python
df['canal'].str.contains(
    'google',
    case=False,
    na=False
)
```

Parâmetros:

- `case=False`: ignora maiúsculas/minúsculas
- `na=False`: ignora nulos

---

### str.startswith()

```python
df['nome'].str.startswith(
    ('A', 'B')
)
```

---

### str.endswith()

```python
df['nome'].str.endswith(
    '.csv'
)
```

---

## Datas

### pd.to_datetime()

```python
pd.to_datetime(
    df['data'],
    dayfirst=True,
    errors='coerce'
)
```

Parâmetros:

- `dayfirst=True`: formato brasileiro
- `errors='coerce'`: inválidos viram NaT

---

### Componentes de data

```python
df['data'].dt.day

df['data'].dt.month

df['data'].dt.year

df['data'].dt.weekday
```

---

## Agrupamentos

### groupby()

```python
df.groupby('canal')['investimento'].sum()
```

---

### agg()

Múltiplas agregações.

```python
df.groupby('canal').agg({
    'investimento':'sum',
    'impressions':'mean'
})
```

Funções comuns:

```python
sum
mean
count
min
max
median
std
```

---

## Ordenação

### sort_values()

```python
df.sort_values(
    by='valor',
    ascending=False
)
```

Parâmetros:

- `by`: coluna
- `ascending`: crescente (`True`) ou decrescente (`False`)

---

## Junções

### merge()

Equivalente ao JOIN SQL.

```python
df1.merge(
    df2,
    on='id',
    how='left'
)
```

Parâmetros:

- `on`: coluna comum
- `left_on`: coluna da esquerda
- `right_on`: coluna da direita
- `how`: tipo do join

Tipos:

```text
left
right
inner
outer
```

---

## Contagens Úteis

### unique()

Valores únicos.

```python
df['canal'].unique()
```

---

### nunique()

Quantidade de valores únicos.

```python
df['canal'].nunique()
```

---

### value_counts()

Frequência dos valores.

```python
df['canal'].value_counts()
```

Parâmetros úteis:

```python
normalize=True
dropna=False
ascending=True
```

---

## Iteração

### iterrows()

```python
for indice, linha in df.iterrows():
    print(indice)
    print(linha)
```

---

### itertuples()

Mais rápido que `iterrows()`.

```python
for linha in df.itertuples():
    print(linha.nome)
```

---

### enumerate()

```python
for i, col in enumerate(df.columns):
    print(i, col)
```

Parâmetro:

- `start`: valor inicial

Exemplo:

```python
for i, col in enumerate(df.columns, start=1):
    print(i, col)
```

---

# Operações úteis com colunas

### Remover pelo índice

```python
df.drop(columns=df.columns[[1, 3, 5]])
```

---

### Selecionar pelo índice

```python
df.iloc[:, 27:]
```

---

### Obter nomes das colunas

```python
df.columns[27:]
```

---

### Inserir várias colunas

```python
novas_colunas = ['X', 'Y', 'Z']

for i, col in enumerate(novas_colunas):
    df.insert(28 + i, col, 0)
```

---

# Métodos para decorar (80% do uso diário)

```text
pd.read_excel()
pd.read_csv()

head()
tail()
shape
columns
dtypes
info()
describe()

loc[]
iloc[]

rename()
drop()
insert()
astype()

fillna()
dropna()
replace()

str.strip()
str.lower()
str.upper()
str.contains()

pd.to_datetime()

groupby()
agg()

sort_values()

merge()

value_counts()
unique()
nunique()

iterrows()
itertuples()
enumerate()
```
````
