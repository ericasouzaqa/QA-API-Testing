# QA API Glossary

Glossário prático de **API REST, HTTP, Postman e testes de API**, criado para estudo, consulta e prática em QA.

O objetivo é ajudar quem está começando a entender APIs e transformar os conceitos aprendidos em testes práticos.

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

---

## Laboratório prático

Depois de estudar os conceitos, pratique utilizando APIs públicas.

### 1. Postman Echo

O Postman Echo é uma API disponibilizada pelo próprio Postman para testar requisições. O serviço retorna informações sobre a requisição enviada e é utilizado na documentação oficial para aprendizado.

#### Primeiro teste

No Postman, crie uma requisição:

```http
GET https://postman-echo.com/get
```

Clique em **Send**.

Observe o Response e verifique:

* Status Code;
* Headers;
* URL;
* método utilizado;
* dados enviados;
* dados retornados.

#### Testando parâmetros

Agora utilize:

```http
GET https://postman-echo.com/get?nome=Erica
```

Compare o Response com o teste anterior.

Pergunta para o exercício:

> Onde o parâmetro `nome` aparece no Response?

Documentação:

[Postman Echo](https://learning.postman.com/docs/developer/echo-api)

---

### 2. Swagger Petstore

Depois do Echo, avance para uma API com operações de negócio simuladas.

O Swagger Petstore é uma API de exemplo baseada em OpenAPI 3.0 e possui operações para pets, usuários e pedidos.

Acesse:

[Swagger Petstore](https://petstore3.swagger.io/)

### Exercício 1 — Consultar pets

Utilize:

```http
GET /pet/findByStatus
```

Escolha um status disponível e execute a requisição.

Valide:

* Status Code;
* estrutura do Response;
* quantidade de registros;
* campos retornados;
* tipos dos dados.

### Exercício 2 — Criar um pet

Utilize:

```http
POST /pet
```

Exemplo:

```json
{
  "id": 12345,
  "name": "Rex",
  "status": "available"
}
```

Valide:

* Status Code;
* ID;
* nome;
* status;
* estrutura do Response.

### Exercício 3 — Consultar o pet criado

Utilize:

```http
GET /pet/{petId}
```

Substitua `{petId}` pelo ID utilizado no exercício anterior.

Valide:

* se o recurso foi encontrado;
* se o ID corresponde;
* se os dados são os mesmos;
* Status Code;
* estrutura do Response.

### Exercício 4 — Alterar o pet

Utilize:

```http
PUT /pet
```

Exemplo:

```json
{
  "id": 12345,
  "name": "Rex",
  "status": "sold"
}
```

Depois consulte novamente:

```http
GET /pet/12345
```

Valide se a alteração foi aplicada.

### Exercício 5 — Cenário negativo

Tente consultar um ID inexistente:

```http
GET /pet/999999999
```

Analise:

* Status Code;
* mensagem;
* estrutura do erro;
* comportamento da API.

Não considere apenas o código HTTP. O conteúdo do Response também deve ser analisado.

### Exercício 6 — Excluir

Utilize:

```http
DELETE /pet/{petId}
```

Depois tente consultar novamente:

```http
GET /pet/{petId}
```

Valide o comportamento apresentado após a exclusão.

---

## Desafio final

Execute o fluxo completo:

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

Organize todas as requisições em uma Collection do Postman.

Collections permitem organizar requisições, testes e outros elementos relacionados a uma API.

Ao terminar, você deverá conseguir explicar:

* o que é um endpoint;
* diferença entre GET, POST, PUT e DELETE;
* o que é Request;
* o que é Response;
* o que é Status Code;
* como testar um cenário positivo;
* como testar um cenário negativo;
* como validar uma resposta;
* como organizar uma Collection.

---

## Próximo desafio: automatização

Depois de executar os testes manualmente, tente criar validações no próprio Postman.

Exemplo:

```javascript
pm.test("Status esperado", function () {
    pm.response.to.have.status(200);
});
```

Depois evolua para validações de:

* campos;
* valores;
* tipos;
* estrutura do Response;
* regras de negócio.

O Postman permite criar testes e organizar requisições em Collections.

---

## Boas práticas em testes de API

### 1. Conheça o contrato

Antes de testar, entenda:

* endpoint;
* método;
* parâmetros;
* headers;
* autenticação;
* Request;
* Response;
* comportamento esperado.

### 2. Teste cenários positivos e negativos

Não teste somente o caminho de sucesso.

Inclua:

* dados válidos;
* campos obrigatórios ausentes;
* dados inválidos;
* formatos incorretos;
* valores limite;
* autenticação inválida;
* recursos inexistentes;
* métodos não permitidos.

### 3. Não valide somente o Status Code

Um `200 OK` não significa automaticamente que o teste passou.

Valide também:

* Response Body;
* Headers;
* campos;
* valores;
* tipos;
* regras de negócio;
* mensagens;
* comportamento esperado.

### 4. Valide erros

Um erro também possui comportamento esperado.

Analise:

```text
Status Code
     +
Mensagem
     +
Estrutura
     +
Comportamento
```

### 5. Utilize dados de teste

Utilize dados controlados e apropriados para os testes.

Evite colocar em arquivos versionados:

* senhas;
* tokens;
* chaves de API;
* credenciais;
* dados pessoais reais.

O Postman recomenda proteger informações sensíveis, incluindo senhas e chaves de API.

### 6. Utilize variáveis

Evite repetir valores fixos.

Exemplo:

```text
{{base_url}}
{{token}}
{{pet_id}}
```

Isso facilita a reutilização dos testes.

### 7. Organize as requisições

Agrupe requisições relacionadas em Collections.

Exemplo:

```text
Petstore
├── Criar Pet
├── Consultar Pet
├── Alterar Pet
├── Excluir Pet
└── Cenários Negativos
```

### 8. Pense em regressão

Depois de uma alteração, execute novamente os testes relevantes.

O objetivo é verificar se o comportamento existente continua funcionando.

### 9. Automatize testes repetitivos

Se uma validação precisa ser executada várias vezes, considere automatizá-la.

O Postman possui recursos para execução de testes e Collections, além de recursos para integração com fluxos de automação.

### 10. Registre evidências

Durante um teste, registre informações suficientes para reproduzir e investigar o resultado.

Exemplos:

* Request;
* Response;
* Status Code;
* logs;
* captura de tela;
* vídeo;
* dados utilizados.

---

## Aplicação em QA

Um teste de API não deve responder apenas:

> "A API respondeu?"

A pergunta deve ser:

> **"A API respondeu corretamente para este cenário?"**

Um fluxo de validação pode ser:

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

## Exemplos de cenários

### Criar recurso

**Dado:** dados válidos.

**Quando:** enviar um POST.

**Então:** o recurso deve ser criado conforme o comportamento esperado.

### Campo obrigatório ausente

**Dado:** Request sem campo obrigatório.

**Quando:** enviar a requisição.

**Então:** a API deve retornar o tratamento esperado para dados inválidos.

### Recurso inexistente

**Dado:** identificador inexistente.

**Quando:** realizar uma consulta.

**Então:** a API deve retornar o comportamento esperado para recurso não encontrado.

### Alteração

**Dado:** recurso existente.

**Quando:** alterar um campo.

**Então:** consultar novamente e verificar se a alteração foi aplicada.

### Exclusão

**Dado:** recurso existente.

**Quando:** excluir.

**Então:** consultar novamente e validar o comportamento após a exclusão.

---

## Glossário

Para consultar os principais conceitos:

[`terms.md`](./terms.md)

O arquivo contém definições de:

* API;
* REST;
* HTTP;
* Request;
* Response;
* Endpoint;
* JSON;
* Headers;
* Parameters;
* Status Codes;
* autenticação;
* Postman;
* Collections;
* testes;
* integração;
* automação;
* CI/CD.

---

## Material complementar

### Postman

O guia oficial do Postman apresenta o envio da primeira requisição, criação de Collection e criação de um teste básico.

[Postman — Guia inicial](https://learning.postman.com/docs/getting-started/quick-start/)

### Postman Echo

[Postman Echo — documentação](https://learning.postman.com/docs/developer/echo-api)

### Swagger Petstore

[Swagger Petstore — API para prática](https://petstore3.swagger.io/)

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
└── terms.md
```

| Arquivo     | Descrição                               |
| ----------- | --------------------------------------- |
| `README.md` | Guia de estudo, prática e boas práticas |
| `terms.md`  | Glossário de termos de API e QA         |

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

O objetivo é sair da simples execução de requisições e desenvolver a capacidade de **analisar, validar e automatizar o comportamento de APIs**.

---

## Autora

**Erica de Souza**

QA Analyst com foco em qualidade de software, testes de API, automação e aplicações de Inteligência Artificial.

---

> Material desenvolvido para estudo, consulta e prática de testes de API com foco em QA.
