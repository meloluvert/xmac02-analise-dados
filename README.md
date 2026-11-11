# Guia de Estudos para Prova: Teorema Central do Limite e Testes de Hipótese

Este guia foi estruturado especificamente para revisão de prova. Ele consolida o **Teorema Central do Limite (TCL)**, o **Roteiro Universal em 6 Etapas** para testes de hipótese e a compilação completa de todos os testes estatísticos abordados no curso, utilizando notação simplificada em texto plano para facilitar a leitura.

---

## 1. O Teorema Central do Limite (TCL) como Fundação

A estatística inferencial utiliza amostras para tomar decisões sobre populações inteiras. O **Teorema Central do Limite (TCL)** é a garantia matemática que permite aplicar a Distribuição Normal na grande maioria dos testes práticos.

* **Conceito Chave**: Independentemente do formato da distribuição original da população (seja ela uniforme, assimétrica ou desconhecida), a **distribuição amostral das médias** se aproxima de uma **Distribuição Normal** conforme o tamanho da amostra cresce (regra prática: `n >= 30`).
* **Média da Distribuição Amostral**: A média das médias amostrais é igual à média populacional original:
  `Média(médias) = mu`
* **Erro Padrão da Média (EP)**: É a medida da variabilidade das médias amostrais. Diminui à medida que o tamanho da amostra aumenta:
  `Erro Padrão (EP) = sigma / sqrt(n)`  (quando o desvio padrão populacional sigma é conhecido)
  `Erro Padrão (EP) = s / sqrt(n)`      (quando estimado pelo desvio padrão amostral s)

> **Por que isso importa na prova?**  
> Graças ao TCL, podemos transformar qualquer média amostral em uma pontuação padronizada `Z` ou `t` e consultar tabelas de probabilidade para tomar decisões.

---

## 2. As 6 Etapas Universais do Teste de Hipótese

Todos os testes paramétricos seguem rigorosamente a mesma sequência lógica de 6 passos.

### Passo 1: Definir a Hipótese Nula (Ho)
É a afirmação inicial de igualdade ou ausência de efeito (o "status quo"). Sempre contém um sinal de igualdade (`=`, `<=`, ou `>=`).
* Exemplo: `Ho: mu = 150 ml`

### Passo 2: Definir a Hipótese Alternativa (Ha)
É a hipótese de mudança, efeito ou diferença que o pesquisador quer comprovar. Nunca contém igualdade (`<>` para bicaudal, `>` ou `<` para unicaudal).
* **Bilateral (Duas Caudas)**: `Ha: mu <> 150 ml` (Busca qualquer diferença)
* **Unilateral à Direita (Uma Cauda)**: `Ha: mu > 150 ml` (Busca aumento)
* **Unilateral à Esquerda (Uma Cauda)**: `Ha: mu < 150 ml` (Busca redução)

### Passo 3: Definir a Probabilidade de Erro (Nível de Significância alpha)
Fixa-se a tolerância para o **Erro Tipo I** antes de coletar os dados.
* **Valores Padrão**: `alpha = 0,05` (5%), `alpha = 0,01` (1%), ou `alpha = 0,10` (10%).
* **Nível de Confiança (C)**: `C = 1 - alpha` (Ex.: se `alpha = 0,05`, Confiança = 95%).

#### Matriz de Decisão: Erros Tipo I e Tipo II
* **Erro Tipo I (alpha)**: Rejeitar `Ho` quando `Ho` é verdadeira (Alarme falso / Risco do Produtor).
* **Erro Tipo II (beta)**: Falhar em rejeitar `Ho` quando `Ho` é falsa (Alarme não soa / Risco do Consumidor).
* **Potência do Teste**: `1 - beta` (Capacidade do teste de rejeitar corretamente uma hipótese nula falsa).

### Passo 4: Calcular a Estatística de Teste
Aplica-se a fórmula do teste escolhido (calculando `Z_cal`, `t_cal`, `Chi2_cal` ou `F_cal`). A estatística mede a quantidade de erros padrões que os dados amostrais estão distantes do valor postulado em `Ho`.

### Passo 5: Definir o Valor Crítico (ou p-valor)
* **Abordagem pelo Valor Crítico**: Determina-se a fronteira na distribuição (`Z_crit`, `t_crit`, etc.) com base no `alpha` e nos graus de liberdade (`df`).
* **Abordagem pelo p-valor**: 
  * Se `p-valor < alpha` -> Rejeita-se `Ho`
  * Se `p-valor >= alpha` -> Falha-se em rejeitar `Ho` (Confirma-se `Ho`)

  [explicar que o Z crítico é o ponto da curva onde o alpha começa a "contar"]

