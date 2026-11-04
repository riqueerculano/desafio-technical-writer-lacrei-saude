# 5. Segurança e LGPD

## 5.1 Objetivo

Esta seção apresenta recomendações de segurança e privacidade para o fluxo de consulta e apresentação de perfis profissionais, considerando a natureza dos dados tratados pela plataforma.

As recomendações têm como referência boas práticas de desenvolvimento seguro e a Lei Geral de Proteção de Dados Pessoais (LGPD — Lei nº 13.709/2018).

> **Importante:** este documento apresenta recomendações técnicas. Não representa uma auditoria nem confirma que os mecanismos descritos estejam implementados na plataforma Lacrei Saúde.

## 5.2 Proteção de dados pessoais

A LGPD classifica dados referentes à saúde como dados pessoais sensíveis.

Por esse motivo, sistemas que tratam essas informações devem adotar medidas técnicas e organizacionais adequadas para proteger os dados contra acessos não autorizados, perda, alteração ou divulgação indevida.

A documentação técnica deve considerar:

- Finalidade e necessidade do tratamento dos dados.
- Restrição de acesso conforme as responsabilidades de cada usuário.
- Proteção das informações durante a transmissão e o armazenamento.
- Minimização da coleta e exposição de dados.
- Cuidados com registros de logs e monitoramento.

## 5.3 Autenticação e autorização

Autenticação e autorização são mecanismos diferentes e complementares.

- **Autenticação:** verifica a identidade de quem está acessando o sistema.
- **Autorização:** determina quais recursos e operações essa identidade pode acessar.

Exemplo ilustrativo:

Um profissional pode estar autenticado na plataforma, mas isso não significa que tenha permissão para acessar informações administrativas ou dados de outros usuários.

### Códigos HTTP relacionados

| Código | Significado | Contexto |
|---|---|---|
| 401 | Unauthorized | Credenciais ausentes ou inválidas |
| 403 | Forbidden | Usuário autenticado sem permissão para acessar o recurso |

Os códigos apresentados são referências conceituais. O comportamento real deve ser confirmado na API.

## 5.4 Validação e proteção de entradas

Toda informação recebida pela API deve ser validada no Back-end.

Recomendações:

- Validar tipos e formatos dos parâmetros.
- Verificar limites de paginação.
- Rejeitar valores incompatíveis com o contrato.
- Utilizar consultas parametrizadas ou mecanismos seguros de ORM para reduzir riscos de SQL Injection.
- Evitar confiar exclusivamente nas validações realizadas pelo Front-end.

A validação no Front-end melhora a experiência de uso, mas não substitui a validação no servidor.

## 5.5 Proteção de informações

Recomendações para reduzir riscos de exposição:

- Utilizar HTTPS na comunicação entre cliente e servidor.
- Restringir o acesso aos dados conforme o princípio do menor privilégio.
- Evitar exposição de informações sensíveis em URLs.
- Não registrar dados pessoais sensíveis desnecessariamente nos logs.
- Não disponibilizar credenciais, tokens ou segredos no código do Front-end.
- Avaliar mecanismos de proteção e controle de acesso aos dados armazenados.

## 5.6 Logs e monitoramento

Os registros de aplicação devem apoiar a identificação e investigação de falhas sem expor informações pessoais desnecessárias.

Sempre que possível, priorizar informações técnicas, como:

- Identificador da requisição (*request ID*).
- Data e horário do evento.
- Operação executada.
- Código de status HTTP.
- Identificação técnica do erro.

Dados de saúde, credenciais, tokens e outras informações sensíveis não devem ser registrados sem necessidade e justificativa adequada.

## 5.7 Princípio do menor privilégio

O acesso a recursos deve ser concedido somente quando necessário para a execução de determinada atividade.

Esse princípio ajuda a reduzir o impacto de acessos indevidos e limita a exposição de informações.

## 5.8 Referência legal

**Lei nº 13.709/2018 — Lei Geral de Proteção de Dados Pessoais (LGPD).**

A LGPD estabelece regras para o tratamento de dados pessoais, incluindo dados pessoais sensíveis, e prevê princípios e medidas de segurança aplicáveis às atividades de tratamento.

Referência oficial: https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm

## 5.9 Pendências de validação

- Confirmar os mecanismos reais de autenticação.
- Verificar como são aplicadas as permissões de acesso.
- Identificar os mecanismos de proteção dos dados em trânsito e em repouso.
- Verificar as políticas de logs e retenção.
- Confirmar como dados sensíveis são tratados e protegidos.
- Validar os controles de segurança com as equipes responsáveis.