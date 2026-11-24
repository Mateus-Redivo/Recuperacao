## Fundamentos de Python

```text
1. FUNDAMENTOS DE PYTHON
[ ] Variáveis, tipos de dados, função print
[ ] Operadores aritméticos (+ - * / // %) e de
    comparação; ORDEM em que são avaliados
```

```python
idade = 15         # int        nome = "Ana"   # str
altura = 1.62      # float      ativo = True   # bool

 7 + 2 = 9    7 - 2 = 5    7 * 2 = 14
 7 / 2 = 3.5  (divisão real)
 7 // 2 = 3   (divisão inteira)
 7 % 2 = 1    (resto)

 2 + 3 * 4   -> 14     (* antes de +)
 (2 + 3) * 4 -> 20     (parênteses primeiro)
 2 + 3 > 4   -> True   (aritmética ANTES da comparação)
 == igual   != diferente   > < >= <=
```

---

## Listas

```text
2. LISTAS
[ ] Acessar por índice, inclusive negativo (lista[-1])
[ ] len() e percorrer a lista com for
```

```python
cores = ["azul", "verde", "rosa", "preto", "roxo"]

 índice    0       1        2       3        4
        +-------+--------+-------+--------+-------+
        | azul  | verde  | rosa  | preto  | roxo  |
        +-------+--------+-------+--------+-------+
 negativo  -5      -4       -3      -2       -1

 cores[0] -> azul     cores[-1] -> roxo
 cores[-2] -> preto   len(cores) -> 5   (último índice = 4)

 for c in cores:
     print(c)
```

---

## Estruturas condicionais

```text
3. CONDICIONAIS
[ ] if, elif, else; a INDENTAÇÃO delimita o bloco
[ ] n % 2 para testar par ou ímpar
```

```python
nota = 6.5
if nota >= 7:
    print("aprovado")
elif nota >= 5:
    print("recuperação")      # <- este
else:
    print("reprovado")

n = 9
if n % 2 == 0:       # resto 0 -> par
    print("par")
else:
    print("ímpar")   # <- este
```

---

## Repetição: for e range

```text
4. REPETIÇÃO
[ ] for com range(início, fim, passo):
    o valor FINAL não é incluído
[ ] Acumuladores e contadores:
    total += n     c += 1
```

```python
range(5)         -> 0 1 2 3 4
range(2, 7)      -> 2 3 4 5 6        (7 fica de fora)
range(0, 10, 3)  -> 0 3 6 9

total = 0         # acumulador
c = 0             # contador
for n in [4, 7, 10]:
    total += n
    c += 1
print(total, c)   # 21 3
```

---

## while, break e laço infinito

```text
[ ] while, condição de parada, break;
    reconhecer LAÇO INFINITO

while repete ENQUANTO a condição for verdadeira
=> alguma coisa dentro do laço precisa MUDAR a condição
```

```python
n = 3
while n > 0:
    print(n)       # 3 2 1
    n -= 1
print("fim")

# INFINITO: esqueceu o n -= 1  (n > 0 nunca deixa de ser True)

while True:        # propositalmente infinito...
    s = input()
    if s == "sair":
        break      # ...até o break
```

---

## Funções (def, return, None)

```text
5. FUNÇÕES
[ ] def, parâmetros, return; return x print
[ ] Sem return -> devolve None (mesmo com print)
```

```python
def quadrado(x):
    return x * x       # DEVOLVE o valor

def mostra(x):
    print(x * x)       # só MOSTRA

a = quadrado(3)        # a vale 9
b = mostra(3)          # imprime 9 ... e b vale None
print(a, b)            # 9 None
```

---

## Valor padrão · return em laço

```text
[ ] Parâmetro com valor padrão: ORDEM e o que acontece
    quando o argumento é omitido
[ ] return dentro de um laço: a função TERMINA na
    1ª vez em que ele executa
```

```python
def saudacao(nome, msg="Olá"):       # padrão DEPOIS dos obrigatórios
    return msg + ", " + nome

saudacao("Ana")          # Olá, Ana       (usou o padrão)
saudacao("Ana", "Oi")    # Oi, Ana        (substituiu)
# def f(a=1, b): ...     # ERRO de sintaxe

def soma(lista):
    t = 0
    for n in lista:
        t += n
        return t          # <- sai na 1ª volta!
soma([5, 6, 7])           # devolve 5, não 18
```

---

## Combinando chamadas

```text
[ ] Combinar chamadas: dobrar(aumentar(n))
    e usar o resultado em outra expressão

Regra: resolve de DENTRO para FORA.
```

```python
def aumentar(v):
    return v + 2
def dobrar(v):
    return v * 2

dobrar(aumentar(4))      # aumentar(4) = 6  ->  dobrar(6) = 12
aumentar(dobrar(4)) + 1  # dobrar(4) = 8 -> aumentar(8) = 10 -> +1 = 11
```

