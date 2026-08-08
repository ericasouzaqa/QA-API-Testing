# Termos de API e QA

Dicionário de consulta rápida sobre API, HTTP, Postman e testes de software.

---

# 1. Fundamentos de API

### API

Application Programming Interface.

Conjunto de regras que permite a comunicação entre sistemas ou componentes.

### API REST

Estilo arquitetural utilizado para construção de serviços web utilizando recursos e conceitos do protocolo HTTP.

### Endpoint

Endereço utilizado para acessar uma operação ou recurso de uma API.

Exemplo:

```text
GET /users
```

### Recurso

Elemento ou entidade manipulada pela API.

Exemplos:

```text
/users
/products
/orders
```

### URI

Identificador utilizado para identificar um recurso.

### JSON

Formato de dados frequentemente utilizado na comunicação entre APIs.

```json
{
  "name": "Erica",
  "email": "erica@email.com"
}
```

---

# 2. HTTP

### HTTP

Protocolo utilizado para comunicação entre clientes e servidores.

### GET

Utilizado normalmente para consultar dados.

### POST

Utilizado normalmente para criar recursos ou enviar dados para processamento.

### PUT

Utilizado normalmente para substituir ou atualizar um recurso.

### PATCH

Utilizado normalmente para atualizar parcialmente um recurso.

### DELETE

Utilizado normalmente para remover um recurso.

### HEAD

Solicita informações semelhantes às de uma requisição GET, mas sem o conteúdo do Response Body.

### OPTIONS

Permite consultar as opções ou métodos suportados por um recurso.

---

# 3. Request

### Request

Requisição enviada pelo cliente para a API.

Pode conter:

* método;
* URL;
* parâmetros;
* headers;
* autenticação;
* body.

### Request Body

Dados enviados no corpo da requisição.

### Query Parameter

Parâmetro enviado na URL.

```text
/users?status=active
```

### Path Parameter

Valor utilizado como parte do caminho do recurso.

```text
/users/123
```

### Header

Informação enviada no cabeçalho da requisição ou resposta.

```text
Content-Type: application/json
```

---

# 4. Response

### Response

Resposta enviada pela API após o processamento de uma requisição.

Pode conter:

* Status Code;
* Headers;
* Body.

### Response Body

Conteúdo retornado pela API.

### Response Header

Informações adicionais enviadas nos cabeçalhos da resposta.

---

# 5. Status Codes

## 2xx — Sucesso

### 200 OK

Requisição processada com sucesso.

### 201 Created

Recurso criado com sucesso.

### 202 Accepted

Requisição aceita para processamento.

### 204 No Content

Requisição processada com sucesso sem conteúdo no Response Body.

## 3xx — Redirecionamento

Indica que são necessárias ações adicionais para completar a requisição.

## 4xx — Erro do cliente

### 400 Bad Request

Requisição inválida.

### 401 Unauthorized

A requisição não possui autenticação válida ou adequada.

### 403 Forbidden

O servidor entendeu a requisição, mas não permite a operação solicitada.

### 404 Not Found

Recurso não encontrado.

### 405 Method Not Allowed

Método HTTP não permitido para o recurso.

### 409 Conflict

Conflito com o estado atual do recurso.

### 422 Unprocessable Content

A requisição é compreensível, mas os dados não podem ser processados.

### 429 Too Many Requests

Limite de requisições excedido.

## 5xx — Erro do servidor

### 500 Internal Server Error

Erro interno do servidor.

### 502 Bad Gateway

Resposta inválida recebida por um gateway ou proxy.

### 503 Service Unavailable

Serviço temporariamente indisponível.

### 504 Gateway Timeout

O gateway ou proxy não recebeu uma resposta dentro do tempo esperado.

---

# 6. Autenticação e autorização

### Authentication

Processo utilizado para verificar a identidade de quem realiza uma requisição.

### Authorization

Processo utilizado para determinar quais ações uma identidade autenticada pode executar.

### API Key

Chave utilizada para identificação ou autorização de acesso a uma API.

### Bearer Token

Token enviado normalmente no header `Authorization`.

```text
Authorization: Bearer <token>
```

### Basic Authentication

Método de autenticação baseado em usuário e senha.

---

# 7. Postman

### Postman

Ferramenta utilizada para criar, enviar, organizar e testar requisições de APIs. O Postman suporta diferentes protocolos, incluindo HTTP.

### Collection

Conjunto organizado de requisições.

Collections também podem conter scripts, variáveis, autenticação, exemplos e testes.

### Environment

Conjunto de variáveis utilizado para representar configurações de determinado ambiente.

