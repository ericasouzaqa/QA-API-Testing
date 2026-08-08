# Termos de API e QA

Dicionário de consulta rápida sobre **API, HTTP, Postman e testes de software**.

---

# 1. Fundamentos de API

### API

Application Programming Interface.

Conjunto de regras que permite a comunicação entre sistemas ou componentes.

### API REST

Estilo arquitetural utilizado para construção de serviços web baseado, entre outros princípios, nos recursos e no protocolo HTTP.

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

Formato de dados utilizado com frequência na comunicação entre APIs.

Exemplo:

```json
{
  "name": "Erica",
  "email": "erica@email.com"
}
```

---

# 2. HTTP

### HTTP

Protocolo utilizado para comunicação entre clientes e servidores na web.

### GET

Utilizado normalmente para consultar dados.

### POST

Utilizado normalmente para criar um recurso ou enviar dados para processamento.

### PUT

Utilizado normalmente para substituir ou atualizar completamente um recurso.

### PATCH

Utilizado normalmente para atualizar parcialmente um recurso.

### DELETE

Utilizado normalmente para remover um recurso.

### HEAD

Semelhante ao GET, mas utilizado para obter os headers da resposta sem o conteúdo do body.

### OPTIONS

Utilizado para consultar as opções ou métodos suportados para um recurso.

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

Exemplo:

```json
{
  "name": "Erica"
}
```

### Query Parameter

Parâmetro enviado na URL após `?`.

Exemplo:

```text
/users?status=active
```

### Path Parameter

Valor utilizado como parte do caminho do recurso.

Exemplo:

```text
/users/123
```

Nesse caso:

```text
123
```

é o identificador do usuário.

### Header

Informação enviada nos cabeçalhos da requisição ou resposta.

Exemplo:

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

Exemplo:

```json
{
  "id": 1,
  "name": "Erica"
}
```

### Response Header

Informações adicionais enviadas nos cabeçalhos da resposta.

---

# 5. Status Codes

Os códigos HTTP indicam o resultado geral de uma requisição.

## 1xx — Informativo

Indica informações relacionadas ao processamento da requisição.

## 2xx — Sucesso

### 200 OK

Requisição processada com sucesso.

### 201 Created

Recurso criado com sucesso.

### 202 Accepted

Requisição aceita para processamento, sem indicar necessariamente que o processamento foi concluído.

### 204 No Content

Requisição processada com sucesso, sem conteúdo no Response Body.

## 3xx — Redirecionamento

Indica que são necessárias ações adicionais para completar a requisição.

## 4xx — Erro do cliente

Indica que existe algum problema relacionado à requisição.

### 400 Bad Request

Requisição inválida.

### 401 Unauthorized

A requisição não possui autenticação válida ou adequada.

### 403 Forbidden

O servidor entendeu a requisição, mas não permite a operação solicitada.

### 404 Not Found

Recurso não encontrado.

### 405 Method Not Allowed

O método HTTP utilizado não é permitido para o recurso.

### 409 Conflict

A requisição entra em conflito com o estado atual do recurso.

### 422 Unprocessable Content

A requisição possui estrutura compreensível, mas não pode ser processada devido aos dados enviados ou às regras aplicadas.

### 429 Too Many Requests

Muitas requisições foram realizadas em determinado período ou limite.

## 5xx — Erro do servidor

Indica falha no processamento pelo servidor.

### 500 Internal Server Error

Erro interno do servidor.

### 502 Bad Gateway

Um servidor atuando como gateway ou proxy recebeu uma resposta inválida de outro servidor.

### 503 Service Unavailable

Serviço temporariamente indisponível.

### 504 Gateway Timeout

O servidor atuando como gateway ou proxy não recebeu uma resposta dentro do tempo esperado.

---

# 6. Autenticação e autorização

### Authentication

Processo utilizado para verificar a identidade de quem está realizando uma requisição.

### Authorization

Processo utilizado para determinar se uma identidade autenticada possui permissão para executar determinada ação.

### API Key

Chave utilizada para identificar ou autorizar o acesso a uma API.

### Bearer Token

Token enviado normalmente no header `Authorization`.

Exemplo:

```text
Authorization: Bearer <token>
```

### Basic Authentication

Método de autenticação baseado em usuário e senha enviados em uma credencial codificada.

---

# 7. Postman

### Postman

Ferramenta utilizada para criar, enviar e testar requisições de APIs.

### Collection

Conjunto organizado de requisições.

Exemplo:

```text
Usuários
├── Criar
├── Consultar
├── Alterar
└── Excluir
```

### Environment

Conjunto de variáveis utilizadas para representar configurações de determinado ambiente.

Exemplo:

```text
base_url
token
user_id
```

### Variable

Valor reutilizável dentro de requisições, scripts ou ambientes.

Exemplo:

```text
{{base_url}}
```

### Collection Runner

Recurso utilizado para executar várias requisições de uma Collection.

### Script

