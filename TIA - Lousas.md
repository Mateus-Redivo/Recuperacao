## Fundamentos de IA

```text
1. FUNDAMENTOS DE IA
[ ] IA FRACA x IA FORTE (geral) x CONSCIÊNCIA
    artificial — com exemplos
[ ] Aplicações do dia a dia: recomendação em streaming,
    chatbots, imagens médicas, drones, agricultura
[ ] Sistema que APRENDE COM DADOS x sistema que
    segue REGRAS FIXAS
```

---

## IA fraca/forte · aprender x regras

```text
 IA FRACA (estreita)      IA FORTE (geral)       CONSCIÊNCIA
 faz UMA tarefa           faz qualquer tarefa    "sente", tem
 ex.: recomendar filme,   intelectual humana     experiência própria
 filtro de spam           (ainda não existe)     (hipotético)
 -> TODA a IA de hoje

 REGRAS FIXAS                     APRENDE COM DADOS
 se temp > 38 -> "febre"          exemplos -> modelo -> previsão
 (humano escreveu a regra)        (o padrão sai dos dados)
```

---

## Tipos de aprendizado de máquina

```text
2. TIPOS DE APRENDIZADO DE MÁQUINA
[ ] SUPERVISIONADO (classificação, regressão),
    NÃO SUPERVISIONADO (agrupamento, associação,
    anomalias) e POR REFORÇO
[ ] Escolher a abordagem para um problema
    (prever vendas / agrupar clientes / detectar fraude)
[ ] SÉRIES TEMPORAIS: padrões no tempo -> projetar futuro
```

```text
 SUPERVISIONADO  (tem RÓTULO / resposta certa)
    classificação -> categoria   (spam ou não)
    regressão     -> número      (preço da casa)
 NÃO SUPERVISIONADO  (sem rótulo)
    agrupamento (clusters) | associação (compra junto) | anomalias
 POR REFORÇO  agente + recompensa/punição, tentativa e erro
```

---

## Séries temporais · escolher a abordagem

```text
 vendas
   |        .        .
   |     .    .   .    .        padrão: sobe e desce todo
   |  .          .          ?    ano (sazonal) -> projetar
   +-------------------------> tempo (meses)
```

```text
Problema                          Abordagem
--------------------------------  -------------------------
prever número no tempo            série temporal / regressão
classificar em categorias         supervisionado (classif.)
agrupar sem rótulos               não sup. (agrupamento)
achar o que foge do normal        anomalias (ex.: fraude)
aprender jogando, com recompensa  por reforço
```

---

## Avaliação de modelos

```text
3. AVALIAÇÃO DE MODELOS
[ ] Divisão TREINO / TESTE e por que é necessária
[ ] ACURÁCIA — e por que ENGANA com classes
    muito desbalanceadas
[ ] MATRIZ DE CONFUSÃO, PRECISÃO e RECALL
[ ] OVERFITTING: o que é e como reduzir
```

```text
 dados --> [ 70% TREINO ] --> modelo aprende
      \--> [ 30% TESTE  ] --> modelo NUNCA viu; mede o desempenho
 (se testar com o que treinou, o modelo "decora" e a nota mente)
```

---

## Matriz de confusão, acurácia, precisão, recall

```text
                  PREVISTO
                Spam    Não spam
 REAL  Spam   |  40  |   10   |   VP = 40   FN = 10
 REAL  Não    |   5  |   45   |   FP = 5    VN = 45

 acurácia = (VP + VN) / total        = 85 / 100 = 0,85
 precisão = VP / (VP + FP)           = 40 / 45  ≈ 0,89
 recall   = VP / (VP + FN)           = 40 / 50  = 0,80
```

```text
precisão: dos que EU disse "spam", quantos eram mesmo?
recall:   dos spams que EXISTEM, quantos eu achei?
```

---

## Acurácia que engana · overfitting