### Passo 6: Tomar a Decisão e Interpretar os Resultados
Compara-se a estatística calculada com o valor crítico e conclui-se em termos práticos do problema (ex.: "Há evidência estatística de que a máquina está desregulada").

---

## 3. Tabela Comparativa de Todos os Testes do Curso

| Teste | Parâmetro Analisado | Condição Principal | Distribuição Usada | Estatística Calculada |
| :--- | :--- | :--- | :--- | :--- |
| **Teste Z (1 Amostra)** | Média (`mu`) | `sigma` conhecido OU `n >= 30` | Normal Padrão (`Z`) | `Z_cal` |
| **Teste t (1 Amostra)** | Média (`mu`) | `sigma` desconhecido E `n < 30` | t de Student (`df = n - 1`) | `t_cal` |
| **Teste de 1 Proporção** | Proporção (`p`) | Binomial com `n*p0 >= 10` e `n*(1-p0) >= 10` | Normal Padrão (`Z`) | `Z_cal` |
| **Teste de 1 Variância** | Variância (`sigma^2`) | Dados com distribuição normal | Chi-Quadrado (`df = n - 1`) | `Chi2_cal` |
| **Teste Z (2 Amostras)** | Comparação de Médias (`mu1 - mu2`) | Amostras independentes; `sigma1, sigma2` conhecidos OU `n1, n2 >= 30` | Normal Padrão (`Z`) | `Z_cal` |
| **Teste t (2 Amostras)** | Comparação de Médias (`mu1 - mu2`) | Amostras independentes; `sigma` desconhecido e `n < 30` | t de Student (Variâncias Iguais ou Diferentes) | `t_cal` |
| **Teste t Pareado** | Média das Diferenças (`mu_d`) | Amostras dependentes (Antes vs Depois no mesmo sujeito) | t de Student (`df = n - 1`) | `t_cal` |
| **Teste de 2 Proporções** | Comparação de Proporções (`p1 - p2`) | Amostras binomiais independentes com min. 10 sucessos/falhas cada | Normal Padrão (`Z`) | `Z_cal` |
| **Teste F (2 Variâncias)** | Comparação de Variâncias (`sigma1^2 / sigma2^2`) | Amostras independentes de populações normais | F de Snedecor (`df1 = n1-1`, `df2 = n2-1`) | `F_cal` |
| **ANOVA (3+ Médias)** | Média de 3+ Grupos (`mu1 = mu2 = ... = muk`) | Amostras independentes de populações normais | F de Snedecor (`df_ext = k-1`, `df_int = N-k`) | `F_cal` |

---

## 4. Detalhamento Simplificado Teste a Teste

### 4.1. Teste Z para 1 Amostra (Média)
* **Hipóteses**: `Ho: mu = mu0` vs `Ha: mu <> mu0` (ou `>` / `<`)
* **Condições**: População normal com desvio padrão `sigma` conhecido OU `n >= 30`.
* **Fórmula**:
  `Z_cal = (x_bar - mu0) / (sigma / sqrt(n))`

### 4.2. Teste t de Student para 1 Amostra (Média)
* **Hipóteses**: `Ho: mu = mu0` vs `Ha: mu <> mu0`
* **Condições**: População normal com desvio padrão populacional desconhecido e amostra pequena (`n < 30`). Usa-se o desvio amostral `s`.
* **Graus de Liberdade**: `df = n - 1`

oq são: (explicar)

falar que os testes que pedem graud de liberdade é por conta da  desvio padrão da população ($\sigma$) é desconhecido, por exmeplo: quando queremos saber se o desviopadr~qao mudou, mas e se não tivermos a média original?

Veja o que acontece na prática com os 51 frascos:O 1º frasco deu $150{,}1\text{ ml}$ $\rightarrow$ tem a "liberdade" de dar qualquer valor.O 2º frasco deu $149{,}8\text{ ml}$ $\rightarrow$ também é um dado livre....O 50º frasco deu $150{,}4\text{ ml}$ $\rightarrow$ ainda é um dado livre.Chegando no 51º frasco, o volume dele não é mais uma informação independente sobre a variabilidade da fábrica. Por quê? Porque a soma de todos os 51 desvios em relação à média amostral tem que fechar exatamente em ZERO. O valor do 51º frasco já está totalmente "preso" aos outros 50.
* **Fórmula**:
  `t_cal = (x_bar - mu0) / (s / sqrt(n))`

