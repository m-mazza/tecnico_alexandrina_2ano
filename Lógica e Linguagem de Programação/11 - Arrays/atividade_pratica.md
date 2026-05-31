# Lógica e Linguagem de Programação

**Semana 11 - Roteiro Atividade Prática**

---

## Arrays

Esta disciplina tem como objetivo introduzir os fundamentos do pensamento lógico aplicado à programação, capacitando o aluno a compreender estruturas de algoritmos e desenvolver habilidades práticas de codificação desde os primeiros contatos com a área.

As aulas combinam momentos teóricos com atividades práticas executadas em sala, garantindo que o aprendizado aconteça de forma ativa e progressiva.


# Exemplo de cálculo de média sem vetor

Neste exemplo, cada nota é armazenada em uma variável diferente.

```python
nota1 = float(input())
nota2 = float(input())
nota3 = float(input())
nota4 = float(input())
nota5 = float(input())
nota6 = float(input())
nota7 = float(input())
nota8 = float(input())
nota9 = float(input())
nota10 = float(input())
nota11 = float(input())
nota12 = float(input())
nota13 = float(input())
nota14 = float(input())
nota15 = float(input())
# ... e assim por diante até nota40

media = (
    nota1 + nota2 + nota3 + nota4 + nota5 +
    nota6 + nota7 + nota8 + nota9 + nota10 +
    nota11 + nota12 + nota13 + nota14 + nota15
    # + ... + nota40
) / 40

print("Média:", media)
```

> Observação: essa solução funciona, mas exige a criação de muitas variáveis. Em Python, geralmente utilizamos listas para armazenar grandes quantidades de dados semelhantes.