```text
 100 clientes: 98 ficam, 2 cancelam
 modelo "ninguém cancela" -> acurácia 98 %   mas recall = 0 / 2 = 0
 => ACURÁCIA ENGANA com classes desbalanceadas;
    olhe precisão, recall, matriz de confusão

 OVERFITTING                 como reduzir
    erro                     + dados / dados variados
 teste ^   .--'              modelo mais simples
       |  /     treino ---   validação cruzada, parar cedo
       +------------------>  regularização
          complexidade       (treino ótimo, teste ruim = decorou)
```

---

## Mineração de dados: desafios e limitações

```text
4. MINERAÇÃO DE DADOS: DESAFIOS
[ ] Qualidade dos dados, overfitting, interpretabilidade
    ("caixa preta"), privacidade (LGPD e GDPR)
[ ] SISTEMAS ESPECIALISTAS e o problema da
    AQUISIÇÃO DE CONHECIMENTO

Desafio            | Como reduzir
-------------------+----------------------------------
Qualidade de dados | limpar, tratar nulos, validar
Overfitting        | mais dados, modelo mais simples
Caixa preta        | modelos interpretáveis, explicações
Privacidade        | anonimizar, consentimento, LGPD
Sist. especialista | difícil extrair e manter a regra
                   | do especialista humano (aquisição)
```

---

## Ética em sistemas autônomos

```text
5. ÉTICA EM SISTEMAS AUTÔNOMOS
[ ] Decisões CRÍTICAS (ex.: carros inteligentes) e a
    necessidade de REGRAS ÉTICAS
[ ] Responsabilidade, transparência e VIÉS na IA

DILEMA: o carro autônomo precisa escolher entre
        dois males inevitáveis. Quem decide? Qual regra?

 RESPONSABILIDADE  quem responde? fabricante, dono, programador?
 TRANSPARÊNCIA     dá para explicar a decisão?
 VIÉS              dados enviesados -> decisões injustas
```

---

## Dashboards e ferramentas

```text
6. DASHBOARDS E FERRAMENTAS
[ ] Categorias: COM CÓDIGO (Streamlit, Python) e
    NO-CODE / LOW-CODE (Tableau)
[ ] Público e contexto de cada tipo

             | COM CÓDIGO       | NO-CODE / LOW-CODE
-------------+------------------+--------------------
Exemplo      | Streamlit        | Tableau
Quem usa     | quem programa    | analista/negócio
Flexibilidade| altíssima        | limitada ao que oferece
Velocidade   | exige programar  | arrasta e solta
Contexto     | integrar modelo  | relatórios rápidos
             | de IA, app sob   | para gestão
             | medida           |
```

---

## Do modelo à produção (deploy)

```text
7. DO MODELO À PRODUÇÃO
[ ] Salvar e carregar modelo treinado (Joblib)
[ ] Por que boa acurácia no teste AINDA exige
    interface e acompanhamento depois do deploy
[ ] DATA DRIFT: o que é e por que o desempenho cai
```

```python
import joblib

joblib.dump(modelo, "modelo.joblib")        # salvar (arquivo 1)

modelo = joblib.load("modelo.joblib")       # carregar (arquivo 2)
modelo.predict([[5.1, 3.5, 1.4, 0.2]])      # fazer previsão

# só carregue .joblib de fonte confiável
```

---

## Data drift · ciclo pós-deploy

```text
 treino/teste (dados de ONTEM) --> modelo bom (acurácia ok)
                                        |
                                    DEPLOY
                                        v
 usuários + dados NOVOS (hoje) -> o mundo muda -> DATA DRIFT
                                        |
 desempenho cai ... -> monitorar -> re-treinar -> novo deploy
                                        ^_________________|

 Precisa também de INTERFACE (dashboard/app) para as pessoas usarem
```

---

## Exercícios 1 (IA e tipos de aprendizado)

```text
EXERCÍCIOS (caderno ou computador; depois compare)

[ ] Liste 10 aplicações de IA do seu dia a dia e
    classifique cada uma como IA FRACA ou FORTE,
    justificando.
[ ] Tipo de aprendizado mais adequado, e por quê:
      - prever vendas do próximo mês
      - separar e-mails em spam ou não
      - agrupar clientes por perfil de compra
      - ensinar um robô a jogar
```