### 4.3. Teste para 1 Proporção Binomial
* **Hipóteses**: `Ho: p = p0` vs `Ha: p <> p0`
* **Condições**: Dados binários (sucesso/falha). Aproximação normal válida se `n * p0 >= 10` e `n * (1 - p0) >= 10`.
* **Fórmula**:
  `Z_cal = (p_hat - p0) / sqrt( (p0 * (1 - p0)) / n )`
  *(onde `p_hat = sucessos / n`)*

### 4.4. Teste Chi-Quadrado (Chi2) para 1 Variância
* **Hipóteses**: `Ho: sigma^2 <= sigma0^2` vs `Ha: sigma^2 > sigma0^2`
* **Condições**: Amostra aleatória de população com distribuição normal.
* **Graus de Liberdade**: `df = n - 1`
* **Fórmula**:
  `Chi2_cal = (n - 1) * s^2 / sigma0^2`

### 4.5. Teste Z e Teste t para 2 Amostras Independentes (Comparação de Médias)
* **Hipóteses**: `Ho: mu1 = mu2` (ou `mu1 - mu2 = 0`) vs `Ha: mu1 <> mu2`
* **Caso Z (sigmas conhecidos ou n1, n2 >= 30)**:
  `Z_cal = (x_bar1 - x_bar2) / sqrt( (sigma1^2 / n1) + (sigma2^2 / n2) )`

* **Caso t com Variâncias Iguais (Homocedasticidade)**:
  * Variância Combinada (`sp^2`):
    `sp^2 = [ (n1 - 1) * s1^2 + (n2 - 1) * s2^2 ] / (n1 + n2 - 2)`
  * Estatística de Teste:
    `t_cal = (x_bar1 - x_bar2) / ( sp * sqrt( (1 / n1) + (1 / n2) ) )`
  * Graus de Liberdade: `df = n1 + n2 - 2`

* **Caso t com Variâncias Diferentes (Heterocedasticidade)**:
  `t_cal = (x_bar1 - x_bar2) / sqrt( (s1^2 / n1) + (s2^2 / n2) )`
  *(Graus de liberdade ajustados pela fórmula de Welch)*

### 4.6. Teste t Pareado (Amostras Dependentes)
* **Aplicação**: Dados pareados do tipo "antes e depois" no mesmo indivíduo.
* **Procedimento**: Calcula-se a diferença individual `d = Antes - Depois`.
* **Hipóteses**: `Ho: mu_d = 0` vs `Ha: mu_d <> 0`
* **Graus de Liberdade**: `df = n - 1`  *(onde n é o número de pares)*
* **Fórmula**:
  `t_cal = d_bar / (s_d / sqrt(n))`
  *(onde `d_bar` é a média das diferenças e `s_d` é o desvio padrão das diferenças)*

### 4.7. Teste para 2 Proporções Binomiais
* **Hipóteses**: `Ho: p1 - p2 = 0` vs `Ha: p1 - p2 <> 0`
* **Condições**: Mínimo de 10 sucessos e 10 falhas em cada amostra.
* **Proporção Agrupada (Pooled)**:
  `p_bar = (n1 * p1_hat + n2 * p2_hat) / (n1 + n2)`
* **Fórmula**:
  `Z_cal = (p1_hat - p2_hat) / sqrt( p_bar * (1 - p_bar) * ( (1 / n1) + (1 / n2) ) )`

### 4.8. Teste F de Snedecor para 2 Variâncias
* **Hipóteses**: `Ho: sigma1^2 = sigma2^2` vs `Ha: sigma1^2 <> sigma2^2`
* **Regra Prática**: Colocar sempre a maior variância amostral no numerador (`s1^2 > s2^2`) para facilitar a consulta na tabela (assim `F_cal >= 1`).
* **Graus de Liberdade**: `df1 = n1 - 1` (numerador) e `df2 = n2 - 1` (denominador).
* **Fórmula**:
  `F_cal = s1^2 / s2^2`

### 4.9. ANOVA (Análise de Variância) para 3 ou Mais Médias
* **Motivação**: Comparar 3 ou mais grupos simultaneamente. Fazer múltiplos testes t individuais inflaria a taxa de Erro Tipo I. Por exemplo, 6 testes t individuais a 95% de confiança reduziriam a confiança global para apenas `0.95^6 = 73.5%` (1 erro a cada 4 testes!).
* **Hipóteses**: 
  * `Ho: mu1 = mu2 = mu3 = ... = muk`
  * `Ha: Ao menos uma das médias é diferente das outras`
