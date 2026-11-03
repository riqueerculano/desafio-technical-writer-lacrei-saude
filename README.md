# Documentação Técnica — Lacrei Saúde

## Sobre o projeto

Este projeto consiste na elaboração de uma documentação técnica voltada à compreensão do fluxo de consulta e apresentação de perfis de profissionais de saúde da plataforma Lacrei Saúde.

O material aborda a comunicação entre Front-end e Back-end, apresentando conceitos de arquitetura, integração por API, estrutura de requisições e respostas, tratamento de erros e requisitos de segurança.

A documentação tem como finalidade facilitar o entendimento do fluxo de integração e servir como referência técnica para profissionais envolvidos no desenvolvimento e na validação da aplicação.

## Objetivos

- Documentar o fluxo de consulta e apresentação de profissionais.
- Explicar a comunicação entre Front-end e Back-end.
- Apresentar exemplos de requisições e respostas da API.
- Documentar conceitos de segurança e privacidade.
- Facilitar a compreensão técnica e a validação da integração.

## Tecnologias mencionadas no desafio

De acordo com as informações disponibilizadas no enunciado:

- **Front-end:** Next.js, TypeScript e Styled-Components.
- **Back-end:** Python, Django e Django REST Framework.
- **Banco de dados:** PostgreSQL.
- **Gerenciamento de dependências:** Poetry.
- **Infraestrutura:** Docker e serviços AWS.

> **Nota:** a relação foi baseada no enunciado do desafio. A configuração e o uso efetivo de cada tecnologia devem ser confirmados na implementação.

## Organização da documentação

| Arquivo | Descrição |
|---|---|
| `docs/01-visao-geral.md` | Objetivo, público-alvo e escopo |
| `docs/02-arquitetura.md` | Componentes e fluxo de comunicação |
| `docs/03-contrato-api.md` | Endpoints, parâmetros e respostas |
| `docs/04-exemplos-api.md` | Exemplos de integração e estados da interface |
| `docs/05-seguranca-lgpd.md` | Segurança e privacidade |
| `docs/06-glossario-referencias.md` | Glossário e fontes técnicas |
| `docs/07-pendencias-validacao.md` | Informações pendentes de confirmação |

### Diagramas

Os diagramas estão organizados na pasta `diagrams/`:

- `arquitetura.mmd`
- `fluxo-consulta.mmd`

### Exemplos

A pasta `examples/` contém exemplos ilustrativos de integração:

- `request.json`
- `response-success.json`
- `response-error.json`

## Nota sobre validação técnica

Os endpoints, parâmetros, estruturas JSON e comportamentos de API apresentados como exemplos são propostas ilustrativas, não contratos oficiais confirmados da Lacrei Saúde.

As informações que dependem da implementação real estão identificadas como pendentes de validação.

## Público-alvo

- Desenvolvedores Front-end.
- Desenvolvedores Back-end.
- Profissionais de QA (Quality Assurance).

## Status do projeto

Documentação técnica em desenvolvimento e revisão.
