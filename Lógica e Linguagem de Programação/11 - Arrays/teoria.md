# Lógica e Linguagem de Programação
**Semana 11 - Assunto: Arrays**

# Vetores (Arrays Unidimensionais)

**Curso:** Técnico em Desenvolvimento de Sistemas — Educação Profissional Paulista  
**Aula:** Declaração e acesso a vetores

---

## O problema das muitas variáveis

Sem vetores, armazenar as notas de 40 alunos exigiria isso:

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

Código gigantesco, repetitivo e impossível de manter. É aí que entram os **vetores**.

---

## O que é um vetor?

Um **vetor** (também chamado de *array*) é uma estrutura de dados que armazena múltiplos valores do **mesmo tipo** sob um **único nome**, organizados sequencialmente na memória. Cada valor é identificado por sua posição, chamada de **índice**.

> 💡 Pense em um armário com gavetas numeradas: cada gaveta guarda um item e você acessa pelo número. Todas guardam o mesmo tipo de objeto.

---

## Características

- **Homogêneo:** todos os elementos são do mesmo tipo.
- **Acesso direto:** qualquer elemento é acessado diretamente pelo índice.
- **Alocação sequencial:** elementos ficam em posições consecutivas na memória.

---

## Indexação em Python (base 0)

Em Python, o primeiro índice é **0** e o último é **tamanho − 1**.

```
[ 8.5 | 7.0 | 9.5 | 6.0 | 8.0 ]
  [0]   [1]   [2]   [3]   [4]
```

---

## Vetores em Python

### Criando

```python
notas = []                        # vazio
notas = [8.5, 7.0, 9.5, 6.0, 8.0]  # com valores
votos = [0] * 5                   # cinco zeros
```

### Acessando e alterando

```python
notas = [8.5, 7.0, 9.5, 6.0, 8.0]

print(notas[0])   # 8.5 — primeiro
print(notas[-1])  # 8.0 — último

notas[1] = 7.5    # altera o segundo elemento
```

### Percorrendo com `for`

```python
notas = []
for i in range(5):
    nota = float(input(f"Nota do aluno {i + 1}: "))
    notas.append(nota)
```

### Calculando a média

```python
notas = [8.5, 7.0, 9.5, 6.0, 8.0]

soma = 0
for nota in notas:
    soma += nota

print(f"Média: {soma / len(notas):.2f}")  # 7.80
```

### Encontrando o maior valor

```python
notas = [8.5, 7.0, 9.5, 6.0, 8.0]

maior = notas[0]
for nota in notas:
    if nota > maior:
        maior = nota

print(f"Maior nota: {maior}")  # 9.5
```

---

## Exemplo prático: sistema de votação

```python
votos = [0] * 11  # índices 1 a 10 representam cada participante

for i in range(1, 11):
    while True:
        voto = int(input(f"Voto {i} (1 a 10): "))
        if 1 <= voto <= 10:
            votos[voto] += 1
            break
        print("Voto inválido!")

for p in range(1, 11):
    print(f"Participante {p:2d}: {votos[p]} voto(s)")
```

---

## Aula 2: Busca Linear

---

## O problema da busca manual

Imagine um sistema de estoque com 100 códigos de produtos. Sem busca linear, verificar se um código existe exigiria isso:

```python
codigo_procurado = 4587
produtos = [...]  # lista com 100 itens

if produtos[0] == codigo_procurado:
    print("Encontrado na posição 0")
elif produtos[1] == codigo_procurado:
    print("Encontrado na posição 1")
elif produtos[2] == codigo_procurado:
    print("Encontrado na posição 2")
# ... e assim por diante até produtos[99]!
```

100 estruturas `if/elif` aninhadas — impossível de manter. E se o vetor tivesse 1.000 ou 10.000 itens?

---

## O que é busca linear?

A **busca linear** (também chamada de busca sequencial) é o algoritmo mais simples de busca em estruturas de dados. Ela percorre cada elemento do vetor, um por um, comparando com o valor procurado, até encontrá-lo ou até esgotar todos os elementos.

Em vez de escrever 100 `if/elif`, usa-se um laço que percorre o vetor automaticamente.

---

## Como funciona a busca linear

- Começar no primeiro elemento do vetor (índice 0).
- Comparar o elemento atual com o valor procurado.
- Se forem iguais, retornar a posição e encerrar.
- Se não forem iguais, avançar para o próximo elemento.
- Repetir até encontrar ou até acabar o vetor.
- Se chegar ao fim sem encontrar, retornar `-1` (convenção em Python).

---

## Os três fundamentos da busca linear