* **Lógica**: Compara a variabilidade **entre grupos** (externa) com a variabilidade **dentro dos grupos** (interna).
* **Graus de Liberdade**:
  * Externa (Numerador): `df_ext = k - 1`  *(k = número de grupos)*
  * Interna (Denominador): `df_int = N - k`  *(N = total geral de observações)*
  * Total: `df_total = N - 1`
* **Fórmula da Estatística F**:
  `MSQ_externa = SQ_externa / df_ext`
  `MSQ_interna = SQ_interna / df_int`
  `F_cal = MSQ_externa / MSQ_interna`

---

## 5. Checklist de Decisão Rápida para a Prova

Para saber qual teste aplicar na questão da prova, faça estas 3 perguntas:

1. **Qual é o parâmetro?**
   * **Média**: Teste Z, Teste t, t Pareado ou ANOVA.
   * **Proporção**: Teste Z de 1 ou 2 Proporções.
   * **Variância**: Chi-Quadrado ou Teste F.

2. **Quantos grupos estão sendo comparados?**
   * **1 Grupo**: Z de 1 amostra, t de 1 amostra, 1 Proporção, Chi-Quadrado de 1 variância.
   * **2 Grupos**: Z de 2 amostras, t de 2 amostras (independentes ou pareadas), 2 Proporções, F de 2 variâncias.
   * **3 ou mais Grupos**: ANOVA.

3. **O desvio padrão populacional (sigma) é conhecido ou amostral (s)? A amostra é grande (n >= 30)?**
   * Se `sigma` for conhecido OU `n >= 30` -> Usar **Distribuição Z**.
   * Se `sigma` for desconhecido E `n < 30` -> Usar **Distribuição t de Student** (`df = n - 1`).


Oq falta:

explicar o equal_var no ttest_ind
(variâncias uiguais ou difewrentes)


para saber isso, 


# Guia de Estudos para Prova
## Teorema Central do Limite e Testes de Hipótese

Este guia reúne os conceitos fundamentais para a prova: **Teorema Central do Limite (TCL)**, roteiro de testes de hipótese, escolha do teste adequado, graus de liberdade e interpretação do parâmetro `equal_var` no Python.

> **Notação:** `μ` = média populacional; `σ` = desvio padrão populacional; `σ²` = variância populacional; `x̄` = média amostral; `s` = desvio padrão amostral; `n` = tamanho da amostra; `p` = proporção populacional; `p̂` = proporção amostral; `α` = nível de significância.

---

## 1. Teorema Central do Limite (TCL)

A estatística inferencial usa amostras para tirar conclusões sobre populações. O **Teorema Central do Limite (TCL)** explica por que a distribuição Normal aparece em muitos procedimentos estatísticos.

### Conceito-chave

Sob condições usuais — especialmente observações independentes, com mesma distribuição e variância finita —, a **distribuição amostral da média** tende a se aproximar de uma distribuição Normal conforme `n` aumenta, mesmo que a população original não seja Normal.

Uma regra prática comum é considerar `n ≥ 30`, mas isso **não é uma garantia universal**: populações muito assimétricas ou com valores extremos podem exigir amostras maiores. Se a população é Normal, a média amostral é Normal para qualquer tamanho de amostra.

### Média e erro padrão

- **Média da distribuição amostral:** `E(x̄) = μ`.
- **Erro padrão da média (EP):** mede a variabilidade esperada entre médias de amostras.

Se `σ` é conhecido:

`EP = σ / √n`

Se `σ` é desconhecido e estimado por `s`:

`EP estimado = s / √n`

Quanto maior `n`, menor tende a ser o erro padrão.

**Por que isso importa?** O TCL permite usar aproximações Normal em muitos problemas. A estatística de teste padroniza a diferença entre o resultado observado e o valor previsto pela hipótese nula, em unidades de erro padrão.

---

## 2. Roteiro universal em 6 etapas para testes de hipótese

### Etapa 1 — Definir a hipótese nula (`H₀`)

É a afirmação de referência, geralmente de ausência de efeito ou diferença. A hipótese nula contém a igualdade. Exemplo:

`H₀: μ = 150 ml`

Em testes unilaterais, a hipótese nula pode ser escrita com desigualdade (`≤` ou `≥`), mas o cálculo é feito na fronteira de igualdade.

