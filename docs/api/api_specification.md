Esta documentação descreve os endpoints da API RESTful para a plataforma Pincel Urbano.

### Autenticação

-   Todas as requisições autenticadas devem enviar um token JWT no cabeçalho `Authorization: Bearer <token>`.

---

#### Serviço de Usuários & Perfis

**POST /auth/register**
-   **Descrição:** Registra um novo Cliente ou Pintor.
-   **Corpo:** `{ "name": "...", "email": "...", "password": "...", "role": "client" | "painter" }`
-   **Resposta (201):** `{ "id": "...", "name": "...", "email": "...", "role": "..." }`

**POST /auth/login**
-   **Descrição:** Autentica um usuário e retorna um token.
-   **Corpo:** `{ "email": "...", "password": "..." }`
-   **Resposta (200):** `{ "accessToken": "ey..." }`

**GET /painters/:id/profile**
-   **Descrição:** Retorna o perfil público de um pintor, incluindo seu portfólio.
-   **Resposta (200):**
    ```json
    {
      "id": "...",
      "name": "Carlos Andrade",
      "bio": "Pintor com 20 anos de experiência...",
      "average_rating": 4.8,
      "portfolio": [
        { "id": "...", "imageUrl": "...", "description": "Fachada residencial" }
      ]
    }
    ```

**PUT /profile**
-   **Descrição:** Atualiza o perfil do pintor autenticado.
-   **Autorização:** `painter`

---

#### Serviço de Projetos & Orçamentos

**POST /projects**
-   **Descrição:** Cliente cria um novo projeto de pintura.
-   **Autorização:** `client`
-   **Corpo:** `{ "title": "Pintura de apartamento", "description": "...", "address": "..." }`
-   **Resposta (201):** Retorna o objeto do projeto criado.

**GET /projects**
-   **Descrição:** Lista os projetos abertos para pintores.
-   **Autorização:** `painter`
-   **Resposta (200):** `{ "data": [ { "id": "...", "title": "...", "clientName": "..." } ], "total": 10 }`

**POST /projects/:id/quotes**
-   **Descrição:** Pintor envia um orçamento para um projeto.
-   **Autorização:** `painter`
-   **Corpo:** `{ "amount": 2500.00, "estimated_days": 5, "message": "..." }`
-   **Resposta (201):** Retorna o objeto do orçamento criado.

**PATCH /quotes/:id/accept**
-   **Descrição:** Cliente aceita um orçamento. A API deve atualizar o status do projeto para "in_progress" e notificar o pintor.
-   **Autorização:** `client` (dono do projeto)
-   **Resposta (200):** `{ "message": "Orçamento aceito com sucesso." }`

**POST /projects/:id/reviews**
-   **Descrição:** Cliente publica uma avaliação para o pintor após a conclusão.
-   **Autorização:** `client` (dono do projeto)
-   **Corpo:** `{ "rating": 5, "comment": "Serviço excelente!" }`
-   **Resposta (201):** Retorna o objeto da avaliação criada.