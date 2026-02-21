# Neo4j Dio - Desafios de Código e Projeto

Este repositório contém as soluções e modelagens desenvolvidas para os desafios de banco de dados em grafos utilizando **Neo4j**, realizados durante o bootcamp na plataforma DIO.

## 🚀 O Projeto: Modelagem de um Serviço de Streaming

O objetivo principal deste desafio foi simular a arquitetura de dados de uma plataforma como a Netflix, focando em conexões entre usuários, conteúdos e preferências.

### 🎥 Evolução da Modelagem

#### 1. Rascunho Inicial (Conceptual)
O modelo começou com a identificação das entidades básicas: Usuário, Filme e Série.
[Clique aqui para acessar o Rascunho do Projeto]([https://neo4j.com/](https://arrows.app/#/local/id=4ewv9rxbRwwswTn2LMwH))

[Clique aqui para acessar o Neo4j](https://neo4j.com/)

### 🛠️ Modelo Otimizado para Neo4j (Cypher)

Para garantir performance em recomendações, o modelo foi refinado seguindo as melhores práticas de grafos:

* **Labels (Nós):** `:User`, `:Movie`, `:TVShow`, `:Season`, `:Episode`, `:Genre`, `:Actor`.
* **Relationships:**
    * `(:User)-[:WATCHED {rating: 5, progress: "80%"}]->(:Movie)`
    * `(:TVShow)-[:HAS_SEASON]->(:Season)-[:HAS_EPISODE]->(:Episode)`
    * `(:Actor)-[:ACTED_IN]->(:Movie)`

### 🔍 Exemplos de Consultas (Cypher)

**Encontrar filmes de um gênero específico recomendados para um usuário:**
```cypher
MATCH (u:User {name: "Hagnok"})-[:CHOSEN]->(g:Genre)
MATCH (m:Movie)-[:IN_GENRE]->(g)
WHERE NOT (u)-[:WATCHED]->(m)
RETURN m.title AS Recomendacao