### Etapa 2 — Definir a hipótese alternativa (`Hₐ`)

Representa o efeito ou diferença que se procura evidenciar. Ela não contém igualdade.

- **Bilateral (duas caudas):** `Hₐ: μ ≠ 150 ml` — procura qualquer diferença.
- **Unilateral à direita:** `Hₐ: μ > 150 ml` — procura aumento.
- **Unilateral à esquerda:** `Hₐ: μ < 150 ml` — procura redução.

A direção deve ser definida antes de observar os resultados.

### Etapa 3 — Definir o nível de significância (`α`)

É a probabilidade máxima tolerada de cometer **Erro Tipo I**, isto é, rejeitar `H₀` quando ela é verdadeira.

Valores comuns: `α = 0,10`, `0,05` ou `0,01`.

O nível de confiança associado é `C = 1 − α`. Por exemplo, `α = 0,05` corresponde a 95% de confiança em um intervalo de confiança relacionado.

#### Erros e potência

| Realidade | Não rejeitar `H₀` | Rejeitar `H₀` |
|---|---|---|
| `H₀` é verdadeira | Decisão correta | **Erro Tipo I (`α`)** |
| `H₀` é falsa | **Erro Tipo II (`β`)** | Decisão correta: potência |

- **Erro Tipo I (`α`):** falso positivo; rejeitar uma hipótese nula verdadeira.
- **Erro Tipo II (`β`):** falso negativo; não rejeitar uma hipótese nula falsa.
- **Potência (`1 − β`):** probabilidade de rejeitar corretamente `H₀` quando ela é falsa.

> “Não rejeitar `H₀`” não significa provar ou confirmar que `H₀` é verdadeira. Significa apenas que os dados não forneceram evidência suficiente contra ela.

### Etapa 4 — Calcular a estatística de teste

Escolhe-se a fórmula adequada e calcula-se, por exemplo, `Z_cal`, `t_cal`, `χ²_cal` ou `F_cal`. A estatística expressa o quão distante o resultado observado está do valor previsto por `H₀`, considerando a variabilidade.

### Etapa 5 — Encontrar o valor crítico ou o p-valor

**Abordagem pelo valor crítico**

O valor crítico é a fronteira que separa a região de não rejeição da região crítica (de rejeição). Ele depende da distribuição usada, de `α`, do tipo de teste (uni ou bilateral) e, no caso da distribuição t, dos graus de liberdade.

**O que é o `Z` crítico?**

É o ponto no eixo horizontal da curva Normal padrão que delimita a região crítica. A área de cauda além desse ponto é `α` (em teste unilateral) ou `α/2` em cada cauda (em teste bilateral).

Exemplos para a Normal padrão:

- Teste unilateral à direita com `α = 0,05`: `Z_crit ≈ 1,645`.
- Teste unilateral à esquerda com `α = 0,05`: `Z_crit ≈ −1,645`.
- Teste bilateral com `α = 0,05`: `Z_crit ≈ ±1,96`.

Assim, em um teste bilateral a 5%, os 5% de área crítica ficam divididos: 2,5% em cada cauda.

**Abordagem pelo p-valor**

O p-valor é a probabilidade, supondo `H₀` verdadeira, de observar uma estatística tão extrema quanto (ou mais extrema que) a obtida, na direção definida por `Hₐ`.

- Se `p-valor ≤ α`: **rejeita-se `H₀`**.
- Se `p-valor > α`: **não se rejeita `H₀`**.

O p-valor não é a probabilidade de `H₀` ser verdadeira.

### Etapa 6 — Decidir e interpretar no contexto

A conclusão deve responder à pergunta prática. Exemplo:

“Como o p-valor é menor que 0,05, rejeitamos `H₀`. Há evidência estatística, ao nível de 5%, de que o volume médio difere de 150 ml.”

Evite concluir que uma diferença é importante na prática apenas porque ela é estatisticamente significativa.

---

## 3. Tabela comparativa dos testes

