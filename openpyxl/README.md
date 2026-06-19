# OpenPyXL Cheat Sheet

## Importação

```python
from openpyxl import load_workbook
from openpyxl import Workbook
```

---

# Criar e abrir arquivos

## Workbook()

Cria um novo arquivo Excel.

```python
wb = Workbook()
```

---

## load_workbook()

Abre um arquivo existente.

```python
wb = load_workbook(
    filename='arquivo.xlsx',
    data_only=False
)
```

Parâmetros:

- `filename`: caminho do arquivo
- `data_only=True`: retorna o valor calculado das fórmulas
- `data_only=False`: retorna a fórmula em si

---

## save()

Salva o arquivo.

```python
wb.save('arquivo.xlsx')
```

---

## close()

Fecha o arquivo.

```python
wb.close()
```

---

# Manipulação de abas

## workbook.sheetnames

Lista as abas.

```python
wb.sheetnames
```

Retorno:

```python
['Base', 'Resumo', 'Dashboard']
```

---

## workbook.active

Obtém a aba ativa.

```python
ws = wb.active
```

---

## workbook['nome']

Seleciona uma aba.

```python
ws = wb['Base']
```

---

## create_sheet()

Cria uma aba.

```python
wb.create_sheet(
    title='Nova_Aba',
    index=0
)
```

Parâmetros:

- `title`: nome da aba
- `index`: posição da aba

---

## remove()

Remove uma aba.

```python
wb.remove(ws)
```

ou

```python
del wb['Base']
```

---

# Informações da planilha

## max_row

Última linha utilizada.

```python
ws.max_row
```

---

## max_column

Última coluna utilizada.

```python
ws.max_column
```

---

## dimensions

Intervalo utilizado.

```python
ws.dimensions
```

Retorno:

```text
A1:AZ100
```

---

# Leitura de células

## Acessar uma célula

```python
ws['A1']
```

ou

```python
ws.cell(
    row=1,
    column=1
)
```

Parâmetros:

- `row`: linha (começa em 1)
- `column`: coluna (começa em 1)

---

## Obter valor

```python
ws['A1'].value
```

ou

```python
ws.cell(1,1).value
```

---

# Escrever em células

## Atribuição direta

```python
ws['A1'] = 'Texto'
```

---

## cell()

```python
ws.cell(
    row=1,
    column=1,
    value='Texto'
)
```

---

# Iterar linhas

## iter_rows()

```python
for linha in ws.iter_rows():
    print(linha)
```

Parâmetros:

```python
iter_rows(
    min_row=None,
    max_row=None,
    min_col=None,
    max_col=None,
    values_only=False
)
```

Parâmetros:

- `min_row`: primeira linha
- `max_row`: última linha
- `min_col`: primeira coluna
- `max_col`: última coluna
- `values_only=True`: retorna apenas os valores

Exemplo:

```python
for linha in ws.iter_rows(
    min_row=2,
    values_only=True
):
    print(linha)
```

---

# Iterar colunas

## iter_cols()

```python
for coluna in ws.iter_cols():
    print(coluna)
```

Parâmetros:

```python
iter_cols(
    min_row=None,
    max_row=None,
    min_col=None,
    max_col=None,
    values_only=False
)
```

---

# Adicionar linhas

## append()

Adiciona uma nova linha ao final.

```python
ws.append([
    'Google',
    'Meta',
    1000
])
```

Também funciona com dicionários.

---

# Inserir linhas

## insert_rows()

```python
ws.insert_rows(
    idx=5,
    amount=1
)
```

Parâmetros:

- `idx`: linha onde inserir
- `amount`: quantidade

Exemplo:

```python
ws.insert_rows(5, 3)
```

Insere 3 linhas antes da linha 5.

---

# Inserir colunas

## insert_cols()

```python
ws.insert_cols(
    idx=3,
    amount=1
)
```

Parâmetros:

- `idx`: coluna onde inserir
- `amount`: quantidade

