## Análise de sistemas

```text
1. ANÁLISE DE SISTEMAS
[ ] Papel da Análise no CICLO DE VIDA do software
[ ] Requisitos de negócio (O QUE fazer)
    x solução técnica (COMO construir)
```

```text
 NEGÓCIO                ANÁLISE                 TÉCNICA
 "o que precisa"  --->  (ponte, traduz)  --->  "como construir"
 requisitos             modelos, regras         projeto, código

 ciclo de vida:  levantar -> ANALISAR -> projetar -> codificar
                 -> testar -> implantar -> manter
```

---

## Modelos ágeis

```text
2. MODELOS ÁGEIS
[ ] Princípios: ciclos curtos, entregas frequentes,
    feedback contínuo do cliente, equipes
    multifuncionais, ACEITA mudanças
[ ] Ágil x tradicional (cascata)
[ ] Entregar incrementos a usuários reais
    REDUZ o risco de um projeto incerto
```

---

## Ágil x cascata

```text
 CASCATA                         ÁGIL (ciclos curtos)
 requisitos                      [plan->faz->entrega->feedback]
    |                            [plan->faz->entrega->feedback]
    v                            [plan->faz->entrega->feedback]
 projeto                              ...  cada volta = incremento
    |
    v
 código  -> testes -> entrega única (no fim)

 Cascata: planeja tudo antes; mudar é caro; cliente vê no final
 Ágil:    entrega aos poucos; muda no meio; cliente vê sempre
```

```text
Projeto INCERTO (ninguém sabe se vai funcionar)?
  -> incremento pequeno + usuário real + feedback
  -> descobre o erro cedo, gasta pouco para corrigir
```

---

## Scrum: papéis

```text
3. SCRUM
[ ] PAPÉIS: PO, Scrum Master, Time de Desenv.
    e a responsabilidade de cada um
    (inclusive remover impedimentos)

PRODUCT OWNER   dono do Backlog; maximiza o VALOR
SCRUM MASTER    facilita o Scrum; REMOVE IMPEDIMENTOS
TIME DE DESENV. multifuncional; cria o INCREMENTO
```

```text
 Stakeholders --> [ PO ]  Product Backlog (prioriza)
                    |
 [ SCRUM MASTER ] --+-- ajuda a equipe, tira bloqueios
                    |
              [ TIME DE DESENVOLVIMENTO ] --> INCREMENTO
```

---

## Scrum: eventos e artefatos

```text
[ ] EVENTOS e objetivo de cada um
[ ] ARTEFATOS: Product Backlog, Sprint Backlog, Incremento

SPRINT PLANNING  o que entra na Sprint e como fazer
DAILY SCRUM      15 min: sincronizar, achar impedimentos
SPRINT REVIEW    mostrar o incremento, colher feedback
SPRINT RETRO     como melhorar o PROCESSO da equipe
```

```text
 Product Backlog --Planning--> Sprint Backlog
                                   |   (Sprint: 1-4 sem.)
                         Daily  Daily  Daily ...
                                   v
                              INCREMENTO --> Review --> Retro
                                   |__________________|
                                      próxima Sprint
```

---

## Kanban

```text
[ ] Kanban e a ideia de LIMITAR o trabalho em andamento (WIP)
```

```text
 A FAZER      | FAZENDO (limite 2) | FEITO
 -------------+--------------------+--------
 [tarefa D]   | [tarefa B]         | [tarefa A]
 [tarefa E]   | [tarefa C]         |
 [tarefa F]   |   (cheio: termina antes de puxar outra)

 limitar o WIP -> menos coisas começadas e não terminadas;
                  o gargalo fica visível
```

---

## Gestão de mudanças

```text
4. GESTÃO DE MUDANÇAS
[ ] TODA mudança afeta ESCOPO, CRONOGRAMA e CUSTO
    -> exige ANÁLISE DE IMPACTO antes
[ ] Fluxo: registro formal com ID único -> análise
    -> decisão do CCB -> atualizar documentação
[ ] SCOPE CREEP: o que é e por que é risco

SCOPE CREEP = escopo que cresce sem controle,
              sem análise nem aprovação
              (pedidos "pequenos" que se acumulam)
Risco: estoura prazo e custo, perde-se o foco
```

---

## Fluxo da mudança (CCB)