### Variable

Valor reutilizável em requisições, scripts ou ambientes.

### Collection Runner

Recurso utilizado para executar requisições de uma Collection.

### Script

Código JavaScript utilizado para adicionar lógica, preparar requisições ou validar respostas.

### Teste no Postman

Validação automatizada executada após uma requisição.

Exemplo:

```javascript
pm.test("Status esperado", function () {
    pm.response.to.have.status(200);
});
```

---

# 8. Testes de API

### Teste de API

Processo de verificar se uma API funciona conforme o comportamento esperado.

### Teste positivo

Utiliza dados válidos e condições esperadas.

### Teste negativo

Utiliza dados inválidos ou condições que devem ser tratadas pela aplicação.

### Teste funcional

Verifica se uma funcionalidade executa conforme os requisitos.

### Teste de integração

Verifica a comunicação entre componentes, serviços ou sistemas.

### Teste de regressão

Verifica se alterações não introduziram problemas em funcionalidades existentes.

### Teste ponta a ponta

Valida um fluxo completo envolvendo diferentes componentes.

### Teste de contrato

Verifica se a comunicação entre sistemas segue o contrato definido para a API.

### Teste de desempenho

Avalia o comportamento da API sob diferentes condições de carga.

---

# 9. Integração

### Integração

Comunicação entre componentes ou sistemas.

```text
Frontend
   ↓
API
   ↓
Serviço externo
   ↓
Banco de dados
```

### Webhook

Mecanismo pelo qual um sistema envia uma notificação para outro quando determinado evento ocorre.

### Timeout

Situação em que uma operação não recebe resposta dentro do período esperado.

### Retry

Nova tentativa de executar uma operação após uma falha.

### Idempotência

Propriedade na qual repetir determinada operação produz o mesmo efeito final, quando aplicável.

---

# 10. Documentação de API

### Swagger

Ferramentas e interfaces associadas ao ecossistema OpenAPI, frequentemente utilizadas para documentar e explorar APIs.

### OpenAPI

Especificação utilizada para descrever APIs HTTP, incluindo operações, parâmetros, respostas e outros elementos do contrato.

### Contrato da API

Definição do comportamento esperado da interface entre sistemas.

---

# 11. Conceitos de QA

### Cenário de teste

Situação definida para verificar determinado comportamento.

### Caso de teste

Conjunto de condições, dados, passos e resultados esperados utilizados para validar uma funcionalidade.

### Resultado esperado

Comportamento que deveria ocorrer.

### Resultado obtido

Comportamento observado durante o teste.

### Evidência

Registro utilizado para demonstrar o resultado da execução.

Exemplos:

* Request;
* Response;
* log;
* captura de tela;
* vídeo;
* relatório.

### Caso de borda

Cenário próximo aos limites definidos por uma regra.

Exemplo:

```text
Limite: 160 caracteres

159 → válido
160 → válido
161 → verificar comportamento esperado
```

---

# 12. Automação

### Automação de testes

Uso de ferramentas e scripts para executar validações automaticamente.

### CI

Continuous Integration.

Prática de integrar alterações frequentemente e executar verificações automatizadas.

### CD

Continuous Delivery ou Continuous Deployment, dependendo do contexto.

### Pipeline

Sequência automatizada de etapas como build, teste e entrega.

### GitHub Actions

Recurso do GitHub utilizado para automatizar workflows, incluindo execução de testes.

---

# 13. Boas práticas

### Validação de Request

Verifique se o cliente envia exatamente os dados esperados.

### Validação de Response

Valide:

* Status Code;
* estrutura;
* campos;
* valores;
* tipos;
* regras de negócio.

### Cenários negativos

Teste:

* dados inválidos;
* dados ausentes;
* valores limite;
* autenticação inválida;
* recursos inexistentes;
* métodos não permitidos.

### Dados sensíveis

Não versionar:

* senhas;
* tokens;
* chaves;
* credenciais;
* informações pessoais reais.

### Reutilização

Utilize Collections, variáveis e scripts para reduzir repetição.

### Regressão

Execute novamente os testes impactados por alterações.

---

# 14. Checklist rápido

```text
[ ] Endpoint correto
[ ] Método HTTP correto
[ ] Parâmetros corretos
[ ] Headers corretos
[ ] Autenticação válida
[ ] Body correto
[ ] Status Code esperado
[ ] Response Body correto
[ ] Regras de negócio validadas
[ ] Cenários negativos executados
[ ] Evidências registradas
[ ] Dados sensíveis protegidos
[ ] Regressão considerada
```