Exemplo:

```python
ws.insert_cols(3,2)
```

Insere 2 colunas antes da coluna C.

---

# Remover linhas

## delete_rows()

```python
ws.delete_rows(
    idx=5,
    amount=1
)
```

Parâmetros:

- `idx`: linha inicial
- `amount`: quantidade

---

# Remover colunas

## delete_cols()

```python
ws.delete_cols(
    idx=3,
    amount=1
)
```

Parâmetros:

- `idx`: coluna inicial
- `amount`: quantidade

---

# Mesclar células

## merge_cells()

```python
ws.merge_cells(
    'A1:D1'
)
```

ou

```python
ws.merge_cells(
    start_row=1,
    start_column=1,
    end_row=1,
    end_column=4
)
```

---

# Desmesclar células

## unmerge_cells()

```python
ws.unmerge_cells(
    'A1:D1'
)
```

---

# Mover células

## move_range()

```python
ws.move_range(
    'A1:C10',
    rows=2,
    cols=1
)
```

Parâmetros:

- `rows`: deslocamento vertical
- `cols`: deslocamento horizontal

---

# Copiar linhas entre abas

```python
for linha in ws_origem.iter_rows(
    min_row=2,
    values_only=True
):
    ws_destino.append(linha)
```

---

# Congelar painéis

## freeze_panes

```python
ws.freeze_panes = 'A2'
```

Congela a primeira linha.

```python
ws.freeze_panes = 'B2'
```

Congela a primeira linha e a primeira coluna.

---

# Ajustar largura de colunas

```python
ws.column_dimensions['A'].width = 20
```

---

# Ajustar altura de linhas

```python
ws.row_dimensions[1].height = 30
```

---

# Obter letra da coluna

```python
from openpyxl.utils import get_column_letter

get_column_letter(27)
```

Retorno:

```text
AA
```

---

# Obter número da coluna

```python
from openpyxl.utils import column_index_from_string

column_index_from_string('AA')
```

Retorno:

```text
27
```

---

# Estilos

## Font

```python
from openpyxl.styles import Font

ws['A1'].font = Font(
    bold=True,
    italic=True,
    size=12
)
```

Parâmetros úteis:

- `bold`
- `italic`
- `size`
- `name`
- `color`

---

## PatternFill

```python
from openpyxl.styles import PatternFill

ws['A1'].fill = PatternFill(
    fill_type='solid',
    fgColor='FFFF00'
)
```

---

## Alignment

```python
from openpyxl.styles import Alignment

ws['A1'].alignment = Alignment(
    horizontal='center',
    vertical='center'
)
```

Parâmetros úteis:

- `horizontal`
- `vertical`
- `wrap_text`

---

## Border

```python
from openpyxl.styles import Border, Side

borda = Side(style='thin')

ws['A1'].border = Border(
    left=borda,
    right=borda,
    top=borda,
    bottom=borda
)
```

---

# Fórmulas

```python
ws['A1'] = '=SUM(B1:B10)'
```

---

# Operações úteis

## Enumerar linhas

```python
for i, linha in enumerate(
    ws.iter_rows(
        min_row=2,
        values_only=True
    ),
    start=2
):
    print(i, linha)
```

---

## Copiar uma aba inteira

```python
nova_aba = wb.copy_worksheet(ws)
```

---

## Renomear aba

```python
ws.title = 'Nova_Aba'
```

---

# Métodos para decorar (80% do uso diário)

```text
load_workbook()
Workbook()

save()
close()

sheetnames
active

create_sheet()
remove()

max_row
max_column

cell()

iter_rows()
iter_cols()

append()

insert_rows()
insert_cols()

delete_rows()
delete_cols()

merge_cells()
unmerge_cells()

move_range()

freeze_panes

column_dimensions
row_dimensions

get_column_letter()
column_index_from_string()

Font()
PatternFill()
Alignment()
Border()
```