| Teste | Parâmetro | Condições principais | Distribuição | Estatística |
|---|---|---|---|---|
| Z de 1 amostra | Média `μ` | `σ` conhecido; ou aproximação para amostra grande sob condições adequadas | Normal padrão | `Z_cal` |
| t de 1 amostra | Média `μ` | `σ` desconhecido; população Normal para amostra pequena | t de Student, `df = n − 1` | `t_cal` |
| 1 proporção | Proporção `p` | Dados sucesso/falha; contagens esperadas suficientes | Normal padrão aproximada | `Z_cal` |
| 1 variância | Variância `σ²` | Amostra aleatória de população Normal | Qui-quadrado, `df = n − 1` | `χ²_cal` |
| Z de 2 amostras | Diferença `μ₁ − μ₂` | Amostras independentes; desvios conhecidos (ou aproximação grande amostral adequada) | Normal padrão | `Z_cal` |
| t de 2 amostras | Diferença `μ₁ − μ₂` | Amostras independentes; desvios desconhecidos | t de Student (pooled ou Welch) | `t_cal` |
| t pareado | Média das diferenças `μ_d` | Dados dependentes em pares | t de Student, `df = n_pares − 1` | `t_cal` |
| 2 proporções | Diferença `p₁ − p₂` | Amostras independentes; contagens suficientes | Normal padrão aproximada | `Z_cal` |
| F de 2 variâncias | Razão `σ₁²/σ₂²` | Amostras independentes de populações Normais | F de Snedecor | `F_cal` |
| ANOVA (3+ médias) | Médias de `k` grupos | Independência, normalidade dos resíduos e variâncias semelhantes (na ANOVA clássica) | F de Snedecor | `F_cal` |

> As condições resumidas são regras de escolha. Em situações específicas, os pressupostos e a aproximação apropriada precisam ser verificados.

---

## 4. Detalhamento dos testes

### 4.1. Teste Z para 1 amostra (média)

- **Hipóteses:** `H₀: μ = μ₀` contra `Hₐ: μ ≠ μ₀` (ou `>` / `<`).
- **Condições:** população Normal com `σ` conhecido; para amostras grandes, a aproximação pode ser adequada pelo TCL.
- **Fórmula:**

`Z_cal = (x̄ − μ₀) / (σ / √n)`

### 4.2. Teste t de Student para 1 amostra (média)

- **Hipóteses:** `H₀: μ = μ₀` contra `Hₐ: μ ≠ μ₀`.
- **Condições:** `σ` desconhecido. Para amostra pequena, é importante que a população seja aproximadamente Normal; usa-se `s` para estimar `σ`.
- **Estatística:**

`t_cal = (x̄ − μ₀) / (s / √n)`

- **Graus de liberdade:** `df = n − 1`.

#### O que são graus de liberdade?

Graus de liberdade (`df`, do inglês *degrees of freedom*) representam quantas informações podem variar independentemente depois que uma ou mais restrições foram impostas aos dados.

Ao calcular o desvio padrão amostral, primeiro usamos os dados para calcular a média `x̄`. Isso impõe uma restrição: a soma dos desvios em relação à média é zero,

`Σ(xᵢ − x̄) = 0`.

Por isso, em uma amostra com 51 observações, depois de conhecer 50 desvios em relação à média, o último fica determinado pela soma zero. Há, então, `51 − 1 = 50` graus de liberdade para estimar a variabilidade.

**Exemplo dos 51 frascos:** os primeiros 50 volumes podem variar; o 51º não pode ser escolhido livremente se a média amostral já estiver fixada, pois precisa fazer a soma dos desvios fechar em zero.

Isso explica por que aparece `n − 1` em vários testes que usam a variância amostral. Não é simplesmente porque `σ` é desconhecido: a perda de um grau de liberdade decorre da estimação da média a partir da própria amostra.

### 4.3. Teste para 1 proporção binomial

- **Hipóteses:** `H₀: p = p₀` contra `Hₐ: p ≠ p₀`.
- **Dados:** cada observação é sucesso/falha.
- **Condição usual para aproximação Normal:** `n p₀ ≥ 10` e `n(1 − p₀) ≥ 10` (alguns cursos usam outros limites).
- **Proporção amostral:** `p̂ = sucessos / n`.
- **Fórmula:**

`Z_cal = (p̂ − p₀) / √[p₀(1 − p₀) / n]`

### 4.4. Teste qui-quadrado (`χ²`) para 1 variância

- **Hipóteses (exemplo unilateral à direita):** `H₀: σ² = σ₀²` contra `Hₐ: σ² > σ₀²`.
- **Condição:** amostra aleatória de uma população Normal.
- **Graus de liberdade:** `df = n − 1`.
- **Fórmula:**

`χ²_cal = (n − 1)s² / σ₀²`

A hipótese nula é escrita na fronteira `σ² = σ₀²` para calcular a estatística. Também é possível formular testes à esquerda ou bilaterais.

### 4.5. Testes Z e t para 2 amostras independentes (comparação de médias)