---

## Escopo de variáveis

```text
6. ESCOPO
[ ] Local x global; quando precisa de `global`
[ ] LER global dentro da função x MODIFICAR
[ ] Prever o valor da global após várias chamadas
```

```python
total = 0                 # global

def mostra():
    print(total)          # só LER: funciona sem global

def soma(n):
    global total          # para MODIFICAR: precisa de global
    total += n

soma(5)
soma(3)
mostra()                  # 8

def f():
    y = 1                 # local: só existe dentro de f
f()
# print(y)  -> erro: y não existe aqui fora
```

---

## Teste de mesa

```text
7. TESTE DE MESA
[ ] Acompanhar o valor de cada variável LINHA A LINHA
    para prever a saída sem executar
```

```python
s = 0
for i in range(1, 5):
    if i % 2 == 0:
        s += i
print(s)
```
```text
 i | i % 2 == 0 |  s
---+------------+----
 - |     -      |  0     (início)
 1 |   Falso    |  0
 2 |  Verdadeiro|  2
 3 |   Falso    |  2
 4 |  Verdadeiro|  6
 saída: 6
```

---

## Exercícios 1 (teste de mesa · soma_pares · conta)

```text
EXERCÍCIOS (caderno/computador; depois confira)

[ ] Escolha 3 códigos com for/while; faça o teste de
    mesa no papel; depois confira no Python.
[ ] soma_pares(lista): soma dos pares. Depois mova o
    return para DENTRO do for, rode e explique por que
    o resultado muda.
[ ] conta(lista, alvo): quantas vezes o alvo aparece,
    SEM usar count().
```

---

## Gabarito — Exercícios 1 (teste de mesa · soma_pares · conta)

Três códigos para o teste de mesa (saídas: `0 2 4`; `4`; `7`):
```python
for i in range(3): print(i * 2)

n = 10; c = 0
while n > 0:
    n -= 3; c += 1
print(c)

t = 0
for x in [1, 2, 3, 4]:
    if x > 2: t += x
print(t)
```
```python
def soma_pares(lista):
    total = 0
    for n in lista:
        if n % 2 == 0:
            total += n
    return total          # fora do for

# return dentro do for: para na 1ª volta (soma só o 1º elemento, se for par,
# ou devolve 0 se for ímpar)

def conta(lista, alvo):
    c = 0
    for x in lista:
        if x == alvo:
            c += 1
    return c
```

---

## Exercícios 2 (maior/menor · média · preço)

```text
[ ] maior(lista) e menor(lista) SEM max()/min()
[ ] media(lista); depois versão com parâmetro padrão
    casas=2 para arredondar
[ ] preco_final(valor, desconto=10): chame COM e SEM o
    2º argumento, prevendo o resultado antes
```

---

## Gabarito — Exercícios 2 (maior/menor · média · preço)

```python
def maior(lista):
    m = lista[0]
    for x in lista:
        if x > m:
            m = x
    return m            # menor: troque > por <

def media(lista, casas=2):
    return round(sum(lista) / len(lista), casas)

def preco_final(valor, desconto=10):
    return valor - valor * desconto / 100

preco_final(100)        # 90.0
preco_final(100, 25)    # 75.0
```

---

## Exercícios 3 (global · índices · range)

```text
[ ] Contador GLOBAL incrementado por uma função com
    `global`: chame várias vezes e preveja o print.
[ ] letras = ['p','y','t','h','o','n']
    preveja letras[0], letras[-1], letras[-4].
    O que geram range(0, 10, 2) e range(1, 10, 3)?
```

---

## Gabarito — Exercícios 3 (global · índices · range)

```python
cont = 0
def inc():
    global cont
    cont += 1
inc(); inc(); inc()
print(cont)     # 3
```
`letras[0]` = 'p' · `letras[-1]` = 'n' · `letras[-4]` = 't'
`range(0, 10, 2)` → 0 2 4 6 8 · `range(1, 10, 3)` → 1 4 7

---

## Exercícios 4 (for ↔ while · pares/ímpares)

```text
[ ] Reescreva um for como while e um while como for,
    mantendo o mesmo resultado.
[ ] Programa que percorra uma lista e mostre a SOMA
    dos pares e a QUANTIDADE de ímpares.
```

---

## Gabarito — Exercícios 4 (for ↔ while · pares/ímpares)

```python
# for -> while
for i in range(1, 4): print(i)
i = 1
while i < 4:
    print(i); i += 1

# soma dos pares + qtd de ímpares
soma = 0; qtd = 0
for n in [8, 3, 6, 5, 7]:
    if n % 2 == 0: soma += n
    else:          qtd += 1
print(soma, qtd)       # 14 3
```

---

