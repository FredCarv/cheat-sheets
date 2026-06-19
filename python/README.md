# Python Nativo Cheat Sheet

> Foco em estruturas de dados (listas, dicionários, tuplas, conjuntos), iteração, atribuição, manipulação e operações muito utilizadas em ETL, automações e análise de dados.

---

# Listas (list)

## Criar listas

```python
lista = []

lista = [1, 2, 3]

lista = ['Google', 'Meta', 'TikTok']
```

---

## Acessar elementos

```python
lista[0]

lista[1]

lista[-1]   # último elemento

lista[-2]   # penúltimo
```

---

## Fatiamento (slice)

```python
lista[1:4]

lista[:3]

lista[3:]

lista[:-1]

lista[::2]

lista[::-1]
```

---

## Iterar uma lista

```python
for item in lista:
    print(item)
```

---

## Iterar obtendo índice

```python
for i, item in enumerate(lista):
    print(i, item)
```

---

## Alterar valor

```python
lista[0] = 'YouTube'
```

---

## Adicionar elemento ao final

```python
lista.append('LinkedIn')
```

---

## Adicionar vários elementos

```python
lista.extend(['Pinterest', 'Spotify'])
```

---

## Inserir em posição específica

```python
lista.insert(2, 'Netflix')
```

---

## Remover por valor

```python
lista.remove('Meta')
```

---

## Remover por índice

```python
lista.pop(2)

lista.pop()   # último elemento
```

---

## Remover tudo

```python
lista.clear()
```

---

## Ordenar

```python
lista.sort()

lista.sort(reverse=True)
```

---

## Ordenar sem alterar a lista original

```python
nova_lista = sorted(lista)

nova_lista = sorted(lista, reverse=True)
```

---

## Inverter

```python
lista.reverse()
```

---

## Contar ocorrências

```python
lista.count('Google')
```

---

## Obter posição

```python
lista.index('Google')
```

---

## Verificar existência

```python
'Google' in lista

'Meta' not in lista
```

---

## Obter tamanho

```python
len(lista)
```

---

## Juntar listas

```python
lista3 = lista1 + lista2
```

---

## Repetir listas

```python
lista = [0] * 10
```

---

# Compreensão de listas (list comprehension)

## Criar lista

```python
quadrados = [x**2 for x in range(5)]
```

Resultado:

```python
[0, 1, 4, 9, 16]
```

---

## Com condição

```python
pares = [x for x in range(10) if x % 2 == 0]
```

---

# Tuplas (tuple)

## Criar

```python
tupla = (1, 2, 3)
```

---

## Acessar

```python
tupla[0]
```

---

## Desempacotar

```python
nome, idade = ('Frederico', 30)

print(nome)

print(idade)
```

---

# Conjuntos (set)

## Criar

```python
conjunto = {1, 2, 3}

conjunto = set(lista)
```

---

## Adicionar

```python
conjunto.add(4)
```

---

## Remover

```python
conjunto.remove(2)

conjunto.discard(2)
```

Diferença:

```python
remove() -> gera erro

discard() -> não gera erro
```

---

## Operações matemáticas

```python
a | b   # união

a & b   # interseção

a - b   # diferença

a ^ b   # diferença simétrica
```

---

# Dicionários (dict)

## Criar

```python
dicionario = {}

dicionario = {

    'canal': 'Google',

    'investimento': 1000

}
```

---

## Acessar sabendo a chave

```python
dicionario['canal']
```

ou

```python
dicionario.get('canal')
```

Diferença:

```python
dict['x'] -> gera erro

dict.get('x') -> retorna None
```

---

# Atribuir valor de uma chave a uma variável

## Sabendo a chave

```python
canal = dicionario['canal']

valor = dicionario.get('investimento')
```

---

## Não sabendo a chave

### Primeira chave

```python
primeira_chave = next(iter(dicionario))

valor = dicionario[primeira_chave]
```

---

## Iterando até encontrar

```python
for chave, valor in dicionario.items():

    if alguma_condicao:

        minha_variavel = valor
```

---

# Atribuir valores do dicionário a variáveis

## Sabendo as chaves

```python
canal = dicionario['canal']

investimento = dicionario['investimento']
```

---

## Desempacotar

```python
canal, investimento = (

    dicionario['canal'],

    dicionario['investimento']

)
```

---

## Sem saber as chaves

```python
valores = list(dicionario.values())

print(valores)
```

---

## Obter o primeiro valor

```python
primeiro_valor = next(iter(dicionario.values()))
```