- **Hipóteses usuais:** `H₀: μ₁ − μ₂ = 0` contra `Hₐ: μ₁ − μ₂ ≠ 0`.
- **Independentes:** as observações de um grupo não são pareadas com as do outro.

#### Caso Z

Usado quando os desvios padrão populacionais são conhecidos:

`Z_cal = (x̄₁ − x̄₂) / √[(σ₁²/n₁) + (σ₂²/n₂)]`

Em amostras grandes, procedimentos aproximados também podem ser usados quando seus pressupostos são razoáveis.

#### Caso t com variâncias iguais (pooled)

Quando se assume que as variâncias populacionais são iguais, estima-se uma variância comum combinando as duas variâncias amostrais:

`sp² = [(n₁ − 1)s₁² + (n₂ − 1)s₂²] / (n₁ + n₂ − 2)`

`sp = √sp²`

` t_cal = (x̄₁ − x̄₂) / [sp √(1/n₁ + 1/n₂)] `

`df = n₁ + n₂ − 2`

#### Caso t com variâncias diferentes (Welch)

Não se exige que as variâncias populacionais sejam iguais:

`t_cal = (x̄₁ − x̄₂) / √[(s₁²/n₁) + (s₂²/n₂)]`

Os graus de liberdade são aproximados pela fórmula de Welch–Satterthwaite:

`df ≈ [(s₁²/n₁ + s₂²/n₂)²] / [((s₁²/n₁)²/(n₁−1)) + ((s₂²/n₂)²/(n₂−1))]`

### 4.6. Teste t pareado (amostras dependentes)

- **Aplicação:** medidas “antes e depois” no mesmo indivíduo, ou pares naturalmente relacionados.
- **Procedimento:** calcular uma diferença por par, por exemplo `dᵢ = Antesᵢ − Depoisᵢ`.
- **Hipóteses:** `H₀: μ_d = 0` contra `Hₐ: μ_d ≠ 0`.
- **Graus de liberdade:** `df = n − 1`, em que `n` é o número de pares.
- **Fórmula:**

`t_cal = d̄ / (s_d / √n)`

Aqui, `d̄` é a média das diferenças e `s_d` é o desvio padrão dessas diferenças. O teste é feito sobre a lista de diferenças, não tratando as duas medições como grupos independentes.

### 4.7. Teste para 2 proporções binomiais

- **Hipóteses:** `H₀: p₁ − p₂ = 0` contra `Hₐ: p₁ − p₂ ≠ 0`.
- **Condições:** amostras independentes e contagens suficientes de sucessos e falhas para a aproximação Normal.
- **Proporções amostrais:** `p̂₁ = x₁/n₁` e `p̂₂ = x₂/n₂`.
- **Proporção agrupada sob `H₀`:**

`p̄ = (x₁ + x₂) / (n₁ + n₂)`

equivalentemente,

`p̄ = (n₁p̂₁ + n₂p̂₂) / (n₁ + n₂)`

- **Estatística:**

`Z_cal = (p̂₁ − p̂₂) / √[p̄(1 − p̄)(1/n₁ + 1/n₂)]`

### 4.8. Teste F de Snedecor para 2 variâncias

- **Hipóteses:** `H₀: σ₁² = σ₂²` contra `Hₐ: σ₁² ≠ σ₂²`.
- **Condições:** amostras independentes de populações Normais.
- **Estatística:** `F_cal = s₁² / s₂²`.
- **Graus de liberdade:** `df₁ = n₁ − 1` (numerador) e `df₂ = n₂ − 1` (denominador).

Para facilitar uma consulta específica de tabela, alguns materiais colocam a maior variância amostral no numerador, fazendo `F_cal ≥ 1`. Porém, é necessário manter os graus de liberdade correspondentes a cada variância e usar a cauda/tabela adequada. Em um teste bilateral, a decisão deve considerar as duas caudas.

### 4.9. ANOVA (análise de variância) para 3 ou mais médias

- **Motivação:** comparar `k ≥ 3` médias simultaneamente. Fazer vários testes t aumenta a chance de pelo menos um Erro Tipo I no conjunto de comparações.
- **Hipóteses:**
  - `H₀: μ₁ = μ₂ = … = μₖ`
  - `Hₐ: pelo menos uma média é diferente`.
- **Lógica:** compara a variabilidade **entre grupos** com a variabilidade **dentro dos grupos**.
- **Graus de liberdade:**
  - Entre grupos (numerador): `df₁ = k − 1`.
  - Dentro dos grupos (denominador): `df₂ = N − k`.
  - Total: `df_total = N − 1`.
