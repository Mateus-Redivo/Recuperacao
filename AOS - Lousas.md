## SOA

```text
1. ARQUITETURA ORIENTADA A SERVIÇOS (SOA)

[ ] SOA x monolito: vantagens e custos de cada
[ ] O que é um serviço? Papel do CONTRATO
[ ] Serviços x outras integrações
      (arquivos, BD compartilhado, biblioteca comum)
[ ] Regra repetida em vários sistemas
      -> quando vira serviço reutilizável?
[ ] Desafios: latência de rede, monitoramento,
      testes de integração, consistência dos dados
```

```text
 MONOLITO                      SOA
+----------------+     +------+ +---------+ +---------+
| Vendas         |     | Loja | | Estoque | | Entrega |
| Estoque        |     +--+---+ +----+----+ +----+----+
| Entrega        |        |          |           |
| (1 código,     |   =====+==========+===========+=====
|  1 banco)      |       chamadas pela REDE (contrato)
+----------------+
+ simples, rápido            + evolui/escala por partes
- tudo sobe junto            - rede, monitorar, testar
```

---

## Serviço e contrato

```text
SERVIÇO = funcionalidade de negócio exposta pela rede
CONTRATO = o que ENTRA, o que SAI, quais ERROS
  -> quem usa não precisa saber como foi feito por dentro

Regra repetida em 3 sistemas?
  mudou a regra = mudar 3 códigos (e errar em 1)
  -> vira SERVIÇO: escrita 1 vez, reutilizada
```

```text
 Loja ----- {cep, peso} ------+
 Entrega -- {cep, peso} ------+--> [ SERVIÇO DE FRETE ]
 Pedidos -- {cep, peso} ------+     (regra escrita 1 vez)
                                         |
 Loja <------ {valor, prazo} ------------+

 CONTRATO:  entrada {cep, peso}
            saída   {valor, prazo}
            erro    "CEP inválido"
```

---

## SOA x outras formas de integrar

```text
FORMAS DE INTEGRAR SISTEMAS

Forma             | Acoplamento      | Problema típico
------------------+------------------+------------------
Arquivos          | baixo            | atraso, formato
BD compartilhado  | ALTO             | mudou tabela,
                  |                  | quebrou todos
Biblioteca comum  | ALTO (versão)    | recompilar e
                  |                  | reimplantar todos
SERVIÇOS          | baixo (contrato) | rede, latência
```

---

## Desafios da SOA

```text
DESAFIOS DA SOA (o "custo" do monolito dividido)

1. LATÊNCIA DE REDE     chamada remota é mais lenta
2. MONITORAMENTO        muitos serviços para vigiar
3. TESTES DE INTEGRAÇÃO cada serviço OK, e juntos?
4. CONSISTÊNCIA         dados em vários lugares,
                        cada serviço com seu banco

Monolito:  + simples de operar   - escala tudo junto
SOA:       + escala/evolui solto - mais complexa
```

```text
 A --> B --> C --> D      se C cai, quem avisa?
       ^                  onde está o erro? (monitorar)
       latência soma a cada salto
```

---

## Computação em nuvem e infraestrutura

```text
2. NUVEM E INFRAESTRUTURA

[ ] Nuvem pública x infra própria (on-premises):
      custo, controle, escalabilidade, latência
[ ] Dados sensíveis + regulações (bancos, LGPD)
      -> escolha da infraestrutura

                 | NUVEM PÚBLICA  | ON-PREMISES
-----------------+----------------+----------------
Custo inicial    | baixo (aluga)  | alto (compra)
Escalabilidade   | rápida         | limitada
Controle         | do provedor    | TOTAL
Latência         | depende da rede| local, baixa
Dados sensíveis  | exige cuidado  | controle direto
```

---

## REST e APIs HTTP

```text
3. REST E APIs HTTP

[ ] Recursos, URLs; GET, POST, PUT, DELETE
[ ] API stateless; papel do token a cada requisição
[ ] Status: 200, 201, 204, 400, 404, 500
[ ] REST x SOAP/WSDL x filas de mensagens (assíncrono)

RECURSO = substantivo na URL   /clientes  /clientes/7
```