---

# Manipular dicionários

## Adicionar

```python
dicionario['pais'] = 'Brasil'
```

---

## Atualizar

```python
dicionario['canal'] = 'Meta'
```

---

## Atualizar várias chaves

```python
dicionario.update({

    'canal': 'TikTok',

    'valor': 500

})
```

---

## Remover

```python
del dicionario['canal']
```

---

## Remover retornando o valor

```python
valor = dicionario.pop('canal')
```

---

## Limpar

```python
dicionario.clear()
```

---

## Copiar

```python
novo = dicionario.copy()
```

---

# Iterar dicionários

## Iterar chaves

```python
for chave in dicionario:

    print(chave)
```

ou

```python
for chave in dicionario.keys():

    print(chave)
```

---

## Iterar valores

```python
for valor in dicionario.values():

    print(valor)
```

---

## Iterar chave e valor

```python
for chave, valor in dicionario.items():

    print(chave, valor)
```

---

## Obter listas

```python
dicionario.keys()

dicionario.values()

dicionario.items()
```

Converter:

```python
list(dicionario.keys())

list(dicionario.values())

list(dicionario.items())
```

---

# Loops

## range()

```python
range(5)

range(1, 5)

range(0, 10, 2)
```

---

## Iterar números

```python
for i in range(5):

    print(i)
```

---

## enumerate()

```python
for i, valor in enumerate(lista):

    print(i, valor)
```

---

## Definir início

```python
for i, valor in enumerate(

    lista,

    start=1

):

    print(i, valor)
```

---

## zip()

Percorre várias estruturas simultaneamente.

```python
nomes = ['Google', 'Meta']

valores = [100, 200]

for nome, valor in zip(

    nomes,

    valores

):

    print(nome, valor)
```

---

# Condicionais

## if

```python
if condicao:

    ...
```

---

## if else

```python
if condicao:

    ...

else:

    ...
```

---

## if elif else

```python
if condicao:

    ...

elif outra:

    ...

else:

    ...
```

---

## Operador ternário

```python
resultado = 'OK' if condicao else 'ERRO'
```

---

# Strings

## Converter

```python
str(valor)

int(valor)

float(valor)

bool(valor)
```

---

## Manipulação

```python
texto.lower()

texto.upper()

texto.title()

texto.strip()

texto.replace()

texto.split()

texto.join()

texto.startswith()

texto.endswith()

texto.find()

texto.count()
```

---

## f-string

```python
nome = 'Google'

print(

    f'Canal: {nome}'

)
```

---

# Funções úteis

## len()

```python
len(objeto)
```

---

## type()

```python
type(objeto)
```

---

## isinstance()

```python
isinstance(

    objeto,

    list

)
```

---

## sorted()

```python
sorted(lista)

sorted(lista, reverse=True)
```

---

## sum()

```python
sum(lista)
```

---

## min()

```python
min(lista)
```

---

## max()

```python
max(lista)
```

---

## any()

Retorna True se pelo menos um for verdadeiro.

```python
any(

    x > 10

    for x in lista

)
```

---

## all()

Retorna True se todos forem verdadeiros.

```python
all(

    x > 10

    for x in lista

)
```

---

# Expressões muito úteis em ETL

## Verificar se existe

```python
if coluna in lista:
```

---

## Verificar se não existe

```python
if coluna not in lista:
```

---

## Verificar se algum item existe

```python
if any(

    col in lista

    for col in novas_colunas

):
```

---

## Verificar se todos existem

```python
if all(

    col in lista

    for col in novas_colunas

):
```

---

## Criar dicionário a partir de duas listas

```python
dicionario = dict(

    zip(

        chaves,

        valores

    )

)
```

---

## Inverter chave e valor

```python
invertido = {

    valor: chave

    for chave, valor

    in dicionario.items()

}
```

---

## Ordenar um dicionário

```python
ordenado = dict(

    sorted(

        dicionario.items()

    )

)
```

---

# Métodos para decorar (80% do uso diário)

```text
len()

type()

isinstance()

range()

enumerate()

zip()

sorted()

sum()

min()

max()

any()

all()

next()

iter()

list()

dict()

set()

tuple()

str()

int()

float()

bool()
```

# Métodos de lista para decorar

```text
append()

extend()

insert()

remove()

pop()

clear()

sort()

reverse()

count()

index()
```

# Métodos de dicionário para decorar

```text
get()

keys()

values()

items()

update()

pop()

clear()

copy()
```
