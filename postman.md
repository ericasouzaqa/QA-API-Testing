# Guia de Postman para QA

Guia prático para aprender a utilizar o Postman na criação, execução e validação de testes de API.

O objetivo é começar pelos conceitos básicos e evoluir até Collections, variáveis, scripts, autenticação e automação.

---

## 1. O que é o Postman?

O Postman é uma ferramenta utilizada para criar e enviar requisições para APIs, analisar respostas e criar testes automatizados.

Ele permite trabalhar com:

* requisições HTTP;
* parâmetros;
* headers;
* autenticação;
* Body;
* Collections;
* variáveis;
* scripts;
* testes;
* execução de Collections;
* automação.

---

## 2. Instalação

Você pode utilizar o Postman pelo aplicativo ou pela versão web.

[Postman](https://www.postman.com/downloads/)

Para sincronizar trabalhos, organizar Collections e utilizar outros recursos, é possível criar uma conta gratuita.

---

# 3. Criando a primeira requisição

Abra o Postman e crie uma nova requisição.

Utilize:

```http
GET https://postman-echo.com/get
```

Clique em:

```text
Send
```

O Postman enviará a requisição e apresentará o Response.

O próprio guia inicial oficial utiliza esse exemplo para demonstrar o primeiro Request.

---

# 4. O que analisar?

Depois de executar uma requisição, observe:

### Status Code

Indica o resultado geral da requisição.

### Response Body

Contém os dados retornados.

### Headers

Contêm informações adicionais da resposta.

### Tempo de resposta

Ajuda a identificar comportamentos de desempenho.

Como QA, não analise apenas o Status Code.

---

# 5. Testando parâmetros

Utilize:

```http
GET https://postman-echo.com/get?nome=Erica
```

Observe onde o parâmetro aparece no Response.

Depois tente adicionar outro:

```http
GET https://postman-echo.com/get?nome=Erica&area=QA
```

Compare os resultados.

---

# 6. Criando uma Collection

Uma Collection permite organizar requisições relacionadas.

Exemplo:

```text
Petstore
├── Criar Pet
├── Consultar Pet
├── Alterar Pet
├── Excluir Pet
└── Cenários Negativos
```

Collections podem armazenar requisições, exemplos, testes, variáveis e configurações relacionadas.

---

# 7. Variáveis

Variáveis evitam repetir informações.

Exemplo:

```text
{{base_url}}
{{pet_id}}
{{token}}
```

Em vez de:

```text
https://petstore3.swagger.io/api/v3
```

utilize:

```text
{{base_url}}
```

Isso facilita a manutenção dos testes.

---

# 8. Environment

Um Environment permite trabalhar com valores diferentes para diferentes ambientes.

Exemplo:

```text
TST
base_url = https://teste.exemplo.com

HOM
base_url = https://homologacao.exemplo.com

PROD
base_url = https://api.exemplo.com
```

Assim, a mesma requisição pode utilizar diferentes configurações.

---

# 9. GET

Utilizado normalmente para consultar dados.

Exemplo:

```http
GET /pet/{petId}
```

Valide:

* Status Code;
* ID;
* campos;
* valores;
* tipos;
* estrutura.

---

# 10. POST

Utilizado normalmente para criar recursos ou enviar dados.

Exemplo:

```http
POST /pet
```

Body:

```json
{
  "id": 12345,
  "name": "Rex",
  "status": "available"
}
```

Valide:

* Status Code;
* recurso criado;
* dados retornados;
* estrutura;
* regras de negócio.

---

# 11. PUT

Utilizado normalmente para atualizar ou substituir um recurso.

Exemplo:

```http
PUT /pet
```

Altere um campo e consulte o recurso novamente.

Pergunta de QA:

> A alteração foi realmente aplicada?

---

# 12. DELETE

Utilizado normalmente para remover um recurso.

Exemplo:

```http
DELETE /pet/12345
```

Depois consulte novamente:

```http
GET /pet/12345
```

Valide o comportamento após a exclusão.

---

# 13. Headers

Headers transportam informações adicionais.

Exemplo:

```text
Content-Type: application/json
```

Outro exemplo:

```text
Authorization: Bearer {{token}}
```

Como QA, verifique se os headers obrigatórios estão presentes e corretos.

---

# 14. Body

O Body contém os dados enviados em determinadas requisições.

Exemplo:

```json
{
  "name": "Rex",
  "status": "available"
}
```

Valide:

* campos obrigatórios;
* tipos;
* formatos;
* valores;
* regras de negócio.

---

# 15. Autenticação

APIs podem exigir autenticação.

Exemplos:

* API Key;
* Bearer Token;
* Basic Authentication.

No Postman, utilize a aba **Authorization** para configurar o mecanismo esperado pela API.

A coleção oficial de aprendizado do Postman utiliza API Key como parte dos exercícios de autenticação.

---

# 16. Scripts

O Postman permite utilizar JavaScript para adicionar lógica antes ou depois das requisições.

Existem dois momentos principais:

```text
Pre-request Script
        ↓
Request
        ↓
Post-response Script
```

Scripts podem preparar dados, gerar valores dinâmicos, armazenar informações e executar validações.

---

# 17. Primeiro teste automatizado

Depois de enviar uma requisição, adicione um teste:

```javascript
pm.test("Status esperado", function () {
    pm.response.to.have.status(200);
});
```

Execute novamente a requisição.

O resultado aparecerá na área de testes.

O guia oficial do Postman apresenta esse mesmo conceito para validar o Status Code de uma resposta.

---

# 18. Validando um campo

Exemplo:

```javascript
const response = pm.response.json();

pm.test("Nome está presente", function () {
    pm.expect(response.name).to.exist;
});
```

---

# 19. Validando um valor

```javascript
const response = pm.response.json();

pm.test("Status correto", function () {
    pm.expect(response.status).to.equal("available");
});
```

---

# 20. Validando tipo

```javascript
const response = pm.response.json();

pm.test("ID é numérico", function () {
    pm.expect(response.id).to.be.a("number");
});
```

---

# 21. Cenário negativo

Testes negativos são fundamentais.

Exemplo:

```text
GET /pet/{id_inexistente}
```

Valide:

```text
Status Code
Mensagem
Estrutura do erro
Comportamento esperado
```

Não presuma que qualquer erro representa um comportamento correto.

O resultado deve ser comparado com o contrato e com a regra esperada da API.

---

# 22. Request chaining

Request chaining significa utilizar dados obtidos em uma requisição em outra.

Exemplo:

```text
Criar Pet
   ↓
ID retornado
   ↓
Consultar Pet usando o ID
   ↓
Alterar Pet
   ↓
Excluir Pet
```

Uma variável pode armazenar o ID retornado:

```javascript
const response = pm.response.json();

pm.collectionVariables.set("pet_id", response.id);
```

Depois:

```text
GET /pet/{{pet_id}}
```

A coleção oficial do Postman utiliza esse conceito para passar dados entre requisições.

---

# 23. Testando o Swagger Petstore

Acesse:

[Swagger Petstore](https://petstore3.swagger.io/)

A API possui operações de criação, consulta, alteração e exclusão de pets.

Monte uma Collection:

```text
Petstore
├── 01 - Criar Pet
├── 02 - Consultar Pet
├── 03 - Alterar Pet
├── 04 - Consultar Alteração
├── 05 - Excluir Pet
└── 06 - Consultar Após Exclusão
```

---

# 24. Exercício prático

### Etapa 1

Crie um pet.

### Etapa 2

Capture o ID retornado.

### Etapa 3

Armazene o ID em uma variável.

### Etapa 4

Consulte o pet usando a variável.

### Etapa 5

Altere o pet.

### Etapa 6

Consulte novamente.

### Etapa 7

Exclua o pet.

### Etapa 8

Consulte novamente e valide o comportamento esperado.

---

# 25. Coleção oficial do Postman

Depois dos exercícios básicos, avance para a coleção:

[Get Started with API Testing — Postman](https://www.postman.com/devrel/postman-community-challenge/folder/4pjyd3k/get-started-with-api-testing)

Essa coleção oficial utiliza uma API bancária fictícia e apresenta exercícios sobre:

* testes simples;
* scripts;
* asserções;
* validação de dados;
* autenticação;
* variáveis;
* encadeamento de requisições;
* validações mais específicas.

Cada requisição possui uma tarefa prática para reforçar o conceito apresentado.

---

# 26. O que estudar nessa coleção

A ordem recomendada é:

```text
Testes básicos
      ↓
Scripts
      ↓
Asserções
      ↓
Variáveis
      ↓
Autenticação
      ↓
Request chaining
      ↓
Validação de dados
      ↓
Automação
```

A própria coleção apresenta exercícios progressivos para esses conceitos.

---

# 27. Executando uma Collection

Depois de criar seus testes, você pode executar uma Collection inteira.

Isso permite:

* executar várias requisições;
* executar testes em sequência;
* repetir cenários;
* analisar resultados.

O Postman também oferece execução manual, agendada e integração com CI/CD por meio de recursos como Postman CLI e Newman.

---

# 28. Desafio final

Crie uma Collection chamada:

```text
QA API Tests
```

Organize:

```text
QA API Tests
│
├── 01 - GET
├── 02 - POST
├── 03 - PUT
├── 04 - DELETE
├── 05 - Cenários Negativos
└── 06 - Testes Automatizados
```

Para cada requisição, tente validar:

```text
[ ] Status Code
[ ] Response Body
[ ] Campos obrigatórios
[ ] Tipos
[ ] Valores
[ ] Regras de negócio
[ ] Cenário negativo
```

---

# 29. Checklist de aprendizado

Ao finalizar este guia, você deve saber:

```text
[ ] Criar uma requisição
[ ] Utilizar GET
[ ] Utilizar POST
[ ] Utilizar PUT
[ ] Utilizar DELETE
[ ] Configurar Headers
[ ] Trabalhar com Parameters
[ ] Configurar Body
[ ] Utilizar autenticação
[ ] Criar Collection
[ ] Criar variáveis
[ ] Utilizar Environment
[ ] Criar Scripts
[ ] Criar testes
[ ] Validar Status Code
[ ] Validar Response
[ ] Fazer Request chaining
[ ] Criar cenários negativos
[ ] Executar uma Collection
```

---

# Referências

[Documentação oficial do Postman](https://learning.postman.com/)

[Postman Quick Start](https://learning.postman.com/docs/getting-started/quick-start/)

[Postman — Get Started with API Testing](https://www.postman.com/devrel/postman-community-challenge/folder/4pjyd3k/get-started-with-api-testing)

[Postman Echo](https://learning.postman.com/docs/developer/echo-api)

[Swagger Petstore](https://petstore3.swagger.io/)