---

## Gabarito — Exercícios 1 (IA e tipos de aprendizado)

Todas as aplicações do dia a dia são IA **fraca** (fazem uma tarefa específica); IA forte/geral não existe hoje.
- prever vendas → supervisionado (regressão) / série temporal
- spam ou não → supervisionado (classificação)
- agrupar clientes → não supervisionado (agrupamento)
- robô que joga → por reforço

---

## Exercícios 2 (métricas)

```text
[ ] Invente uma MATRIZ DE CONFUSÃO; calcule acurácia,
    precisão e recall e comente.
[ ] Explique por que um modelo que "prevê que ninguém
    cancela" pode ter 95% de acurácia e ainda assim
    ser INÚTIL.
```

---

## Gabarito — Exercícios 2 (métricas)

```text
MATRIZ (exemplo)      PREVISTO
                   Sim      Não
 REAL  Sim       |  30  |   20   |   VP = 30  FN = 20
 REAL  Não       |  10  |   40   |   FP = 10  VN = 40

 acurácia = (30 + 40) / 100 = 0,70
 precisão = 30 / (30 + 10)  = 0,75
 recall   = 30 / (30 + 20)  = 0,60
 -> acerta 70%, mas deixa escapar 40% dos casos positivos
```

Exemplo: 100 clientes, 5 cancelam. O modelo diz "ninguém cancela": acerta 95 → acurácia 95%, mas encontra **0 dos 5** que cancelam (recall = 0/5 = 0) e não tem nenhuma previsão positiva. A acurácia engana porque a classe "cancela" é rara; o modelo não cumpre a função (identificar quem vai cancelar). Por isso olhamos matriz de confusão, precisão e recall.

---

## Exercícios 3 (código)

```text
[ ] Treine um modelo simples (scikit-learn), separando
    TREINO e TESTE, e meça a acurácia.
[ ] Salve com joblib, carregue em OUTRO arquivo e
    faça uma previsão.
[ ] Dashboard simples com Streamlit (ou outra) com
    ao menos 2 GRÁFICOS.
```

---

## Gabarito — Exercícios 3 (código)

```python
# treino.py
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
import joblib

X, y = load_iris(return_X_y=True)
Xtr, Xte, ytr, yte = train_test_split(X, y, test_size=0.3, random_state=42)
modelo = DecisionTreeClassifier().fit(Xtr, ytr)
print(accuracy_score(yte, modelo.predict(Xte)))
joblib.dump(modelo, "modelo.joblib")

# uso.py
import joblib
modelo = joblib.load("modelo.joblib")
print(modelo.predict([[5.1, 3.5, 1.4, 0.2]]))

# painel.py  ->  streamlit run painel.py
import streamlit as st, pandas as pd
df = pd.DataFrame({"mes": ["Jan", "Fev", "Mar"],
                   "vendas": [10, 14, 9], "custos": [6, 7, 8]}).set_index("mes")
st.title("Painel de vendas")
st.line_chart(df["vendas"])
st.bar_chart(df["custos"])
```

---

## Exercícios 4 (ética e desafios)

```text
[ ] Parágrafo sobre um DILEMA ÉTICO de um carro
    autônomo e quais REGRAS deveriam orientar a decisão.
[ ] Escolha 2 desafios da mineração de dados
    (ex.: qualidade dos dados e privacidade) e proponha
    como REDUZIR cada um.
```

---

## Gabarito — Exercícios 4 (ética e desafios)

Dilema: o carro não consegue evitar o acidente e precisa escolher quem proteger; regras: prioridade à vida, não discriminar (viés), transparência sobre a regra usada, responsabilidade definida (fabricante/operador), supervisão humana quando possível.
Desafios: qualidade dos dados → limpeza, validação, tratamento de nulos/duplicados; privacidade → anonimização, consentimento, coletar só o necessário (LGPD/GDPR).

---
