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