- **Quadrados médios:**

`MSQ_entre = SQ_entre / (k − 1)`

`MSQ_dentro = SQ_dentro / (N − k)`

- **Estatística:**

`F_cal = MSQ_entre / MSQ_dentro`

A ANOVA indica se há evidência de que nem todas as médias são iguais; sozinha, não identifica exatamente quais grupos diferem. Para isso, podem ser necessários testes posteriores (*post hoc*), como Tukey, conforme o conteúdo da disciplina.

---

## 5. `equal_var` no `ttest_ind` do Python

A função `scipy.stats.ttest_ind` compara as médias de **duas amostras independentes**. O parâmetro `equal_var` informa qual suposição será usada sobre as variâncias populacionais.

```python
from scipy.stats import ttest_ind

resultado = ttest_ind(amostra1, amostra2, equal_var=True)
```

- **`equal_var=True` (padrão):** assume variâncias populacionais iguais. Usa o teste t clássico com variância combinada (*pooled*), cuja fórmula é apresentada na seção 4.5.
- **`equal_var=False`:** não assume variâncias iguais. Usa o **teste t de Welch**, que calcula o erro padrão com as variâncias separadas e ajusta os graus de liberdade.

### Como decidir?

A decisão não deve ser feita apenas olhando se os tamanhos das amostras são iguais. O ponto é se a hipótese de variâncias iguais é plausível.

- Se o enunciado disser que as variâncias são iguais (ou que há homocedasticidade), use `equal_var=True`.
- Se disser que são diferentes (heterocedasticidade), use `equal_var=False`.
- Se não houver justificativa para assumir variâncias iguais, **Welch (`equal_var=False`) costuma ser uma escolha segura e robusta**. Ele também funciona bem quando as variâncias são iguais, embora possa perder um pouco de eficiência em certas condições.

```python
# Assume variâncias iguais (pooled)
ttest_ind(amostra1, amostra2, equal_var=True)

# Não assume variâncias iguais (Welch)
ttest_ind(amostra1, amostra2, equal_var=False)
```

**Atenção:** `ttest_ind` é para amostras independentes. Para dados “antes e depois” ou pares relacionados, use um teste pareado, como `scipy.stats.ttest_rel`.

---

## 6. Checklist de decisão rápida para a prova

Faça estas perguntas:

### 1. Qual parâmetro está sendo analisado?

- **Média:** Z, t de 1 amostra, t de 2 amostras, t pareado ou ANOVA.
- **Proporção:** teste Z de 1 ou 2 proporções.
- **Variância:** qui-quadrado de 1 variância ou F de 2 variâncias.

### 2. Quantos grupos ou amostras estão sendo comparados?

- **1 amostra:** Z/t de 1 média, 1 proporção ou qui-quadrado de 1 variância.
- **2 amostras:** Z/t de 2 médias, t pareado (se os dados forem dependentes), 2 proporções ou F de 2 variâncias.
- **3 ou mais grupos:** ANOVA para comparar médias.

### 3. As amostras são independentes ou dependentes?

- **Independentes:** grupos distintos, sem pareamento entre observações.
- **Dependentes/pareadas:** mesmas pessoas antes e depois, ou observações organizadas em pares.

### 4. Para médias, `σ` é conhecido?

- **`σ` conhecido:** teste Z, sob os pressupostos apropriados.
- **`σ` desconhecido:** teste t; para duas amostras independentes, decidir entre pooled e Welch conforme a suposição sobre variâncias.
- **Amostra grande (`n ≥ 30`):** o TCL pode justificar aproximações, mas não transforma automaticamente qualquer situação em teste Z. Siga os pressupostos e a orientação da disciplina.

---

## Resumo final

- **TCL:** a distribuição das médias amostrais tende à Normal conforme o tamanho da amostra cresce, sob condições adequadas.
- **`α`:** probabilidade de Erro Tipo I tolerada.
- **p-valor ≤ α:** rejeitar `H₀`; **p-valor > α:** não rejeitar `H₀`.
- **Graus de liberdade:** quantidade de informação independente restante após restrições; em muitos casos com variância amostral, aparece `n − 1`.
- **`equal_var=True`:** t de duas amostras com variâncias iguais (*pooled*).
- **`equal_var=False`:** t de Welch, sem assumir variâncias iguais.
- **Conclusão do teste:** sempre escrever no contexto do problema, sem afirmar que `H₀` foi provada.