```text
Método  Ação        Exemplo             Status
GET     ler         GET /clientes/7     200 | 404
POST    criar       POST /clientes {..} 201 | 400
PUT     atualizar   PUT /clientes/7 {..}200 | 204 | 404
DELETE  remover     DELETE /clientes/7  204 | 404

 200 OK      201 Criado       204 Sem conteúdo
 400 Requisição inválida (erro do cliente)
 404 Não encontrado
 500 Erro no servidor (erro nosso)
```

---

## Stateless · REST x SOAP x filas

```text
STATELESS: cada requisição traz TUDO que o servidor precisa

 Req 1: GET /pedidos    + token --> servidor valida --> 200
 Req 2: GET /pedidos/5  + token --> servidor valida --> 200
                         ^
        servidor NÃO guarda "quem é você" entre as chamadas
```

```text
         | REST         | SOAP / WSDL   | FILA (assíncrono)
---------+--------------+---------------+-------------------
Formato  | JSON/HTTP    | XML (envelope)| mensagem
Contrato | URL+métodos  | WSDL (formal) | formato da msg
Resposta | na hora      | na hora       | depois (não espera)
Uso      | APIs web     | sistemas      | tarefas em segundo
         |              | corporativos  | plano, picos
```

---

## Padrão MVC

```text
4. PADRÃO MVC

[ ] Responsabilidade de Model, View e Controller
[ ] Caminho de "Salvar" pelas 3 camadas

MODEL      = dados + regras de negócio
VIEW       = o que o usuário vê (tela/resposta)
CONTROLLER = recebe a ação, aciona o Model,
             escolhe a View
```

```text
 Usuário clica [Salvar]
        |
        v
 +------------+  1) envia os dados   +---------+
 | CONTROLLER | -------------------> |  MODEL  |
 |            | <------------------- | (regras,|
 +-----+------+  2) resultado        |  dados) |
       |                             +---------+
       | 3) escolhe a tela
       v
 +------------+
 |    VIEW    |  "Cadastro salvo!"
 +------------+
```

---

## Spring Boot

```text
5. SPRING BOOT
[ ] @RestController @GetMapping @PostMapping
    @PathVariable @RequestBody
[ ] Resposta: método devolve OBJETO x devolve null
[ ] Validações no DTO + @Valid
[ ] @RestControllerAdvice + @ExceptionHandler
```

```java
@RestController
@RequestMapping("/produtos")
public class ProdutoController {

  @GetMapping("/{id}")                     // GET /produtos/5
  public Produto buscar(@PathVariable Long id) { ... }

  @PostMapping                             // POST /produtos
  public Produto criar(@RequestBody @Valid ProdutoDTO dto) { ... }
}
// devolve objeto -> 200 + JSON
// devolve null   -> 200 + corpo VAZIO (Spring não vira 404)
```

---

## Validação com @Valid

```java
public record ProdutoDTO(
    @NotBlank String nome,        // não pode ser vazio
    @Positive double preco,       // maior que zero
    @Min(0) int estoque           // não negativo
) {}

@PostMapping
public Produto criar(@RequestBody @Valid ProdutoDTO dto)
//                               ^^^^^^ sem @Valid, as regras
//                                      do DTO são ignoradas
```

```text
Bean Validation:  declara no DTO  (@NotBlank, @Positive...)
@Valid:           ATIVA no Controller
dado inválido  ->  400 (Requisição inválida)
```

---

## Exceções centralizadas

```java
@RestControllerAdvice
public class ErroHandler {

  @ExceptionHandler(ProdutoNaoEncontrado.class)
  public ResponseEntity<String> trata(ProdutoNaoEncontrado e) {
    return ResponseEntity.status(404).body(e.getMessage());
  }
}
// Service faz:  throw new ProdutoNaoEncontrado(id);
// Controller NÃO precisa de try/catch
```

```text
Service lança exceção ──> @RestControllerAdvice captura
                      ──> vira resposta HTTP (ex.: 404)
Vantagem: tratamento em UM lugar, Controller limpo
```

---

## Arquitetura em camadas

```text
6. CAMADAS

[ ] Controller / Service / Repository:
      responsabilidade e quem conhece quem
[ ] O que o JpaRepository oferece
      (inclusive consultas derivadas do nome)
[ ] Entidade x DTO

CONTROLLER  recebe/responde HTTP, usa DTO
SERVICE     regras de negócio
REPOSITORY  acesso ao banco
ENTIDADE    espelha a tabela    DTO  dados da API
```