```text
 Solicitação  --->  REGISTRO formal  --->  ANÁLISE DE IMPACTO
 de mudança         (ID único)              escopo? prazo? custo?
                                                   |
                                                   v
                                         CCB decide (Comitê de
                                         Controle de Mudanças)
                              +------------+-----------+
                              v            v           v
                          APROVA        REJEITA      ADIA
                              |
                              v
                       IMPLEMENTA  ->  ATUALIZA a documentação
```

---

## UML: caso de uso

```text
5. UML — DIAGRAMA DE CASO DE USO
[ ] Identificar ATORES, CASOS DE USO, LIMITE do
    sistema e ASSOCIAÇÕES
[ ] Como cada elemento é desenhado

ATOR       boneco (fica FORA do limite)
CASO DE USO  elipse com verbo (ação do sistema)
LIMITE       retângulo que envolve os casos de uso
ASSOCIAÇÃO   linha ligando ator ao caso de uso
```

---

## Caso de uso: exemplo

```text
              +--------- Caixa Eletrônico ----------+
              |                                     |
   O          |        (  Sacar dinheiro  )         |
  /|\ ---------------->                             |
  / \         |        (  Consultar saldo )         |
 Cliente      |                                     |
              |        (  Repor cédulas   )  <------------ O
              |                                     |     /|\
              +-------------------------------------+     / \
                                                       Técnico

 ator = fora do retângulo | caso de uso = elipse | linha = associação
```

---

## UML: classes

```text
6. UML — DIAGRAMA DE CLASSES
[ ] Classe: atributos e métodos
[ ] Herança e MULTIPLICIDADE
      1 | 0..1 | 0..* | 1..*
[ ] Associação x AGREGAÇÃO x COMPOSIÇÃO + exemplo
```

```text
 +-----------------+
 |     Animal      |   <- nome da classe
 +-----------------+
 | - nome: String  |   <- atributos
 +-----------------+
 | + comer(): void |   <- métodos
 +-----------------+
         ^
         |  herança (triângulo vazado aponta p/ a classe-mãe)
 +-----------------+
 |      Cão        |
 +-----------------+
```

---

## Associação, agregação, composição

```text
 ASSOCIAÇÃO   Professor ---------- Turma      (se relacionam)

 AGREGAÇÃO    Time ◇----------- Jogador       (todo-parte FRACA:
              1        0..*                     jogador existe sem o time)

 COMPOSIÇÃO   Pedido ◆--------- ItemPedido    (todo-parte FORTE:
              1        1..*                     sem o pedido, o item
                                                não existe)
```

```text
◇ losango VAZIO = agregação  (parte vive sozinha)
◆ losango CHEIO = composição (parte morre com o todo)
Justificar sempre: "a parte existe SEM o todo?"
```

---

## UML: diagrama de estados

```text
7. UML — DIAGRAMA DE ESTADOS
[ ] Estados, estado inicial, estado final,
    eventos e transições
[ ] Diferença: EVENTO x AÇÃO x ESTADO

ESTADO     situação em que o objeto PERMANECE
EVENTO     algo que ACONTECE e dispara a transição
AÇÃO       o que é executado ao transitar/entrar
```

```text
 (●) --abrir--> [ Aberto ] --atribuir--> [ Em atendimento ]
                                              |
                                          resolver
                                              v
                      [ Fechado ] <--confirmar-- [ Resolvido ]
                          |
                         (◉)  estado final

 (●) estado inicial   [ ] estado   --evento--> transição   (◉) final
```

---

## Exercícios 1 (UML)

```text
EXERCÍCIOS (caderno; depois compare)

[ ] Biblioteca online: DIAGRAMA DE CASO DE USO com
    ≥ 2 atores, ≥ 4 casos de uso e o limite do sistema.
[ ] Mesmo sistema: DIAGRAMA DE CLASSES (Livro, Usuário,
    Empréstimo...) com atributos, métodos,
    multiplicidades e ≥ 1 agregação ou composição.
[ ] DIAGRAMA DE ESTADOS de um pedido de e-commerce
    (aguardando pagamento, pago, enviado, entregue,
    cancelado) com os eventos de cada transição.
```

---

## Gabarito — Exercícios 1 (UML)

