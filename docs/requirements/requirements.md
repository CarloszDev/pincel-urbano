```markdown
# Documento de Requisitos - Pincel Urbano

Este documento detalha os requisitos funcionais, não-funcionais, regras de negócio e perfis de usuário para a plataforma Pincel Urbano.

### Perfis de Usuários

1.  **Cliente:** Pessoa física, síndico de condomínio ou gerente de negócio que precisa contratar um serviço de pintura.
2.  **Pintor/Profissional:** Trabalhador autônomo ou representante de uma pequena empresa de pintura que oferece seus serviços.

### Requisitos Funcionais (RF)

| ID   | Descrição                                                                              | Perfil         | Prioridade |
|------|------------------------------------------------------------------------------------------|----------------|------------|
| RF01 | O sistema deve permitir que um usuário se cadastre como "Cliente" ou "Pintor".           | Ambos          | Alta       |
| RF02 | O Pintor deve poder preencher seu perfil com informações pessoais, biografia e foto.       | Pintor         | Alta       |
| RF03 | O Pintor deve poder criar e gerenciar um portfólio, adicionando fotos e descrições de trabalhos anteriores. | Pintor         | Alta       |
| RF04 | O Cliente deve poder criar um novo projeto, informando título, descrição, tipo de imóvel e anexando fotos do local. | Cliente        | Alta       |
| RF05 | O Pintor deve poder visualizar uma lista de projetos abertos e filtrá-los por bairro ou tipo de serviço. | Pintor         | Alta       |
| RF06 | O Pintor deve poder enviar um orçamento para um projeto, informando valor, prazo estimado e uma mensagem. | Pintor         | Alta       |
| RF07 | O Cliente deve poder visualizar os orçamentos recebidos, acessar o perfil dos pintores e escolher um para o serviço. | Cliente        | Alta       |
| RF08 | O sistema deve disponibilizar um chat para comunicação entre Cliente e Pintor após o aceite de um orçamento. | Ambos          | Média      |
| RF09 | Ao final do serviço, o Cliente deve poder avaliar o Pintor com uma nota de 1 a 5 estrelas e um comentário. | Cliente        | Alta       |
| RF10 | A nota média do Pintor deve ser visível publicamente em seu perfil.                       | Ambos          | Alta       |
| RF11 | O sistema deve notificar o Pintor sobre novos projetos em sua região e o Cliente sobre novos orçamentos recebidos. | Ambos          | Média      |

### Requisitos Não-Funcionais (RNF)

| ID   | Categoria       | Descrição                                                                                                                              |
|------|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| RNF01| Desempenho      | O upload de imagens do portfólio deve ser otimizado para não exceder 5 segundos. A listagem de projetos deve carregar em menos de 2 segundos. |
| RNF02| Usabilidade     | A interface deve ser limpa e objetiva. O processo de postar um projeto não deve levar mais de 3 minutos. O app mobile deve ser fácil de usar em campo. |
| RNF03| Segurança       | Dados pessoais devem ser protegidos. A comunicação entre cliente e servidor deve ser via HTTPS. Senhas devem ser armazenadas com hash. |
| RNF04| Disponibilidade | O sistema deve ter uma disponibilidade de 99.5%.                                                                                         |
| RNF05| Confiabilidade  | O sistema de notificações e chat deve garantir a entrega das mensagens. O sistema de avaliações não pode ser manipulado.             |
| RNF06| Compatibilidade | O aplicativo móvel deve ser compatível com Android 8.0+ e iOS 14+. O portal web deve ser responsivo e compatível com os principais navegadores. |

### Regras de Negócio (RN)

1.  **RN01:** O cadastro de um Pintor requer aprovação de um administrador para garantir a qualidade da plataforma.
2.  **RN02:** Um Cliente só pode avaliar um Pintor após a marcação de um projeto como "Concluído".
3.  **RN03:** Um Pintor não pode ver os orçamentos de outros pintores para o mesmo projeto.
4.  **RN04:** A plataforma retém uma comissão de 10% sobre o valor do orçamento aceito (para monetização futura).
5.  **RN05:** Um projeto postado expira após 30 dias se nenhum orçamento for aceito.

### Histórias de Usuário

**HU-01: Encontrar Oportunidades**
- **Eu, como** um pintor autônomo,
- **Quero** criar um perfil com meu portfólio e ver uma lista de projetos de pintura disponíveis na minha cidade,
- **Para que** eu possa encontrar mais trabalhos e aumentar minha renda.

**HU-02: Contratar com Segurança**
- **Eu, como** uma síndica de condomínio,
- **Quero** postar a necessidade de pintura da fachada do prédio e receber orçamentos de vários profissionais com avaliações de outros clientes,
- **Para que** eu possa contratar um serviço de qualidade com segurança e transparência.

**HU-03: Construir Reputação**
- **Eu, como** um pintor profissional,
- **Quero** receber avaliações pelos meus serviços concluídos,
- **Para que** eu possa construir uma boa reputação na plataforma e atrair clientes maiores.

---
**Alinhamento com ODS 11:** Estes requisitos criam uma ferramenta de empoderamento econômico para trabalhadores locais, promovendo a manutenção e o embelezamento da infraestrutura urbana (casas, prédios, espaços públicos), o que contribui diretamente para cidades mais agradáveis, sustentáveis e economicamente ativas.