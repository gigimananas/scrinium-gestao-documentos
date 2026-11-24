# SCRINIUM: Gestão Eletrônica de Documentos

Sistema web para **governança e validação de documentos de projetos**: organiza projetos, controla versões, conduz o fluxo de revisão e aprovação e mantém a rastreabilidade de tudo o que acontece com cada arquivo.

🔗 **Sistema:** publicado no Railway (scrinium-production.up.railway.app). <!-- PREENCHER: o deploy está fora do ar em nov/2026; reativar ou trocar por vídeo/prints -->
📘 **Manual do usuário:** [`Manual_do_Usuario_SCRINIUM.pdf`](Manual_do_Usuario_SCRINIUM.pdf)
📊 **Apresentação do projeto:** [`Apresentacao_Gestao_de_Evidencia.pdf`](Apresentacao_Gestao_de_Evidencia.pdf)

> Projeto da disciplina **Consultoria Especializada de Apoio ao Projeto Integrado: Engenharia de Software**, do Bacharelado em Ciência de Dados e Inteligência Artificial da **PUC-SP** (2026/1).

## Equipe: Insight Squad

| Integrante | Papel |
|---|---|
| **Giovanna Freitas** | **Gerente de projeto** |
| Yuri Nicolav | Arquiteto |
| Kaique Munhoz | Hacker (desenvolvimento) |
| Enzo Kato | Comunicador |

## O problema

O cliente do caso foi a **Salesforce**, líder global em CRM, com ecossistema 100% em nuvem e projetos complexos. O projeto partiu de uma **entrevista qualitativa com um profissional de gestão de projetos da empresa**. Os principais achados:

- O envio de documentos **não seguia um padrão único** e dependia do perfil de cada gerente de projeto.
- Faltava **governança sobre versionamento** e sobre quais documentos eram obrigatórios em cada fase.
- **Não havia fluxo formal** de validação e aprovação; tudo dependia de cobrança.
- Resultado: baixa visibilidade, processo reativo e risco para a confiança no projeto.

> **Insight da pesquisa:** muitas vezes os documentos estão formalmente completos, mas não refletem a realidade do projeto. Há relatórios que passam sensação de controle mesmo com atrasos e problemas.

O cenário ideal pedido pelo entrevistado: entregáveis automáticos por fase, fluxo de aprovação, dashboards executivos, acompanhamento em tempo real e alertas de pendência.

## Requisitos

| Funcionais | Não funcionais | De domínio |
|---|---|---|
| Autenticação e perfis | Interface simples e intuitiva | Cada projeto tem critérios próprios de validação |
| Cadastro de projetos | Acesso pelo navegador em vários dispositivos | Qualidade e relevância valem mais que quantidade |
| Envio e validação de documentos | Segurança das informações | Documentos genéricos, duplicados ou irrelevantes não contam |
| Filtros e histórico | Integridade dos dados | O gestor acompanha e valida |
| Relatórios e indicadores | Escalabilidade para expansão futura | |

## Arquitetura e design

- **Estilo arquitetural:** monolítico em camadas (apresentação, regras de negócio e dados), escolhido pela simplicidade, facilidade de manutenção e aderência ao escopo.
- **Modelagem UML:** diagrama de classes (Usuário, Projeto, Documento, Envio, Validação), diagrama de sequência (fluxo de envio) e diagrama de atividade (análise e decisão de aprovação ou rejeição).
- **Design Patterns:**
  - **Factory Method** para criar os diferentes tipos de documento e validadores
  - **Facade** para centralizar as operações de enviar, validar, aprovar e rejeitar
  - **Observer** para notificar usuários, gestores e dashboards quando o status de um documento muda

## Evolução: do protótipo ao SCRINIUM

**1ª versão (protótipo):** cadastro e login de usuários, área protegida, upload de PDFs e listagem dos documentos por usuário.

**Versão final (SCRINIUM):**

| Área | O que faz |
|---|---|
| **Projetos e permissões** | Convites por e-mail e 4 perfis (Administrador, Revisor, Editor, Leitor), seguindo o princípio do menor privilégio |
| **Cadastro de documentos** | Upload de PDF com código automático (DOC001), tipo, fase e confidencialidade |
| **Integridade** | Verificação de PDF corrompido, páginas vazias e duplicidade, com **hash SHA256** de cada arquivo |
| **OCR** | Reconhece texto de PDFs digitalizados e torna o conteúdo pesquisável |
| **Conformidade automática** | Regras por projeto: palavras obrigatórias, número de páginas, validação de CNPJ, datas e valores |
| **Versionamento** | DOC001 v1 → v2 → v3, com histórico de quem enviou, quando e por quê |
| **Revisão e aprovação** | Em elaboração → Em revisão → Aprovado / Rejeitado, com vários revisores e prazos |
| **Auditoria e LGPD** | Registro de visualizações, downloads, alterações e aprovações; exportação do projeto em ZIP |
| **Relatórios** | Documentos por status, prazos e decisões, com exportação em CSV |

## Tecnologias

Stack definida pela equipe para o projeto:

| Camada | Tecnologia |
|---|---|
| Backend | Python · Flask |
| Frontend | HTML · CSS · Bootstrap (templates Flask) |
| Banco de dados | SQLite |
| Autenticação | Flask-Login |
| Deploy | Render (protótipo) → Railway (versão final) |

<!-- PREENCHER: confirmar com o Kaique/Yuri se a versão final manteve essa stack e qual biblioteca de OCR foi usada -->

Motivos da escolha: baixo custo, curva de aprendizado menor, rapidez no desenvolvimento e boa manutenção no contexto acadêmico.

## Minha contribuição

Atuei como **gerente de projeto** da equipe: conduzi o planejamento e a organização das entregas e participei de todas as etapas, com destaque para o **levantamento de requisitos**, a **modelagem UML** (diagramas de classe, sequência e atividade) e o **protótipo** da interface. Também participei da apresentação final.
<!-- PREENCHER: confirmar com a Giovanna -->
