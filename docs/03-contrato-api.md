# 3. Contrato da API

## 3.1 Objetivo

Esta seção apresenta uma proposta ilustrativa de contrato para o fluxo de consulta e apresentação de perfis profissionais.

O contrato descreve métodos HTTP, endpoints, parâmetros, formatos de resposta e possíveis códigos de status, servindo como referência para a integração entre Front-end e Back-end.

> **Importante:** os endpoints e exemplos desta seção não foram confirmados no código-fonte da Lacrei Saúde. São propostas técnicas para demonstrar a documentação do fluxo e precisam ser validadas com a implementação real.

## 3.2 Operações propostas

| Método | Endpoint | Finalidade |
|---|---|---|
| GET | `/profissionais/` | Listar profissionais |
| GET | `/profissionais/{id}/` | Consultar detalhes de um profissional |

A pesquisa por filtros utiliza parâmetros de consulta na operação de listagem, sem exigir um endpoint separado.

## 3.3 Listagem de profissionais

**Método:** GET

**Endpoint:** `/profissionais/`

**Descrição:** retorna uma lista de profissionais, podendo aplicar filtros e paginação.

### Parâmetros de consulta

| Parâmetro | Tipo esperado | Obrigatório | Descrição |
|---|---|---|---|
| `especialidade` | String | Não | Filtra pela especialidade |
| `cidade` | String | Não | Filtra pela cidade |
| `page` | Integer | Não | Número da página |
| `page_size` | Integer | Não | Quantidade de registros por página |

### Exemplo de requisição

```http
GET /profissionais/?especialidade=psicologia&cidade=sao-paulo&page=1&page_size=10
Accept: application/json
```

Os parâmetros de consulta são transmitidos na URL. Os tipos indicados na tabela representam os valores esperados pela API após a interpretação e validação.

### Exemplo de resposta — 200 OK

```json
{
  "count": 25,
  "next": "https://api.exemplo.com/profissionais/?page=2",
  "previous": null,
  "results": [
    {
      "id": 1,
      "nome": "Ana Silva",
      "especialidade": "Psicologia",
      "cidade": "São Paulo"
    },
    {
      "id": 2,
      "nome": "Carlos Souza",
      "especialidade": "Psicologia",
      "cidade": "São Paulo"
    }
  ]
}
```

Os dois registros são ilustrativos e não representam dados reais da plataforma. O exemplo demonstra o formato de uma resposta paginada; a quantidade de itens apresentada pode ser apenas uma amostra da página.

### Campos da resposta

| Campo | Tipo | Descrição |
|---|---|---|
| `count` | Integer | Total de registros encontrados |
| `next` | String ou Null | URL da próxima página, quando disponível |
| `previous` | String ou Null | URL da página anterior, quando disponível |
| `results` | Array | Lista de profissionais da página atual |

### Paginação

A paginação permite retornar os registros em partes, evitando respostas excessivamente grandes.

Exemplo:

```http
GET /profissionais/?page=2&page_size=10
```

Considerando 25 registros no total:

- Página 1: registros 1 a 10.
- Página 2: registros 11 a 20.
- Página 3: registros 21 a 25.

Na última página, o campo `next` pode retornar `null`. Na primeira página, o campo `previous` pode retornar `null`.

A estrutura apresentada é uma proposta ilustrativa e precisa ser validada com o comportamento real da API.

## 3.4 Consulta de detalhes de um profissional

**Método:** GET

**Endpoint:** `/profissionais/{id}/`

**Descrição:** consulta os detalhes de um profissional identificado pelo seu ID.

### Exemplo de requisição

```http
GET /profissionais/123/
Accept: application/json
```

### Exemplo de resposta — 200 OK

```json
{
  "id": 123,
  "nome": "Ana Silva",
  "especialidade": "Psicologia",
  "cidade": "São Paulo"
}
```

Os campos são exemplos didáticos e não representam o schema oficial da plataforma.

## 3.5 Códigos de status HTTP

| Código | Significado | Situação ilustrativa |
|---|---|---|
| 200 | OK | Consulta realizada com sucesso |
| 400 | Bad Request | Parâmetro inválido |
| 401 | Unauthorized | Autenticação ausente ou inválida |
| 403 | Forbidden | Usuário autenticado sem permissão |
| 404 | Not Found | Profissional não encontrado |
| 500 | Internal Server Error | Falha inesperada no servidor |

Os códigos apresentados são possibilidades de comportamento. Os status efetivamente utilizados devem ser confirmados na implementação.

## 3.6 Exemplo de erro

**Requisição ilustrativa:**

```http
GET /profissionais/?page=abc
```

**Resposta ilustrativa — 400 Bad Request:**

```json
{
  "error": "INVALID_PAGE",
  "message": "O parâmetro page deve ser um número inteiro positivo."
}
```

### Campos do erro

| Campo | Tipo | Descrição |
|---|---|---|
| `error` | String | Identificador técnico do erro |
| `message` | String | Descrição do problema |

## 3.7 Validação e tratamento

O Back-end deve validar os parâmetros recebidos antes de executar a consulta.

Entre as validações propostas estão:

- Verificar se `page` é um inteiro positivo.
- Verificar se `page_size` respeita os limites definidos pela API.
- Validar os formatos dos filtros recebidos.
- Verificar se o profissional solicitado existe.
- Aplicar os controles de acesso necessários antes de disponibilizar dados protegidos.

O Front-end deve interpretar os códigos de resposta e apresentar mensagens adequadas ao usuário, sem expor detalhes internos do servidor.

## 3.8 Pendências de validação

- Confirmar os endpoints reais.
- Verificar os nomes e tipos dos parâmetros.
- Confirmar a estrutura de paginação.
- Identificar os campos reais dos perfis profissionais.
- Verificar os códigos HTTP utilizados.
- Confirmar o formato oficial das respostas de erro.
- Validar os requisitos de autenticação e autorização.