```text
 Cliente HTTP -> CONTROLLER -> SERVICE -> REPOSITORY -> BANCO
                  (DTO)        (regras)   (Entidade)

 Controller conhece o Service
 Service conhece o Repository
 (ninguém "pula" camada; Repository não conhece Controller)

 interface ProdutoRepository extends JpaRepository<Produto, Long> {
     List<Produto> findByCategoria(String categoria); // derivada do nome
 }
 // já vem pronto: save, findById, findAll, deleteById
```

---

## Exercícios 1 (SOA)

```text
EXERCÍCIOS (caderno ou computador; depois compare)

[ ] Invente uma empresa com 3 sistemas (ex.: loja,
    estoque, entrega). Desenhe a troca por serviços:
    que serviços cada um expõe? Qual o contrato?

[ ] Tabela: monolito x SOA
    vantagens | desvantagens | quando usar cada um
```

---

## Gabarito — Exercícios 1 (SOA)

```text
 LOJA ---- consultaEstoque(item) ----> ESTOQUE
   |         contrato: {item} -> {qtd}
   +------ solicitaEntrega(pedido) --> ENTREGA
             contrato: {endereco, itens} -> {codigoRastreio, prazo}
 ESTOQUE expõe: consultaEstoque, baixaEstoque
 ENTREGA expõe: solicitaEntrega, rastreio
```

Tabela esperada: monolito = simples de implantar/testar/operar, mas escala e evolui tudo junto (bom para sistema pequeno/equipe pequena); SOA = escala e evolui por partes, reuso, mas rede, monitoramento e consistência (bom para vários sistemas/equipes e regras compartilhadas).

---

## Exercícios 2 (REST)

```text
[ ] Liste 5 endpoints REST para /clientes:
    método | URL | corpo da requisição | status esperado

[ ] Explique em até 5 linhas o caminho de um
    POST /clientes, da requisição à resposta.
```

---

## Gabarito — Exercícios 2 (REST)

```text
GET    /clientes        -            200
GET    /clientes/{id}   -            200 | 404
POST   /clientes        {nome,email} 201 | 400
PUT    /clientes/{id}   {nome,email} 200 | 404 | 400
DELETE /clientes/{id}   -            204 | 404
```

POST /clientes: requisição chega ao Controller → `@Valid` valida o DTO (400 se inválido) → Controller chama o Service → Service aplica as regras e chama o Repository → Repository grava no banco → volta pelo Service ao Controller → resposta 201 com o cliente criado.

---

## Exercícios 3 (Spring Boot)

```text
[ ] Crie em Spring Boot uma API de clientes em camadas
    (Controller, Service, Repository) com um DTO
    validado por @Valid.

[ ] Faça a API devolver 404 quando o cliente não
    existe, usando uma exceção tratada em um
    @RestControllerAdvice.
```

---

## Gabarito — Exercícios 3 (Spring Boot)

```java
public record ClienteDTO(@NotBlank String nome, @Email String email) {}

@Entity class Cliente { @Id @GeneratedValue Long id; String nome; String email; }

interface ClienteRepository extends JpaRepository<Cliente, Long> {}

@Service class ClienteService {
  private final ClienteRepository repo;
  ClienteService(ClienteRepository repo) { this.repo = repo; }
  Cliente buscar(Long id) {
    return repo.findById(id).orElseThrow(() -> new ClienteNaoEncontrado(id));
  }
  Cliente criar(ClienteDTO dto) { /* converte DTO -> entidade e salva */ }
}

@RestController @RequestMapping("/clientes")
class ClienteController {
  @GetMapping("/{id}") Cliente buscar(@PathVariable Long id) { return service.buscar(id); }
  @PostMapping Cliente criar(@RequestBody @Valid ClienteDTO dto) { return service.criar(dto); }
}

@RestControllerAdvice class ErroHandler {
  @ExceptionHandler(ClienteNaoEncontrado.class)
  ResponseEntity<String> trata(ClienteNaoEncontrado e) {
    return ResponseEntity.status(404).body(e.getMessage());
  }
}
```

---
