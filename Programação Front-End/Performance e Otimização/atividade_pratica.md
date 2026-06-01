# Atividade Prática — Introdução à Performance Web

**Nome:** _____________________________________________ **Turma:** ___________

---

## Contexto

Você foi contratado como estagiário em uma pequena empresa de tecnologia. Seu supervisor pediu que você analise por que o site da empresa demora para carregar e sugira melhorias simples.

Nesta atividade, você vai **observar, identificar e propor soluções** para problemas de performance — sem precisar programar do zero.

---

## Parte 1 — Conhecendo as ferramentas (sem código)

**Objetivo:** Aprender a usar o Google Lighthouse para analisar um site real.

### Passo a passo

1. Abra o **Google Chrome** e acesse qualquer site de sua escolha (ex.: o site da sua escola ou uma loja online simples).
2. Pressione **F12** para abrir o Chrome DevTools.
3. Clique na aba **Lighthouse** (caso não apareça, clique na seta `>>` para encontrá-la).
4. Selecione apenas a categoria **Performance**.
5. Escolha o dispositivo **Mobile**.
6. Clique em **Analyze Page Load** e aguarde o relatório ser gerado.

### O que observar no relatório

Após a análise, preencha a tabela abaixo com os valores que o Lighthouse exibir:

| Métrica | O que mede | Valor obtido |
|---|---|---|
| First Contentful Paint (FCP) | Tempo até o primeiro conteúdo aparecer | |
| Largest Contentful Paint (LCP) | Tempo até o maior elemento carregar | |
| Total Blocking Time (TBT) | Tempo bloqueado por scripts pesados | |
| Cumulative Layout Shift (CLS) | Elementos que se moveram na tela | |

**Pontuação geral de Performance:** _______

> 💡 **Dica:** Pontuações acima de 90 são consideradas boas. Entre 50 e 89 são medianas. Abaixo de 50, precisam de atenção.

---

## Parte 2 — Identificando problemas

**Objetivo:** Reconhecer situações comuns que deixam sites lentos.

Leia cada situação abaixo e marque qual técnica de otimização poderia resolver o problema:

| Situação-problema | Técnica que resolve |
|---|---|
| Um site tem 30 imagens grandes que carregam todas de uma vez, mesmo as que estão no fim da página | |
| Um arquivo JavaScript com 500 linhas de comentários e espaços desnecessários aumenta o tempo de download | |
| Uma lista com 10.000 nomes é renderizada inteira na tela, travando o navegador | |
| Um componente de botão é redesenhado toda vez que qualquer coisa na página muda, mesmo sem necessidade | |

**Opções:** Lazy Loading / Minificação / Virtualização de Listas / Memoization (React.memo)

---

## Parte 3 — Reflexão escrita

Responda com suas próprias palavras (2 a 4 linhas cada):

**1.** Por que um site lento pode prejudicar a experiência do usuário? Pense em situações do dia a dia.

```
___________________________________________________________________________
___________________________________________________________________________
___________________________________________________________________________
```

**2.** Explique com um exemplo prático o que é Lazy Loading. Você pode usar uma analogia do cotidiano.

```
___________________________________________________________________________
___________________________________________________________________________
___________________________________________________________________________
```

**3.** Qual a diferença entre analisar a performance com o **Lighthouse** e com a aba **Network** do DevTools?

```
___________________________________________________________________________
___________________________________________________________________________
___________________________________________________________________________
```

