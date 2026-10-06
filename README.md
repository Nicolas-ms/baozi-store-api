# Baozi Store — API REST

API REST desenvolvida para a disciplina de Desenvolvimento Web Back-End, representando
o controle básico de clientes, produtos e pedidos da Baozi Store, uma pequena loja de
pãozinho chinês.

## Tecnologias

- Java 25
- Spring Boot 4.1
- Spring Data JPA
- H2 (banco relacional em arquivo)
- Gradle

## Como executar

```bash
./gradlew bootRun
```

A API fica disponível em `http://localhost:8080`. O banco H2 é criado
automaticamente na pasta `data/`.

Console H2: `http://localhost:8080/h2-console`
(URL JDBC: `jdbc:h2:file:./data/baozi-store`, usuário `sa`, sem senha).

## Arquitetura

Padrão MVC do Spring:

- `com.baozistore.model` — entidades JPA
- `com.baozistore.repository` — repositórios (Spring Data JPA)
- `com.baozistore.controller` — controllers REST

## Entidades

### Cliente

| Campo         | Tipo       |
|---------------|------------|
| id            | Long       |
| nome          | String     |
| clienteDesde  | LocalDate  |

### Produto

| Campo   | Tipo       |
|---------|------------|
| id      | Long       |
| nome    | String     |
| preco   | BigDecimal |
| estoque | Boolean    |

### Pedido

| Campo       | Tipo    |
|-------------|---------|
| id          | Long    |
| clienteId   | Long    |
| produtoId   | Long    |
| quantidade  | Integer |

## Endpoints

Todos os recursos respondem em JSON.

### Clientes

| Método   | Rota             | Descrição            |
|----------|------------------|----------------------|
| POST     | /clientes        | Cadastrar cliente    |
| GET      | /clientes        | Listar todos         |
| GET      | /clientes/{id}   | Consultar por ID     |
| PUT      | /clientes/{id}   | Atualizar            |
| DELETE   | /clientes/{id}   | Apagar               |

### Produtos

| Método   | Rota             | Descrição            |
|----------|------------------|----------------------|
| POST     | /produtos        | Cadastrar produto    |
| GET      | /produtos        | Listar todos         |
| GET      | /produtos/{id}   | Consultar por ID     |
| PUT      | /produtos/{id}   | Atualizar            |
| DELETE   | /produtos/{id}   | Apagar               |

### Pedidos

| Método   | Rota             | Descrição            |
|----------|------------------|----------------------|
| POST     | /pedidos         | Registrar pedido     |
| GET      | /pedidos         | Listar todos         |
| GET      | /pedidos/{id}    | Consultar por ID     |
| PUT      | /pedidos/{id}    | Atualizar            |
| DELETE   | /pedidos/{id}    | Apagar               |

## Exemplos de requisição

```bash
curl -X POST http://localhost:8080/clientes \
  -H "Content-Type: application/json" \
  -d '{"nome":"NicolasRU","clienteDesde":"2026-10-06"}'

curl -X POST http://localhost:8080/produtos \
  -H "Content-Type: application/json" \
  -d '{"nome":"Paozinho Chines","preco":5.50,"estoque":true}'

curl -X POST http://localhost:8080/pedidos \
  -H "Content-Type: application/json" \
  -d '{"clienteId":1,"produtoId":1,"quantidade":10}'
```