### 1. Iteração (percorrendo)

Percorrer o vetor elemento por elemento usando um laço. No pior caso, se o vetor tem 100 elementos, haverá 100 iterações.

```python
numeros = [15, 42, 8, 23, 16, 4, 31]

for i in range(len(numeros)):
    print(numeros[i])  # examina cada elemento
```

### 2. Comparação (verificação)

Verificar se o elemento atual é igual ao valor procurado. É o "coração" do algoritmo — sem ela, não saberíamos se encontramos o que procuramos.

```python
numeros = [15, 42, 8, 23, 16, 4, 31]
valor_procurado = 23

for i in range(len(numeros)):
    if numeros[i] == valor_procurado:
        print("Encontrou!")
```

### 3. Retorno de posição (resultado)

Quando encontrado, retornar o índice. Se não encontrado, retornar `-1`.

```python
for i in range(len(numeros)):
    if numeros[i] == valor_procurado:
        posicao = i  # armazena a posição
        break        # para a busca imediatamente
```

> O `break` é essencial: sem ele, o laço continuaria percorrendo o vetor mesmo depois de achar o valor.

---

## Implementação completa da busca linear

```python
numeros = [15, 42, 8, 23, 16, 4, 31]

valor_procurado = int(input("Digite o valor a procurar: "))

encontrado = False
posicao = -1

for i in range(len(numeros)):
    if numeros[i] == valor_procurado:
        encontrado = True
        posicao = i
        break

if encontrado:
    print(f"Valor encontrado na posição: {posicao}")
else:
    print("Valor não encontrado no vetor.")
```

**Exemplo de saída:**
```
Digite o valor a procurar: 23
Valor encontrado na posição: 3
```

---

## Complexidade O(n)

A eficiência da busca linear está diretamente relacionada ao tamanho do vetor.

- **Melhor caso:** o valor está na primeira posição → 1 comparação.
- **Pior caso:** o valor não existe ou está no final → n comparações.
- **Conclusão:** dobrar o tamanho do vetor dobra o tempo de busca no pior caso.

```python
numeros = [15, 42, 8, 23, 16, 4, 31]
valor_procurado = 4
comparacoes = 0

for i in range(len(numeros)):
    comparacoes += 1
    if numeros[i] == valor_procurado:
        print(f"Encontrado na posição {i} após {comparacoes} comparação(ões).")
        break
else:
    print(f"Não encontrado após {comparacoes} comparação(ões).")
```

---

## 🐍 Funções nativas do Python usadas neste arquivo

### `input()`
Lê um valor digitado pelo usuário no terminal e retorna sempre uma **string**.
```python
nome = input("Digite seu nome: ")  # retorna string
```

### `float()`
Converte um valor para número decimal (ponto flutuante).
```python
nota = float("8.5")  # 8.5
nota = float(input("Digite a nota: "))  # lê e converte em uma linha
```

### `int()`
Converte um valor para número inteiro.
```python
voto = int("3")   # 3
voto = int(input("Digite o voto: "))  # lê e converte em uma linha
```

### `print()`
Exibe um valor ou mensagem no terminal.
```python
print("Olá!")           # texto simples
print(notas[0])         # valor de uma posição do vetor
print(f"Média: {7.80:.2f}")  # com f-string formatada
```

### `range()`
Gera uma sequência de números inteiros, muito usada em laços `for`.
```python
range(5)      # 0, 1, 2, 3, 4
range(1, 11)  # 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

### `len()`
Retorna o número de elementos de uma lista (tamanho do vetor).
```python
notas = [8.5, 7.0, 9.5]
print(len(notas))  # 3
```

### `.append()`
Método de lista que adiciona um elemento ao **final** do vetor.
```python
notas = []
notas.append(8.5)  # [8.5]
notas.append(7.0)  # [8.5, 7.0]
```

### `break`
Interrompe imediatamente o laço em execução. Essencial na busca linear para parar assim que o valor é encontrado.
```python
for i in range(len(numeros)):
    if numeros[i] == valor_procurado:
        break  # sai do laço imediatamente
```

---

## Resumo

- **Vetor:** múltiplos valores do mesmo tipo sob um único nome.
- **Índice:** posição do elemento (base 0 em Python).
- **Alocação sequencial:** elementos lado a lado na memória, acesso direto e imediato.
- **Laços + vetores:** combinação que torna o código simples e escalável.
- **Busca linear:** percorre o vetor elemento por elemento até encontrar o valor ou esgotar o vetor.
- **Complexidade O(n):** o tempo de busca cresce proporcionalmente ao tamanho do vetor.
