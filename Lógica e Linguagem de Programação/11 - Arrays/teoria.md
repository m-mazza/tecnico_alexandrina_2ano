# Lógica e Linguagem de Programação
**Semana 11 - Assunto: Arrays**

---

# O problema de muitas variáveis
Na desenvolvimento de software, muitas vezes precisamos manipular uma grande massa de dados. Abaixo, há um exemplo:

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

O Código não parece ser muito eficente, certo? E se houver um 41 aluno?

## Vetores
Uma coleção de dados é chamado de vetor ou array ou arranjo