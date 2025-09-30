# Pincel Urbano - Conectando Cores e Oportunidades

## 📝 Descrição do Projeto

**Pincel Urbano** é uma plataforma multiplataforma (Web e Mobile) que conecta pintores autônomos e pequenas empresas de pintura a clientes residenciais, comerciais e condomínios em Fortaleza. O sistema funciona como um marketplace focado, permitindo que clientes postem seus projetos e recebam orçamentos de profissionais qualificados, enquanto os pintores ganham visibilidade, constroem uma reputação digital e acessam um fluxo constante de oportunidades de trabalho.

### 🎯 Problema Abordado e Justificativa

Pintores autônomos, como muitos trabalhadores de ofício, enfrentam dificuldades para divulgar seu trabalho, encontrar clientes de forma consistente e formalizar orçamentos de maneira profissional. Por outro lado, clientes muitas vezes lutam para encontrar profissionais de confiança, com referências e um portfólio verificável. Essa lacuna gera informalidade e insegurança para ambas as partes.

Este projeto está diretamente alinhado ao **ODS 11 (Cidades e Comunidades Sustentáveis)**, contribuindo para:
- **Meta 11.4:** Fortalecer esforços para proteger e salvaguardar o patrimônio cultural. A plataforma incentiva a renovação de fachadas e a criação de murais artísticos, valorizando a estética urbana.
- **Meta 11.7:** Proporcionar o acesso universal a espaços públicos seguros e inclusivos. A revitalização de espaços através da pintura pode aumentar a percepção de segurança e o orgulho comunitário.
- **Desenvolvimento Econômico Local:** Ao gerar trabalho e renda para profissionais locais, a plataforma fortalece a economia da comunidade, tornando-a mais resiliente e sustentável.

O Pincel Urbano ataca esse problema criando um ecossistema digital seguro e eficiente, que profissionaliza a contratação de serviços de pintura e embeleza a cidade, um projeto de cada vez.

### 🚀 Objetivos do Sistema

- **Conectar** diretamente clientes a pintores qualificados em Fortaleza.
- **Prover** uma ferramenta para pintores criarem portfólios digitais e gerenciarem seus orçamentos.
- **Facilitar** a publicação de projetos e o recebimento de múltiplos orçamentos para os clientes.
- **Garantir** segurança e transparência através de um sistema de avaliação e reviews.
- **Promover** projetos de arte urbana e revitalização de espaços públicos.

### 📋 Escopo do Projeto

**O que está incluído:**
- Cadastro e autenticação de dois perfis: "Cliente" e "Pintor".
- Perfil do Pintor com portfólio de trabalhos, biografia e avaliações.
- Funcionalidade para o Cliente postar um projeto com descrição, fotos e dimensões.
- Sistema de envio e recebimento de orçamentos para os projetos.
- Canal de comunicação (chat) entre cliente e pintor após o aceite do orçamento.
- Sistema de avaliação e review de 5 estrelas após a conclusão do serviço.
- Acesso via aplicativo móvel (foco no Pintor) e plataforma Web (foco no Cliente).

**O que NÃO está incluído (nesta fase):**
- Integração de pagamento direto pela plataforma.
- Venda de materiais de pintura (e-commerce).
- Módulo de gerenciamento de equipes para empresas de pintura.

### 🏛️ Visão Geral da Arquitetura

A arquitetura será baseada em microsserviços, garantindo que o sistema seja escalável para atender a um número crescente de usuários e projetos. A comunicação será centralizada por um API Gateway, que direcionará as requisições do Frontend (Web/Mobile) para os serviços de backend apropriados.

**Diagrama de Arquitetura (Visão de Alto Nível):**


graph TD
    subgraph "Clientes"
        A[Mobile App - React Native]
        B[Web App - React.js]
    end
    subgraph "Backend (Cloud)"
        C(API Gateway)
        D[Serviço de Usuários/Perfis]
        E[Serviço de Projetos/Orçamentos]
        F[Serviço de Notificações/Chat]
        G[Banco de Dados - PostgreSQL]
        H[Storage de Arquivos - S3]
    end
    A --> C
    B --> C
    C --> D
    C --> E
    C --> F
    D --> G
    E --> G
    E --> H
    F --> G


### 💻 Tecnologias Propostas

Frontend (Mobile): React Native
Frontend (Web): React.js com Next.js
Backend: Node.js (TypeScript) com framework NestJS
Banco de Dados: PostgreSQL
APIs: RESTful com documentação em OpenAPI (Swagger)
Autenticação: JWT (JSON Web Tokens)
Armazenamento de Arquivos: AWS S3 (para fotos de projetos e portfólios)
Containerização: Docker
Cloud: AWS (API Gateway, Lambda/ECS, RDS, S3)
CI/CD: GitHub Actions

🗓️ Cronograma para Etapa 2 (N708)
Sprint	Duração	Atividades Principais	Entregáveis
1	2 semanas	Configuração do ambiente, CI/CD, Serviço de Usuários (Backend), Telas de Login/Cadastro	Repositório configurado, API de Usuários, Telas prontas
2	2 semanas	CRUD do Perfil do Pintor (Portfólio, Bio), Upload de imagens (Backend)	Gerenciamento de perfil funcional com fotos
3	2 semanas	CRUD de Projetos (Cliente), Listagem de Projetos (Pintor), Telas Web/Mobile	Cliente posta projetos, Pintor visualiza a lista
4	2 semanas	Sistema de Orçamentos (Backend + Frontend), Aceite de Orçamento	Pintor envia orçamento, Cliente aceita
5	2 semanas	Módulo de Chat em tempo real (Websockets), Sistema de Notificações	Chat funcional entre as partes
6	2 semanas	Sistema de Avaliação e Reviews, Refatoração e Testes de integração	Sistema de reputação implementado
7	1 semana	Correção de bugs, Preparação para deploy, Documentação final, Apresentação	Aplicação estável, Documentação e vídeo de demo

👥 Integrantes da Equipe e Papéis
Nome do Aluno	Matrícula	Papel no Projeto
[Carlos Cauan Moreira]	[2326258]	Arquiteto de Software / Desenvolvedor
[José Danilo de Sousa]	[2326306] Figma / Imagens
[Jonarta Santiago Soares]	[2327349]	Documentacao
[Igor Davi Vieram Dos Santos]	[2326203]	Arquitetura escrita


Links Figma - Imagens

https://www.figma.com/design/mwDpGCOk9LWZtclOGQrkxq/Pintor-app?t=iqNmBemujbdPg1E4-1
https://imgur.com/a/W6KUFYq