```text
CASO DE USO                  +--------- Biblioteca ----------+
 Usuário  ------------------>|  (Pesquisar livro)            |
 Usuário  ------------------>|  (Emprestar livro)            |
 Usuário  ------------------>|  (Devolver livro)             |
 Bibliotecário -------------->|  (Cadastrar livro)           |
 Bibliotecário -------------->|  (Aplicar multa)             |
                             +-------------------------------+

CLASSES
 Usuário 1 ------ 0..* Empréstimo 0..* ------ 1 Livro
 Empréstimo: dataRetirada, dataDevolução ; renovar(), devolver()
 Biblioteca ◆---- 1..* Livro     (composição: sem a biblioteca, o acervo não existe)
 (ou Biblioteca ◇---- Usuário: agregação)

ESTADOS DO PEDIDO
 (●)--criar--> [Aguardando pagamento] --pagar--> [Pago] --despachar--> [Enviado]
                    |                              |                      |
                 cancelar                       cancelar               entregar
                    v                              v                      v
               [Cancelado]                    [Cancelado]            [Entregue] --> (◉)
```

---

## Exercícios 2 (Scrum e backlog)

```text
[ ] 5 HISTÓRIAS DE USUÁRIO para um app à sua escolha;
    ordene num Product Backlog.
      "Como <quem>, quero <o quê>, para <por quê>"
[ ] Simule UMA SPRINT de 1 semana: o que acontece na
    Planning, Dailies, Review e Retrospective.
[ ] Tabela: papéis do Scrum + responsabilidade + 3
    situações em que cada papel deve agir.
```

---

## Gabarito — Exercícios 2 (Scrum e backlog) (1/2)

```text
PRODUCT BACKLOG (app da biblioteca escolar), em ordem de valor

1. Como aluno, quero buscar livros pelo título,
   para saber se há exemplares.
2. Como bibliotecário, quero registrar empréstimos,
   para controlar quem está com cada livro.
3. Como aluno, quero reservar um livro,
   para garanti-lo antes de ir à escola.
4. Como aluno, quero receber aviso de devolução,
   para evitar multa.
5. Como bibliotecário, quero um relatório de atrasos,
   para cobrar as devoluções.
```

---

## Gabarito — Exercícios 2 (Scrum e backlog) (2/2)

```text
SPRINT DE 1 SEMANA
Planning (seg)  PO apresenta os itens 1 e 2; o time estima
                e escolhe o que cabe -> Sprint Backlog.
Daily (ter-sex) 15 min: o que fiz, o que farei, impedimentos.
                (Scrum Master remove os impedimentos)
Review (sex)    time mostra o incremento funcionando (busca
                + empréstimo); PO e usuários dão feedback.
Retro (sex)     o que foi bem? o que melhorar? 1 ação para
                a próxima Sprint.
```

```text
Papel          | Responsabilidade            | Age quando...
Product Owner  | Backlog, prioridade, valor  | stakeholder muda a prioridade;
               |                             | dúvida sobre requisito; aceita item
Scrum Master   | facilita, tira impedimentos | servidor de testes cai; conflito
               |                             | na equipe; evento sem foco
Time Desenv.   | cria o incremento           | estima, programa, testa, entrega
```

---

## Exercícios 3 (mudança e comparação)

```text
[ ] Escreva uma SOLICITAÇÃO DE MUDANÇA fictícia e
    descreva os passos até a aprovação pelo CCB,
    indicando o impacto em ESCOPO, PRAZO e CUSTO.
[ ] Parágrafo: desenvolvimento ÁGIL x modelo CASCATA.
```

---

## Gabarito — Exercícios 3 (mudança e comparação)

```text
SM-014 | Pedido: adicionar pagamento por Pix no app
Impacto: escopo +1 módulo | prazo +2 semanas | custo +R$ 6.000
Fluxo: registrar (SM-014) -> analisar impacto -> CCB aprova/rejeita/adia
       -> implementar -> atualizar documentos (requisitos, cronograma, custo)
```

**Parágrafo (ágil × cascata):** No modelo em cascata, as etapas (requisitos, projeto, código, testes e entrega) acontecem em sequência e o cliente só vê o produto no final, então mudar é caro. No desenvolvimento ágil, o software é entregue em ciclos curtos, com feedback contínuo do cliente e aceitação de mudanças, o que reduz o risco quando os requisitos são incertos.

---
