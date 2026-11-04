# 4. Exemplos de Integração

## 4.1 Objetivo

Esta seção apresenta exemplos ilustrativos de requisições e respostas para demonstrar como o Front-end pode consumir a API e tratar os diferentes resultados da consulta de profissionais.

> **Importante:** os exemplos são mocks técnicos. Os endpoints, campos, parâmetros e formatos devem ser validados com a implementação real da API da Lacrei Saúde.

## 4.2 Exemplo de requisição

A consulta de profissionais utiliza o método HTTP GET e pode receber filtros e parâmetros de paginação pela URL.

**Requisição ilustrativa:**

```http
GET /profissionais/?especialidade=psicologia&cidade=sao-paulo&page=1&page_size=10
Accept: application/json
```

Como se trata de uma operação GET, os critérios de consulta são enviados por meio de query parameters, não no corpo da requisição.

## 4.3 Exemplo de resposta com sucesso

**Status HTTP:** `200 OK`

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

Os registros são fictícios e representam apenas uma amostra da resposta.

## 4.4 Exemplo de resposta sem resultados

**Status HTTP:** `200 OK`

```json
{
  "count": 0,
  "next": null,
  "previous": null,
  "results": []
}
```

Uma consulta válida pode não encontrar profissionais que correspondam aos filtros informados.

Nesse cenário, a API pode retornar uma resposta de sucesso com uma lista vazia. O Front-end deve apresentar um estado vazio (*Empty State*), em vez de interpretar a ausência de resultados como uma falha técnica.

## 4.5 Exemplo de resposta com erro

**Status HTTP:** `400 Bad Request`

```json
{
  "error": "INVALID_PAGE",
  "message": "O parâmetro page deve ser um número inteiro positivo."
}
```

Esse exemplo demonstra uma possível resposta quando o parâmetro de paginação apresenta um valor inválido.

O formato e o código HTTP precisam ser confirmados com a implementação real.

## 4.6 Estados da interface

O Front-end deve considerar diferentes estados durante a consulta:

| Estado | Situação | Comportamento esperado |
|---|---|---|
| Loading | Requisição em andamento | Exibir indicador de carregamento |
| Success | Consulta realizada com resultados | Apresentar os perfis encontrados |
| Empty State | Consulta válida sem resultados | Exibir mensagem informativa |
| Error | Falha na requisição | Apresentar mensagem de erro e opção de tentar novamente, quando aplicável |

## 4.7 Fluxo de integração

1. O usuário acessa a página de consulta.
2. O Front-end apresenta os campos de pesquisa.
3. O usuário informa os filtros desejados.
4. O Front-end envia a requisição GET para a API.
5. O Back-end valida os parâmetros e processa a consulta.
6. A API retorna os dados ou uma resposta de erro.
7. O Front-end interpreta a resposta.
8. A interface apresenta os resultados ou o estado correspondente.

## 4.8 Tratamento de erros no Front-end

O Front-end deve interpretar o resultado da requisição e apresentar mensagens compreensíveis.

Recomendações:

- Não apresentar mensagens técnicas internas diretamente ao usuário.
- Diferenciar ausência de resultados de falhas na comunicação.
- Disponibilizar uma nova tentativa quando a operação permitir.
- Evitar expor dados sensíveis em mensagens ou logs.
- Manter estados visuais consistentes durante a consulta.

## 4.9 Pendências de validação

- Confirmar o formato real das respostas da API.
- Verificar se a paginação utiliza os campos apresentados.
- Confirmar os códigos HTTP e os formatos de erro.
- Validar os estados de interface com o comportamento real do Front-end.
- Confirmar os mecanismos utilizados para cancelamento e repetição de requisições, se existentes.