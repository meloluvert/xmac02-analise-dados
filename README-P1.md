# 📘 Guia de Consulta Rápida — Métodos Matemáticos para Análise de Dados

Resumo-ensino prático e direto para prova. Cada seção explica **o que é**, **para que serve** e **como usar**, com a sintaxe essencial.

---

## 📑 Índice por Aula

| Aula | Conteúdo |
|------|----------|
| **Aula 1** | [Introdução e Importações](#aula-1-introdução-e-importações) |
| **Aula 2** | [Listas em Python](#aula-2-listas-em-python) |
| **Aula 3** | [Média, Desvio Padrão e Boxplot](#aula-3-média-desvio-padrão-e-boxplot) |
| **Aula 4** | [Arrays, Matrizes e Operações (NumPy)](#aula-4-arrays-matrizes-e-operações-numpy) |
| **Aula 5** | [Probabilidade — Conceitos Básicos](#aula-5-probabilidade--conceitos-básicos) |
| **Aula 6** | [Distribuição Binomial](#aula-6-distribuição-binomial) |
| **Aula 7** | [Distribuição de Poisson](#aula-7-distribuição-de-poisson) |
| **Aula 8** | [Series e DataFrames (Pandas)](#aula-8-series-e-dataframes-pandas) |
| **Aula 9** | [Gráfico de Pizza, Barras e Área](#aula-9-gráfico-de-pizza-barras-e-área) |
| **Aula 10** | [Linhas, Histogramas e Barras (Seaborn)](#aula-10-linhas-histogramas-e-barras-seaborn) |
| **Aula 11** | [Crosstab e Groupby Avançado](#aula-11-crosstab-e-groupby-avançado) |
| **Aula 12** | [Distribuição Normal](#aula-12-distribuição-normal) |
| **Aula 13** | [Distribuição Exponencial](#aula-13-distribuição-exponencial) |
| — | [Pegadinhas de Prova](#pegadinhas-e-erros-mais-comuns) |

---

## Aula 1: Introdução e Importações

Sempre comece o código com as importações padrão. Elas trazem as ferramentas que usaremos em todas as aulas.

```python
import numpy as np                  # Arrays e operações matemáticas
import pandas as pd                 # Tabelas (DataFrames) e Series
import matplotlib.pyplot as plt     # Gráficos básicos
import seaborn as sns               # Gráficos estatísticos
import statistics as st             # Média, mediana, quantis etc.
from scipy.stats import binom, poisson, norm, expon  # Distribuições
```

**Por que importar assim?**  
`scipy.stats` concentra várias distribuições. Depois de importar, você chama a função pelo nome da distribuição:

```python
binom.pmf(...)   # Binomial
poisson.cdf(...) # Poisson
norm.pdf(...)    # Normal
expon.sf(...)    # Exponencial
```
Também é possível gerar amostras com o numpy:

```python
mil_lancamentos = np.random.binomial(2,0.5,1000)
fila = np.random.poisson(3.6,1000)

```

Todas seguem o mesmo padrão de nomes de métodos (`pmf`/`pdf`, `cdf`, `sf` etc.).

---

## Aula 2: Listas em Python

Lista é a estrutura mais básica de dados em Python: uma sequência ordenada e mutável de elementos.

```python
# Criação
numeros = [10, 15, 12, 14, 15, 18, 20]
nomes   = ["Ana", "Bruno", "Carlos"]

# Acesso por índice (começa em 0)
numeros[0]      # 10 (primeiro)
numeros[-1]     # 20 (último)
numeros[1:4]    # [15, 12, 14] (do índice 1 até o 3)

# Operações úteis
len(numeros)            # Quantidade de elementos
numeros.append(25)      # Adiciona no final
numeros.remove(15)      # Remove a primeira ocorrência do valor
sum(numeros)            # Soma
sorted(numeros)         # Nova lista ordenada (não altera a original)
```

**Quando usar lista?**  
Para dados pequenos ou quando você ainda não precisa das vantagens de NumPy (velocidade e operações vetorizadas). Em análise de dados, listas viram arrays ou Series rapidamente.

---

## Aula 3: Média, Desvio Padrão e Boxplot

### Estatística Descritiva Básica

```python
dados = [10, 15, 12, 14, 15, 18, 20]

media      = st.mean(dados)       # Média aritmética
mediana    = st.median(dados)     # Valor central (Q2)
moda       = st.mode(dados)       # Valor mais frequente
variancia  = st.variance(dados)   # Variância amostral
desvio     = st.stdev(dados)      # Desvio padrão amostral

# Quartis — retorna lista [Q1, Q2, Q3]
quartis = st.quantiles(dados)
q1, q2, q3 = quartis[0], quartis[1], quartis[2]
iqr = q3 - q1                     # Intervalo Interquartil
```

**Com Pandas (mais comum em DataFrames):**

```python
df['coluna'].mean()
df['coluna'].median()
df['coluna'].std()
df['coluna'].quantile(0.25)   # Q1
df['coluna'].quantile(0.75)   # Q3
df['coluna'].describe()       # Resumo completo
```

### Boxplot — Anatomia e Uso

O boxplot resume a distribuição com cinco números e destaca outliers.

```
       Outlier (*)
          |
    +-----+-----+       ← Limite superior (Q3 + 1,5·IQR)
    |     |     |
    +-----+-----+       ← Q3 (75%)
    |           |
    |-----------|       ← Mediana (Q2)
    |           |
    +-----+-----+       ← Q1 (25%)
    |     |     |
    +-----+-----+       ← Limite inferior (Q1 − 1,5·IQR)
          |
       Outlier (*)
```

- **IQR** = Q3 − Q1 → altura da caixa (50 % centrais dos dados).
- **Outliers** = valores fora de [Q1 − 1,5·IQR ; Q3 + 1,5·IQR].

**Sintaxe mais cobrada em prova (Pandas):**

```python
# Boxplot simples
df.boxplot(column='total_bill')

# Agrupado por categoria (column = numérico, by = categórico)
df.boxplot(column='tip', by='day')
plt.suptitle('')          # Remove o subtítulo automático feio do Pandas

# Padrão de prova: filtrar ANTES
generos = ['Animation', 'Comedy', 'Drama']
df[df['genre'].isin(generos)].boxplot(column='score', by='genre')
plt.suptitle('')
```

**Com Seaborn (mais flexível):**

```python
sns.boxplot(data=df, x='day', y='total_bill', hue='sex')
```

---

## Aula 4: Arrays, Matrizes e Operações (NumPy)

Arrays NumPy são **homogêneos** (mesmo tipo) e permitem operações vetorizadas (muito mais rápidas que listas).

```python
# Criação
arr  = np.array([1, 2, 3, 4, 5])
mat  = np.arange(1, 10).reshape(3, 3)   # Matriz 3×3 de 1 a 9
zeros = np.zeros((3, 3))
ones  = np.ones((2, 4))
espacado = np.linspace(0, 100, 5)       # 5 pontos igualmente espaçados

# Indexação
arr[0]        # primeiro
arr[-1]       # último
arr[1:4]      # do 1 ao 3
mat[0, :]     # primeira linha
mat[:, 1]     # segunda coluna

# Operações
arr.mean()
arr.std()
arr.sum()
arr.max()
arr.min()
```

**Diferença lista × array:**  
Lista é genérica; array é otimizado para cálculo numérico e permite operações elemento a elemento sem laços.

---

## Aula 5: Probabilidade — Conceitos Básicos

**Probabilidade** mede a chance de um evento ocorrer (valor entre 0 e 1).

- **Evento discreto**: contagem (número de sucessos, número de chamadas).
- **Evento contínuo**: medida (altura, tempo, temperatura).

**Distribuições discretas** → usam **pmf** (Probability Mass Function) = probabilidade de um valor **exato**.  
**Distribuições contínuas** → usam **pdf** (Probability Density Function) = densidade; a probabilidade de um intervalo é a **área** sob a curva.

Funções comuns (válidas para quase todas as distribuições do `scipy.stats`):

| Função | Significado |
|--------|-------------|
| `.pmf(k, ...)` ou `.pdf(x, ...)` | Probabilidade/densidade no ponto |
| `.cdf(k, ...)` | P(X ≤ k) — acumulada até k |
| `.sf(k, ...)`  | P(X > k) — sobrevivência (= 1 − cdf) |
| `.mean(...)`   | Média teórica da distribuição |
| `.var(...)`    | Variância teórica |
| `.std(...)`    | Desvio padrão teórico |

---

## Aula 6: Distribuição Binomial

**O que é:**  
Modelo para o número de **sucessos** em **n** tentativas independentes, cada uma com probabilidade **p** de sucesso.

**Quando usar:**  
- Lançamentos de moeda  
- Aprovação/reprovação de alunos  
- Defeitos em peças (sucesso = defeito)  

**Parâmetros:** `n` (tentativas), `p` (probabilidade de sucesso).

```python
from scipy.stats import binom

n, p = 10, 0.5

binom.pmf(3, n, p)      # P(X = 3)  — exatamente 3 sucessos
binom.cdf(3, n, p)      # P(X ≤ 3)  — no máximo 3
binom.sf(3, n, p)       # P(X > 3)  — mais de 3
binom.mean(n, p)        # média = n·p
binom.var(n, p)         # variância = n·p·(1−p)
binom.std(n, p)         # desvio padrão
```

---

## Aula 7: Distribuição de Poisson

**O que é:**  
Modelo para o **número de eventos** que ocorrem em um intervalo fixo de tempo (ou espaço), quando os eventos acontecem de forma independente e com taxa média constante **μ** (ou λ).

**Quando usar:**  
- Número de chamadas por hora  
- Acidentes por dia  
- Erros de digitação por página  

**Parâmetro:** `mu` = taxa média de ocorrências no intervalo.

```python
from scipy.stats import poisson

mu = 4

poisson.pmf(2, mu)      # P(X = 2)  — exatamente 2 eventos
poisson.cdf(2, mu)      # P(X ≤ 2)  — até 2 eventos
poisson.sf(2, mu)       # P(X > 2)  — mais de 2
poisson.mean(mu)        # média = μ
poisson.var(mu)         # variância = μ (igual à média!)
poisson.std(mu)
```

**Relação com a Exponencial:**  
Se o número de eventos segue Poisson, o **tempo entre eventos** segue Exponencial.

---

## Aula 8: Series e DataFrames (Pandas)

### Criação

```python
# Series (1 dimensão rotulada)
s = pd.Series([40, 55, 30, 70, 65], index=["Seg", "Ter", "Qua", "Qui", "Sex"])
s["Ter"]   # 55

# DataFrame (tabela)
df = pd.DataFrame({
    "Nome": ["Ana", "Bruno", "Carlos"],
    "Idade": [23, 35, 29],
    "Salario": [4500, 7200, 5100]
})
```

### Leitura e Inspeção

```python
df = pd.read_csv("arquivo.csv", encoding="latin-1")  # encoding comum em PT

df.shape                  # Mostra o número de linhas e colunas
df.head()                 # Mostra as 5 primeiras linhas
df.info()                 # Mostra informações gerais sobre o DataFrame
df.describe()             # Mostra estatísticas descritivas das colunas numéricas
df.columns                # Mostra os nomes das colunas
df.dtypes                 # Mostra o tipo de dado de cada coluna
df["Coluna"].unique()     # Mostra os valores únicos da coluna
df["Coluna"].value_counts() # Conta quantas vezes cada valor aparece
df.isnull().sum()         # Conta os valores ausentes (NaN) em cada coluna
df.rename(columns={'Close': 'Close TSLA'}, inplace=True)

```

### Seleção: `loc` × `iloc`

| Método | Busca por | Exemplo |
|--------|-----------|---------|
| `df["Coluna"]` | nome da coluna | retorna Series |
| `df[["A","B"]]` | lista de colunas | retorna DataFrame |
| `.loc[linhas, colunas]` | **rótulos** (nomes) | `df.loc[0:2, ["Idade","Salario"]]` |
| `.iloc[linhas, colunas]` | **posição inteira** | `df.iloc[0:3, 1:3]` |


```python
# pega linhas 1 e 5 pelo índice númérico, com todas as colunas
print(df.iloc[[0,4]])


#pega linhas 1 e 5 só com as duas primeiras colunas
print(df.iloc[[0,4], [0,1]])


# a mesma coisa do que em cima, só que com os índices como strings
df.loc[['Item-1', 'Item-5'],['Comprimento', 'Largura']]

```

### Filtros Booleanos (muito cobrado)

**Regras de ouro:**
1. Use `&` (E), `|` (OU), `~` (NÃO) — nunca `and`/`or`.
2. Cada condição **entre parênteses**.

```python
# Filtro simples
df[df["Idade"] >= 18]
# Filtro + coluna específica
dataset_titanic[dataset_titanic['sex'] =='female']['age'].median()
df[['Comprimento', 'Largura']].head() #duas colunas, mas sem loc

# E / OU
df[(df["Operador"] == "Op-1") & (df["Comprimento"] > 105)]
df[(df["Comprimento"] >= 110) | (df["Largura"] >= 53)]

# Pertence / não pertence a lista
df[df["Regiao"].isin(["Europa", "Africa"])]
df[~df["Regiao"].isin(["Asia"])]
```

### Manipulação

```python
df["Volume"] = df["Comp"] * df["Larg"] * df["Alt"]   # nova coluna
df = df.drop("Volume", axis=1)                       # remove coluna
df = df.drop(0, axis=0)                              # remove linha
df.sort_values(by="Salario", ascending=False)
filtro = df['LanguageHaveWorkedWith'].str.contains('palavra aqui'), na=False) 
```

---

## Aula 9: Gráfico de Pizza, Barras e Área

### Pizza (`plt.pie`)

Ideal para **proporções** de um todo.

```python
labels = ["Confirmados", "Prováveis", "Suspeitos"]
sizes  = [3351, 453, 200]

plt.pie(sizes, labels=labels, autopct="%1.1f%%", startangle=90)
plt.axis("equal")
plt.show()
```

### Barras — várias formas de fazer o mesmo gráfico

```python
# 1) Matplotlib / Pandas
df.plot(kind="bar", x="Categoria", y="Valores")

# 2) Barras horizontais
df.plot(kind="barh", x="Pais", y="PIB")

# 3) Seaborn (melhor quando tem hue)
sns.barplot(data=df, x="Tipo", y="Mortes", hue="Pais", errorbar=None)

#com countplot
sns.countplot(x='class', hue='alive', data=df)

dados = np.random.randint(1,7,6000)
sns.countplot(x=dados)
```
| Gráfico | Para que serve? | Eixos necessários | O que o Eixo Y representa por padrão? |
| :--- | :--- | :--- | :--- |
| **`sns.barplot`** | Compara categorias com um valor numérico | `x` (Categoria) e `y` (Número) | Média/Agregação de um valor da base |
| **`sns.countplot`** | Conta quantas vezes cada categoria aparece | Apenas `x` (ou apenas `y`) | Frequência/Quantidade de linhas (`count`) |

**Empilhada a partir de crosstab:**

```python
#região no x, ano no y
tabela = pd.crosstab(df["Regiao"], df["Ano"], values=df["Total"], aggfunc="sum")
tabela.plot(kind="bar", stacked=True)


#o hue vai ser o ano o eixo x vai ser a rtegião e o y vai ser a soma
df3 = pd.crosstab(
                df2['Region_of_Incident'],
                  df2['Reported_Year'], 
                    values=df2['Total_Dead_and_Missing'],
                    aggfunc='sum'
                  )

df3.plot(kind='bar', stacked=False)

```

### Área Empilhada (`kind="area"`)

Mostra magnitude cumulativa ao longo do tempo.

```python
df.set_index("Ano")[["Roubo", "Homicidio", "Furto"]].plot(kind="area", stacked=True)
summary.plot(kind='area', stacked=True)

#ano no eixo x, qtd crime no y e as taxas empilhadas (sendo que cada cor vai representar um crime)
summary = pd.crosstab(df['Year'], df['Crime'], values=df['Rate'], aggfunc=np.sum)
summary.plot(kind='area', stacked=True)


```


### Setar ìndice

Agora a coluna Country pode ser usada como índice
```python
df_gdp.set_index('Country', inplace=True)
```




---

## Aula 10: Linhas, Histogramas e Barras (Seaborn)

### Linhas — duas formas

```python
# Matplotlib / Pandas
df.plot(kind="line", x="Ano", y=["PIB_Brasil", "PIB_Argentina"])

# Seaborn (suporta hue facilmente)
sns.lineplot(data=df, x="Ano", y="Taxa_Crime", hue="Categoria")
```

### Dispersão + Regressão

```python
#fit_reg é a opção da reta
sns.regplot(data=df, x="Idade", y="Pressao_Arterial", scatter_kws={"alpha": 0.6}, fit_reg=True)
```

### Histograma: `histplot` × `displot`

| Função | O que faz | Quando usar |
|--------|-----------|-------------|
| `sns.histplot` | Histograma (pode adicionar KDE) | Dentro de `subplot` ou quando você já tem `ax` |
| `sns.displot` | Figura completa de distribuição | Gráfico único e rápido; cria sua própria figura |

```python
# com .hist
df.hist('age', bins=8,figsize=(8,8))

# histplot (mais controle)
sns.histplot(df["CPI"], bins=15, kde=True)

# displot (atalho para figura inteira)
sns.displot(df["CPI"], bins=15, kde=True)
```

**Dois histogramas lado a lado (padrão de prova):**

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 5))
sns.histplot(df[df["Regiao"]=="Europe"]["CPI"], bins=15, kde=True, ax=axes[0])
sns.histplot(df[df["Regiao"]=="Africa"]["CPI"], bins=15, kde=True, ax=axes[1])
plt.tight_layout()

#USANDO O SUPLOT SEPARADO
plt.subplot(1,2,1)
plt.pie(sizes_sierra, labels=labels_sierra,autopct='%1.1f%%', shadow=True, startangle=90)
plt.title('Pie chart of Ebola deaths in Sierra Leone')

plt.subplot(1,2,2)
plt.pie(sizes_guinea, labels=labels_guinea,autopct='%1.1f%%', shadow=True, startangle=90)
plt.title('Pie chart of Ebola deaths in Guinea')

plt.tight_layout()
plt.show()

```

---

## Aula 11: Crosstab e Groupby Avançado

### O que é `crosstab`?

Tabela de frequência (ou agregação) entre duas ou mais variáveis categóricas.  
Responde: “Quantas vezes a categoria A aparece junto com a categoria B?”

```python
pd.crosstab(
    index,                # o que vai nas linhas
    columns,              # o que vai nas colunas
    values=None,          # coluna numérica (opcional)
    aggfunc=None,         # 'mean', 'sum', 'count'... (obrigatório se values)
    margins=False,        # adiciona totais
    normalize=False       # False | 'all' | 'index' | 'columns'
)
```

**Exemplos essenciais:**

```python
# Contagem simples
ct = pd.crosstab(df["gender"], df["education_level"])

# Média de uma variável numérica
ct_mean = pd.crosstab(df["gender"], df["education_level"],
                      values=df["score"], aggfunc="mean")

# Com totais
ct = pd.crosstab(df["gender"], df["education_level"], margins=True)

# agrupe por ano os crimes,  olhando taxas somadas
summary = pd.crosstab(df['Year'], df['Crime'], values=df['Rate'], aggfunc=np.sum)

# Normalização
pd.crosstab(..., normalize="index")   # % dentro de cada linha
pd.crosstab(..., normalize="columns") # % dentro de cada coluna
pd.crosstab(..., normalize="all")     # % do total geral
pd.crosstab(..., normalize=True) 

#nomear índices
pd.crosstab(df['pickup_borough'], df['payment'], rownames=['Zone'], colnames=['Payment Method'] )
```

**Heatmap (melhor visualização de crosstab):**

```python
#annot é para colocar todas as informações
sns.heatmap(ct, annot=True, cmap="coolwarm", fmt="g")
```

**Barras a partir do crosstab:**

```python
ct.plot(kind="bar")           # agrupadas
ct.plot(kind="bar", stacked=True)  # empilhadas
```

### Groupby — o que é e como usar

`groupby` **parte** o DataFrame por chaves e calcula agregações em cada grupo.

```python
# Média de uma coluna
df.groupby("Company")[["Sales"]].mean()

# Várias funções
df.groupby("Company")["Sales"].agg(["mean", "sum", "count", "std"])

# Funções diferentes por coluna
df.groupby("Company").agg({"Sales": ["mean", "sum"], "Score": "max"})

# Múltiplas chaves
df.groupby(["day", "sex"])["total_bill"].mean()
```

**Regra de ouro para plotar com Seaborn:**  
Sempre use `.reset_index()` para transformar o resultado de volta em DataFrame com colunas normais.

```python
df_agrupado = df.groupby(["day", "sex"])["total_bill"].mean().reset_index()
sns.barplot(data=df_agrupado, x="day", y="total_bill", hue="sex")
```

---

## Aula 12: Distribuição Normal

**O que é:**  
Distribuição **contínua** em forma de sino, simétrica em torno da média **μ**. O desvio padrão **σ** controla a largura.

**Quando usar:**  
- Alturas, pesos, notas padronizadas  
- Erros de medição  
- Qualquer variável que seja soma de muitos fatores independentes (Teorema Central do Limite)

**Área sob a curva = probabilidade.**  
Como é contínua, P(X = valor exato) = 0. Trabalhamos sempre com intervalos.

```python
from scipy.stats import norm

mu, sigma = 0, 1   # normal padrão

norm.pdf(0, mu, sigma)     # densidade no ponto 0
norm.cdf(1.96, mu, sigma)  # P(X ≤ 1.96) ≈ 0.975
norm.sf(1.96, mu, sigma)   # P(X > 1.96)
norm.mean(mu, sigma)
norm.std(mu, sigma)
```

**Regra empírica (muito cobrada):**  
- ≈ 68 % dos dados entre μ − σ e μ + σ  
- ≈ 95 % entre μ − 2σ e μ + 2σ  
- ≈ 99,7 % entre μ − 3σ e μ + 3σ

---

## Aula 13: Distribuição Exponencial

**O que é:**  
Distribuição **contínua** que modela o **tempo de espera** até o próximo evento, quando os eventos seguem um processo de Poisson.

**Quando usar:**  
- Tempo entre chegadas de clientes  
- Tempo até a próxima falha de um equipamento  
- Tempo de vida de componentes eletrônicos  

**Parâmetro:** `scale` = 1/λ (onde λ é a taxa). No `scipy`, o parâmetro principal é `scale`.

```python
from scipy.stats import expon

# scale = 1/λ  (ex.: se λ = 2 eventos/hora, scale = 0.5)
expon.pdf(1, scale=0.5)    # densidade
expon.cdf(1, scale=0.5)    # P(X ≤ 1)
expon.sf(1, scale=0.5)     # P(X > 1)
expon.mean(scale=0.5)      # média = scale
expon.std(scale=0.5)
```

**Relação com Poisson:**  
Se o número de eventos em um intervalo é Poisson(μ), o tempo entre eventos é Exponencial com média 1/μ.

---

## Pegadinhas e Erros Mais Comuns

| Erro | Forma errada | Forma correta |
|------|--------------|---------------|
| `and` / `or` em filtro | `df[df.A>5 and df.B<2]` | `df[(df.A>5) & (df.B<2)]` |
| Esquecer parênteses | `df[df.A>5 & df.B<2]` | `df[(df.A>5) & (df.B<2)]` |
| `values` sem `aggfunc` | `pd.crosstab(x,y,values=z)` | `pd.crosstab(x,y,values=z,aggfunc="mean")` |
| Esquecer `.reset_index()` | `sns.barplot(df.groupby(...).mean())` | `...mean().reset_index()` |
| `annot=True` no heatmap | `sns.heatmap(ct)` | `sns.heatmap(ct, annot=True, fmt="g")` |
| Normalização errada | achar que `normalize=True` é por linha | `normalize="index"` (linha) ou `"columns"` |
| `loc` × `iloc` | `df.loc[0:2]` querendo posição | `df.iloc[0:2]` |
| Subtítulo do boxplot | não limpar | `plt.suptitle("")` |
| Filtrar dentro do boxplot | `df.boxplot(..., filtro)` | filtrar o DataFrame **antes** |

---

### Dicas finais de prova

- Filtro clássico: `df[(df["Op"]=="Op-1") & (df["Comp"]>105)]`
- Boxplot com filtro: `df[df["genre"].isin([...])].boxplot(column="score", by="genre"); plt.suptitle("")`
- Quartis: `st.quantiles(df["col"])` → `[Q1, Q2, Q3]`
- Crosstab completo: `pd.crosstab(..., values=..., aggfunc="mean", margins=True)`
- Groupby + Seaborn: sempre `.reset_index()`
- Heatmap: `annot=True, fmt="g"`

Boa prova! 🚀
