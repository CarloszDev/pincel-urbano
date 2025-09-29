# Arquitetura do Sistema - Pincel Urbano

Este documento descreve a arquitetura proposta para a plataforma Pincel Urbano, as decisões técnicas e os padrões utilizados.

### Descrição da Arquitetura

A arquitetura do Pincel Urbano é baseada em **Microsserviços** e hospedada em nuvem (AWS), com um design *API-first*. Esta abordagem foi escolhida para garantir alta coesão e baixo acoplamento entre os domínios da aplicação (usuários, projetos, etc.), permitindo que o sistema evolua e escale de forma sustentável. Os clientes (Web e Mobile) interagem com os serviços de backend através de um **API Gateway**, que centraliza a segurança, o roteamento e o monitoramento das requisições.

**Contribuição para o ODS 11:** Uma arquitetura modular e escalável é fundamental para suportar o crescimento da economia local. Ela permite que a plataforma se adapte a novas demandas, como a inclusão de outros tipos de serviços de reforma, sem comprometer a estabilidade do ecossistema que conecta profissionais a oportunidades, fomentando uma cidade economicamente resiliente.

### Componentes do Sistema

1.  **Frontend (Mobile - React Native):** Focado na experiência do **Pintor**. Permite gerenciar perfil/portfólio, encontrar novos projetos, enviar orçamentos e se comunicar com clientes de forma ágil, mesmo fora do escritório.
2.  **Frontend (Web - React.js):** Focado na experiência do **Cliente**. Oferece uma interface confortável para postar projetos detalhados, comparar orçamentos, analisar portfólios e gerenciar os serviços contratados.
3.  **API Gateway (AWS API Gateway):** Ponto de entrada único para todas as requisições. Responsável por autenticação de tokens JWT, roteamento para os microsserviços e aplicação de políticas de rate limiting.
4.  **Serviço de Usuários & Perfis:** Gerencia o cadastro, login, e os perfis detalhados de Clientes e Pintores, incluindo o portfólio.
5.  **Serviço de Projetos & Orçamentos:** Orquestra toda a lógica de negócio relacionada à criação de projetos, envio, visualização e aceite de orçamentos.
6.  **Serviço de Notificações & Chat:** Responsável por enviar notificações (push/email) sobre eventos importantes e por gerenciar a comunicação em tempo real (via WebSockets) entre usuários.
7.  **Banco de Dados (AWS RDS - PostgreSQL):** Banco de dados relacional para armazenar os dados estruturados da aplicação (usuários, projetos, orçamentos, avaliações).
8.  **Storage de Arquivos (AWS S3):** Serviço de armazenamento de objetos para todas as mídias do sistema, como fotos de perfil, imagens de portfólio e fotos de projetos.

### Padrões Arquiteturais Utilizados

-   **Microsserviços:** Decomposição do sistema em serviços independentes por domínio de negócio.
-   **API Gateway:** Padrão que fornece uma fachada unificada para um conjunto de microsserviços.
-   **Database per Service:** Cada microsserviço possui seu próprio esquema de banco de dados, garantindo autonomia e evitando acoplamento.
-   **CQRS (Command Query Responsibility Segregation) - (Potencial):** Para o serviço de Projetos, podemos futuramente separar os modelos de escrita (criar projeto/orçamento) dos de leitura (listar projetos), otimizando a performance de cada operação.

### Diagrama de Arquitetura Detalhado

[![Diagrama de Arquitetura Detalhado](https://i.imgur.com/example-detailed.png)](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&dark=auto#G1-TKLqGBEVEuI7kTKPuG376MMACiTVMjT)
*Link para o diagrama editável no Draw.io: [Clique Aqui](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&dark=auto#G1-TKLqGBEVEuI7kTKPuG376MMACiTVMjT)*

```mermaid
graph TD
    subgraph Clients
        Mobile_Pintor[Mobile App (Pintor)]
        Web_Cliente[Web App (Cliente)]
    end

    subgraph "AWS Cloud"
        APIGateway(API Gateway)

        subgraph "Microsserviços (Lambda/ECS)"
            UserService[Serviço de Usuários/Perfis]
            ProjectService[Serviço de Projetos/Orçamentos]
            NotificationService[Serviço de Notificações/Chat]
        end

        subgraph "Persistência"
            DB[(PostgreSQL - RDS)]
            S3[Object Storage - S3]
        end

        subgraph "Comunicação em Tempo Real"
            WSS[WebSocket API]
        end
    end

    Mobile_Pintor --> APIGateway
    Web_Cliente --> APIGateway
    Mobile_Pintor -- ws:// --> WSS
    Web_Cliente -- ws:// --> WSS

    APIGateway -- /users, /profiles --> UserService
    APIGateway -- /projects, /quotes --> ProjectService
    WSS --> NotificationService

    UserService --> DB
    ProjectService --> DB
    UserService -- Fotos de Perfil/Portfólio --> S3
    ProjectService -- Fotos de Projetos --> S3
    ProjectService -- Publica Evento --> NotificationService


Decisões Técnicas e Justificativas

Node.js (NestJS) para Backend: Ideal para construir microsserviços eficientes e escaláveis. A arquitetura modular do NestJS com TypeScript se alinha perfeitamente à nossa estratégia.

React Native vs. Web: A decisão de focar o app mobile no pintor e a web no cliente otimiza a experiência para cada perfil. O pintor precisa de mobilidade, enquanto o cliente (muitas vezes uma empresa) se beneficia de uma tela maior para gerenciar projetos.

PostgreSQL: É um SGBD relacional maduro, confiável e com excelente suporte a diferentes tipos de dados, adequado para a estrutura de nosso negócio.

AWS S3: A solução padrão-ouro para armazenamento de arquivos na nuvem, oferecendo durabilidade, escalabilidade e baixo custo para as imagens da plataforma.