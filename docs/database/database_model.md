```markdown
# Modelo de Dados - Pincel Urbano

Este documento descreve o modelo de dados, as entidades, relacionamentos e o dicionário de dados para o banco de dados da plataforma Pincel Urbano.

### Modelo de Dados

O modelo é relacional e projetado para suportar as principais jornadas do usuário: um cliente postando um projeto, um pintor enviando um orçamento, e o sistema de reputação baseado em avaliações.

### Diagrama Entidade-Relacionamento (ER)

[![Diagrama ER](https://i.imgur.com/example-er-diagram.png)](https://dbdiagram.io/d/database_model-68db0c14d2b621e4227a87bb)
*Link para o diagrama DbDiagram.io: [Clique Aqui](https://dbdiagram.io/d/database_model-68db0c14d2b621e4227a87bb)*

**Código para DbDiagram.io:**

Table users {
  id uuid [pk]
  name varchar(255) [not null]
  email varchar(255) [unique, not null]
  password_hash varchar(255) [not null]
  role user_role [not null]
  created_at timestamp [default: `now()`]
}

Enum user_role {
  client
  painter
}

Table painter_profiles {
  user_id uuid [pk, ref: > users.id]
  bio text
  phone_number varchar(20)
  city varchar(100)
  state varchar(2)
  profile_picture_url varchar(255)
  average_rating decimal(2,1) [default: 0]
}

Table portfolio_items {
  id uuid [pk]
  painter_id uuid [ref: > painter_profiles.user_id]
  image_url varchar(255) [not null]
  description text
  created_at timestamp [default: `now()`]
}

Table projects {
  id uuid [pk]
  client_id uuid [ref: > users.id]
  title varchar(255) [not null]
  description text [not null]
  address text
  status project_status [not null, default: 'open']
  created_at timestamp [default: `now()`]
  completed_at timestamp
}

Enum project_status {
  open
  in_progress
  completed
  canceled
}

Table project_photos {
  id uuid [pk]
  project_id uuid [ref: > projects.id]
  photo_url varchar(255) [not null]
}

Table quotes {
  id uuid [pk]
  project_id uuid [ref: > projects.id]
  painter_id uuid [ref: > users.id]
  amount decimal(10, 2) [not null]
  estimated_days int
  message text
  status quote_status [not null, default: 'pending']
  created_at timestamp [default: `now()`]
}

Enum quote_status {
  pending
  accepted
  rejected
}

Table reviews {
  id uuid [pk]
  project_id uuid [ref: > projects.id]
  client_id uuid [ref: > users.id]
  painter_id uuid [ref: > users.id]
  rating int [not null]
  comment text
  created_at timestamp [default: `now()`]
}


### Descrição das Entidades e Relacionamentos

-   **users:** Tabela base para todos os usuários, diferenciados pelo campo `role`.
-   **painter_profiles:** Armazena informações adicionais específicas dos pintores, em uma relação 1-para-1 com `users`.
-   **portfolio_items:** Cada item é uma foto/descrição do trabalho de um pintor, em uma relação N-para-1 com `painter_profiles`.
-   **projects:** Contém os detalhes de um serviço solicitado por um `client`.
-   **quotes:** Representa um orçamento enviado por um `painter` para um `project`. Um projeto pode ter várias `quotes`.
-   **reviews:** Avaliação que um `client` deixa para um `painter` após a conclusão de um `project`.

### Dicionário de Dados (Parcial)

| Tabela | Campo | Tipo | Descrição |
|---|---|---|---|
| **users** | id | uuid | Identificador único do usuário (PK) |
| | role | user_role | Papel do usuário ('client', 'painter') |
| **painter_profiles** | user_id | uuid | Chave primária e estrangeira para `users` |
| | average_rating | decimal(2,1)| Nota média calculada a partir das `reviews` |
| **projects**| id | uuid | Identificador único do projeto (PK) |
| | client_id | uuid | FK para o usuário que criou o projeto |
| | status | project_status | Status atual do projeto ('open', 'in_progress', 'completed')|
| **quotes** | id | uuid | Identificador único do orçamento (PK) |
| | project_id | uuid | FK para o projeto que está sendo orçado |
| | painter_id | uuid | FK para o pintor que enviou o orçamento |
| | amount | decimal(10,2)| Valor do orçamento em Reais (BRL) |