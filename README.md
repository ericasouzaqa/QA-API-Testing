# QA API Testing

Guia prático de APIs, Postman e testes para QA.

---

## Objetivo

Este projeto funciona como um guia de aprendizado para:

* entender APIs;
* interpretar Requests e Responses;
* conhecer os principais métodos HTTP;
* entender Status Codes;
* utilizar o Postman;
* criar cenários de teste;
* testar cenários positivos e negativos;
* analisar erros;
* aplicar boas práticas de QA;
* praticar testes em APIs públicas.

---

## Como estudar

A recomendação é seguir uma sequência:

```text
Fundamentos de API
        ↓
HTTP
        ↓
Request e Response
        ↓
Status Codes
        ↓
Postman
        ↓
Testes positivos e negativos
        ↓
Testes de integração
        ↓
Automação
```

Consulte o arquivo [`terms.md`](./terms.md) sempre que encontrar um termo desconhecido.

Para o estudo específico de Postman, consulte [`postman.md`](./postman.md).

---

## Laboratório prático

Depois de estudar os conceitos, pratique utilizando APIs públicas.

### Postman Echo

O Postman Echo é uma API disponibilizada pelo próprio Postman para testar requisições. O serviço retorna informações sobre a requisição enviada e é utilizado na documentação oficial para aprendizado.

Exemplo:

```http
GET https://postman-echo.com/get
```

Depois experimente:

```http
GET https://postman-echo.com/get?nome=Erica
```

Observe:

* Status Code;
* Headers;
* URL;
* método utilizado;
* parâmetros;
* dados retornados.

[Postman Echo](https://learning.postman.com/docs/developer/echo-api)

---

## Swagger Petstore

O Swagger Petstore é uma API de exemplo baseada na especificação OpenAPI 3.0 e possui operações para pets, usuários e pedidos.

Acesse:

[Swagger Petstore](https://petstore3.swagger.io/)

Pratique:

```text
POST /pet
GET /pet/{petId}
PUT /pet
DELETE /pet/{petId}
```

Monte o seguinte fluxo:

```text
Criar
  ↓
Consultar
  ↓
Alterar
  ↓
Consultar novamente
  ↓
Excluir
  ↓
Consultar novamente
```

---

## Desafio final

Crie uma Collection no Postman contendo:

1. Criar pet;
2. Consultar pet;
3. Alterar pet;
4. Consultar novamente;
5. Excluir pet;
6. Consultar após exclusão;
7. Criar pelo menos um cenário negativo.

Depois adicione testes automatizados para validar:

* Status Code;
* presença de campos;
* valores;
* tipos;
* estrutura do Response;
* comportamento esperado.

O Postman permite organizar requisições em Collections e executar essas Collections como conjuntos de testes.

---

## Boas práticas em testes de API

### Conheça o contrato

Antes de testar, entenda:

* endpoint;
* método;
* parâmetros;
* headers;
* autenticação;
* Request;
* Response;
* comportamento esperado.

### Teste cenários positivos e negativos

Inclua:

* dados válidos;
* campos obrigatórios ausentes;
* dados inválidos;
* formatos incorretos;
* valores limite;
* autenticação inválida;
* recursos inexistentes;
* métodos não permitidos.

### Não valide somente o Status Code

Um `200 OK` não garante que o comportamento esteja correto.

Valide também:

* Response Body;
* Headers;
* campos;
* valores;
* tipos;
* regras de negócio;
* mensagens;
* comportamento esperado.

### Utilize dados de teste

Evite versionar:

* senhas;
* tokens;
* chaves de API;
* credenciais;
* dados pessoais reais.

### Utilize variáveis

Exemplo:

```text
{{base_url}}
{{token}}
{{pet_id}}
```

### Organize as requisições

Exemplo:

```text
Petstore
├── Criar Pet
├── Consultar Pet
├── Alterar Pet
├── Excluir Pet
└── Cenários Negativos
```

### Pense em regressão

Depois de uma alteração, execute novamente os testes relevantes.

### Automatize testes repetitivos

Quando uma validação precisa ser executada frequentemente, considere automatizá-la.

O Postman permite executar Collections manualmente, agendar execuções e integrar execuções a pipelines de CI/CD.

---

## Aplicação em QA

Um teste de API não deve responder apenas:

> A API respondeu?

A pergunta deve ser:

> A API respondeu corretamente para este cenário?

Fluxo de validação:

```text
Requisito
   ↓
Contrato da API
   ↓
Request
   ↓
Processamento
   ↓
Response
   ↓
Validação
   ↓
Evidência
   ↓
Resultado
```

---

## Material complementar

### Postman

Para estudar o Postman de forma mais detalhada:

[`postman.md`](./postman.md)

[Documentação oficial do Postman](https://learning.postman.com/)

### Get Started with API Testing

O Postman disponibiliza uma coleção prática que trabalha scripts, encadeamento de requisições, autorização, variáveis e validação de dados.

[Get Started with API Testing — Postman](https://www.postman.com/devrel/postman-community-challenge/folder/4pjyd3k/get-started-with-api-testing)

### APIs para prática

[Postman Echo](https://learning.postman.com/docs/developer/echo-api)

[Swagger Petstore](https://petstore3.swagger.io/)

---

## Tecnologias e ferramentas

* REST
* HTTP
* JSON
* Postman
* Swagger / OpenAPI
* Git
* GitHub

---

## Estrutura

```text
qa-api-glossary/
├── README.md
├── terms.md
└── postman.md
```

| Arquivo      | Descrição                                   |
| ------------ | ------------------------------------------- |
| `README.md`  | Guia principal, laboratório e boas práticas |
| `terms.md`   | Glossário de termos de API e QA             |
| `postman.md` | Guia prático de estudo do Postman           |

---

## Próximos passos

Depois de concluir os exercícios:

```text
Fundamentos
    ↓
Postman
    ↓
Testes manuais
    ↓
Cenários negativos
    ↓
Testes automatizados
    ↓
Integração
    ↓
CI/CD
    ↓
Testes de desempenho
```

O objetivo é sair da simples execução de requisições e desenvolver a capacidade de analisar, validar e automatizar o comportamento de APIs.

---

## Autora

**Erica de Souza**

QA Analyst com foco em qualidade de software, testes de API, automação e aplicações de Inteligência Artificial.

---

> Material desenvolvido para estudo, consulta e prática de testes de API com foco em QA.