Código executado no contexto de uma requisição ou Collection para automatizar comportamentos e validações.

### Teste no Postman

Validação automatizada executada após uma requisição.

Exemplo:

```javascript
pm.test("Status esperado", function () {
    pm.response.to.have.status(200);
});
```

### Mock Server

Recurso que simula o comportamento de uma API para permitir testes e desenvolvimento sem depender do servidor real.

---

# 8. Testes de API

### Teste de API

Processo de verificar se uma API funciona conforme o comportamento esperado.

Pode envolver validação de:

* Request;
* Response;
* Status Code;
* Headers;
* Body;
* regras de negócio;
* autenticação;
* integrações.

### Teste positivo

Valida o comportamento esperado utilizando dados válidos.

### Teste negativo

Valida o comportamento da aplicação diante de dados inválidos ou condições não esperadas.

### Teste funcional

Verifica se uma funcionalidade executa conforme os requisitos.

### Teste de integração

Verifica a comunicação entre componentes, serviços ou sistemas.

### Teste de regressão

Verifica se alterações realizadas não introduziram problemas em comportamentos existentes.

### Teste ponta a ponta

Valida um fluxo completo da aplicação envolvendo múltiplos componentes ou endpoints.

### Teste de contrato

Verifica se a comunicação entre sistemas respeita o contrato definido para a API.

### Teste de desempenho

Avalia o comportamento da API sob diferentes condições de carga, considerando métricas como tempo de resposta, volume e disponibilidade.

---

# 9. Conceitos de teste

### Cenário de teste

Situação definida para verificar determinado comportamento.

### Caso de teste

Conjunto de condições, dados, passos e resultados esperados utilizados para validar uma funcionalidade.

### Resultado esperado

Comportamento que deveria ocorrer durante a execução.

### Resultado obtido

Comportamento observado durante o teste.

### Evidência

Registro utilizado para demonstrar o resultado da execução.

Exemplos:

* captura de tela;
* Request;
* Response;
* log;
* relatório;
* vídeo.

### Caso positivo

Cenário em que os dados e condições atendem ao comportamento esperado.

### Caso negativo

Cenário em que dados inválidos, incompletos ou condições específicas são utilizados para verificar o tratamento da aplicação.

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

# 10. Integração

### Integração

Comunicação entre componentes ou sistemas.

Exemplo:

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

Mecanismo pelo qual um sistema envia uma notificação para outro sistema quando determinado evento ocorre.

### Timeout

Situação em que uma operação não recebe resposta dentro do período esperado.

### Retry

Nova tentativa de executar uma operação após uma falha.

### Idempotência

Propriedade em que repetir determinada operação produz o mesmo efeito final, quando aplicável.

---

# 11. Documentação de API

### Swagger

Ferramentas e interfaces associadas ao ecossistema OpenAPI, frequentemente utilizadas para documentar e explorar APIs.

### OpenAPI

Especificação padronizada para descrever APIs HTTP de forma que pessoas e ferramentas possam compreender suas operações, parâmetros, respostas e outros elementos do contrato.

### Contrato da API

Definição do comportamento esperado da interface entre sistemas.

Pode especificar:

* endpoints;
* métodos;
* parâmetros;
* headers;
* autenticação;
* Request;
* Response;
* códigos de resposta.

---

# 12. Boas práticas

### Validação de Request

Verifique se o cliente envia exatamente os dados esperados.

### Validação de Response

Não valide somente o código HTTP.

Verifique também:

* estrutura;
* campos;
* valores;
* tipos;
* regras de negócio.

### Cenários negativos

Sempre que aplicável, teste:

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

### Evidências

Registre informações suficientes para reproduzir e investigar o resultado.

### Automação

Automatize testes repetitivos e relevantes.

### Regressão

Execute novamente os testes impactados por alterações.

---

# 13. Termos relacionados a automação

### Automação de testes

Uso de ferramentas e scripts para executar validações automaticamente.

### CI

Continuous Integration.

Prática de integrar alterações frequentemente e executar verificações automatizadas.

### CD

Continuous Delivery ou Continuous Deployment, dependendo do contexto.

Relaciona-se à automação das etapas de entrega e implantação.

### Pipeline

Sequência automatizada de etapas executadas durante processos como build, teste e entrega.

### GitHub Actions

Recurso de automação do GitHub utilizado para executar workflows, incluindo testes automatizados.

---

# 14. Checklist rápido para testes de API

Antes de finalizar um teste, verifique:

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

---

# Referências

* Postman — [Documentação oficial](https://learning.postman.com/docs/)
* Postman — [Testes de API](https://learning.postman.com/docs/tests-and-scripts/test-apis/test-apis/)
* Postman — [Execução e automação de testes](https://learning.postman.com/docs/tests-and-scripts/run-tests/run-tests)
* Postman — [Testes de integração](https://learning.postman.com/docs/tests-and-scripts/test-apis/integration-testing/)
* OpenAPI — [Especificação oficial](https://spec.openapis.org/oas/latest.html)
