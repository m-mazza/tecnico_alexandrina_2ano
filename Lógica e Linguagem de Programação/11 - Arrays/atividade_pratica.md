# Atividade Prática: Decifrando os Dados

**Curso:** Técnico em Desenvolvimento de Sistemas — Educação Profissional Paulista  
**Unidade:** Vetores (arrays unidimensionais)  
**Nome:** _________________________________ **Turma:** _________

---

## Objetivo

Identificar e extrair informações de um vetor ao percorrê-lo, calculando soma, maior, menor e média por meio de um teste de mesa.

---

## Contexto

Você e sua dupla são analistas de dados juniores. A equipe de marketing precisa de uma análise rápida sobre o desempenho de um novo jogador. Vocês receberam os dados brutos (as pontuações) e precisam extrair insights valiosos.

---

## Materiais necessários

- Computador com ambiente de desenvolvimento.
- Editor de texto ou IDE para pseudocódigo.
- Papel e caneta ou um editor de texto simples.

---

## Parte 1: Preparação

1. O vetor de pontuações do jogador é: `[80, 100, 60, 120]`
2. Preparem as três variáveis que precisarão rastrear: `soma`, `maior` e `menor`.

---

## Parte 2: Inicialização das variáveis

Antes de percorrer o vetor, definam os valores iniciais:

- `soma = 0`
- `maior = 80` *(primeiro elemento do vetor)*
- `menor = 80` *(primeiro elemento do vetor)*

> Por que usar o primeiro elemento como referência para `maior` e `menor`? Começar com `0` para `menor` poderia gerar um resultado incorreto caso todos os valores fossem positivos e maiores que zero.

---

## Parte 3: Teste de mesa — rastreando a varredura

Percorra o vetor elemento por elemento e atualize as variáveis a cada iteração.

### Iteração 1 — Elemento: `80`

| Operação | Cálculo | Resultado |
|---|---|---|
| soma | 0 + 80 | 80 |
| 80 > maior (80)? | Não | maior = 80 |
| 80 < menor (80)? | Não | menor = 80 |

**Estado:** `soma=80, maior=80, menor=80`

---

### Iteração 2 — Elemento: `100`

| Operação | Cálculo | Resultado |
|---|---|---|
| soma | 80 + 100 | 180 |
| 100 > maior (80)? | Sim | maior = 100 |
| 100 < menor (80)? | Não | menor = 80 |

**Estado:** `soma=180, maior=100, menor=80`

---

### Iteração 3 — Elemento: `60`

| Operação | Cálculo | Resultado |
|---|---|---|
| soma | 180 + 60 | 240 |
| 60 > maior (100)? | Não | maior = 100 |
| 60 < menor (80)? | Sim | menor = 60 |

**Estado:** `soma=240, maior=100, menor=60`

---

### Iteração 4 — Elemento: `120`

| Operação | Cálculo | Resultado |
|---|---|---|
| soma | 240 + 120 | 360 |
| 120 > maior (100)? | Sim | maior = 120 |
| 120 < menor (60)? | Não | menor = 60 |

**Estado:** `soma=360, maior=120, menor=60`

---

## Parte 4: Finalizando a análise

**Valores finais após percorrer todo o vetor:**

- `soma = 360`
- `maior = 120`
- `menor = 60`

**Cálculo da média:**

```
média = soma / número de elementos
média = 360 / 4 = 90
```

**Relatório final para a equipe de marketing:**

| Métrica | Valor |
|---|---|
| Pontuação média | 90 |
| Melhor pontuação (máximo) | 120 |
| Pior pontuação (mínimo) | 60 |

> **Insight:** O jogador apresenta desempenho consistente, com média de 90 pontos. A variação entre mínimo (60) e máximo (120) indica oscilação de performance que pode ser investigada.

---

## Implementação em Python

```python
pontuacoes = [80, 100, 60, 120]

soma = 0
maior = pontuacoes[0]
menor = pontuacoes[0]

for pontuacao in pontuacoes:
    soma += pontuacao
    if pontuacao > maior:
        maior = pontuacao
    if pontuacao < menor:
        menor = pontuacao

media = soma / len(pontuacoes)

print(f"Pontuação média:           {media:.1f}")
print(f"Melhor pontuação (máximo): {maior}")
print(f"Pior pontuação (mínimo):   {menor}")
```

**Saída:**
```
Pontuação média:           90.0
Melhor pontuação (máximo): 120
Pior pontuação (mínimo):   60
```

---

## Perguntas de consolidação

1. O que a inicialização de `maior` e `menor` com o primeiro elemento do vetor revela sobre a importância de ter um ponto de partida confiável? Por que começar com `0` para `menor` poderia ser um problema?

2. Descreva como o processo de percorrer `[80, 100, 60, 120]` e chegar ao resumo (Média: 90, Máx.: 120, Mín.: 60) se conecta com a ideia de "destilar" informação útil a partir de dados brutos.

3. Este algoritmo tem complexidade **O(n)**. Se usássemos um algoritmo **O(n²)** para a mesma análise com 1 milhão de pontuações, quantos passos seriam necessários? O que isso diz sobre a importância de escolher o algoritmo certo para o trabalho?
