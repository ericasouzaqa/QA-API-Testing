# QA API Glossary

Glossário prático de **API REST, HTTP, Postman e testes de API**, criado para estudo, consulta e aplicação em QA.

O objetivo é ajudar quem está começando a entender os principais conceitos envolvidos na comunicação entre sistemas e na validação de APIs.

## 🎯 Objetivo

Este projeto serve como material de apoio para:

* entender conceitos de APIs;
* interpretar Requests e Responses;
* utilizar o Postman;
* analisar códigos HTTP;
* estruturar cenários de teste;
* investigar erros;
* aplicar boas práticas de testes de API.

## 📚 Como estudar

A melhor forma de utilizar este material é consultar os termos conforme você avança nos estudos.

Uma sequência recomendada:

```text
HTTP
  ↓
API
  ↓
Endpoint
  ↓
Request
  ↓
Response
  ↓
Status Code
  ↓
Autenticação
  ↓
Postman
  ↓
Testes de API
```

Depois, avance para conceitos de integração, automação e testes de cenários completos.

## 🔎 Principais conceitos

O glossário aborda termos relacionados a:

### API

* API
* API REST
* Endpoint
* URI
* Recurso
* JSON
* Request
* Response

### HTTP

* GET
* POST
* PUT
* PATCH
* DELETE
* HEAD
* OPTIONS
* Headers
* Body
* Query Parameters
* Path Parameters
* Status Codes

### Autenticação e segurança

* Authentication
* Authorization
* API Key
* Bearer Token
* Basic Authentication

### Postman

* Collection
* Environment
* Variables
* Scripts
* Testes
* Collection Runner
* Mock Server

### Testes

* Teste positivo
* Teste negativo
* Teste funcional
* Teste de integração
* Teste de regressão
* Teste de contrato
* Teste ponta a ponta
* Teste de desempenho

## 🧪 Como aplicar em QA

Durante um teste de API, não valide somente se existe uma resposta.

Analise o fluxo completo:

```text
Request
   ↓
Processamento
   ↓
Response
   ↓
Validação
   ↓
Resultado
```

### No Request

Verifique:

* método HTTP;
* endpoint;
* parâmetros;
* headers;
* autenticação;
* body;
* formato dos dados.

### No Response

Verifique:

* código HTTP;
* headers;
* estrutura do body;
* tipos dos campos;
* valores retornados;
* mensagens;
* regras de negócio.

O Postman permite testar código de resposta, headers e dados do body por meio de scripts de teste.

## ✅ Boas práticas em testes de API

### 1. Conheça o contrato

Antes de testar, entenda o comportamento esperado da API.

Verifique:

* endpoint;
* método;
* parâmetros;
* headers;
* autenticação;
* Request;
* Response;
* códigos esperados.

Quando disponível, uma especificação OpenAPI pode servir como referência do contrato da API.

### 2. Teste cenários positivos e negativos

Não valide somente o fluxo de sucesso.

Inclua cenários como:

* dados válidos;
* campos obrigatórios ausentes;
* dados inválidos;
* formatos incorretos;
* valores limite;
* autenticação inválida;
* recurso inexistente;
* método não permitido.

### 3. Não valide somente o Status Code

Um `200 OK` não garante que o comportamento esteja correto.

Valide também:

* estrutura do Response;
* dados retornados;
* tipos dos campos;
* regras de negócio;
* mensagens;
* headers;
* tempo de resposta, quando aplicável.

### 4. Valide o tratamento de erros

Verifique se a API retorna o comportamento esperado para situações inválidas.

Analise:

```text
Código HTTP
     +
Mensagem
     +
Estrutura do erro
     +
Comportamento da aplicação
```

### 5. Utilize dados de teste adequados

Evite utilizar dados reais ou informações sensíveis desnecessariamente.

Não versionar:

* senhas;
* tokens;
* chaves de API;
* credenciais;
* informações pessoais reais.

O Postman recomenda utilizar mecanismos próprios para armazenar informações sensíveis, como o Vault, em vez de inserir segredos diretamente nas requisições.

### 6. Organize as requisições

Utilize Collections para agrupar requisições relacionadas.

Exemplo:

```text
Usuários
├── Criar usuário
├── Consultar usuário
├── Alterar usuário
└── Excluir usuário
```

Collections também podem ser utilizadas para executar conjuntos de testes e organizar fluxos.

### 7. Utilize variáveis

Evite repetir valores fixos.

Exemplo:

```text
{{base_url}}
{{token}}
{{user_id}}
```

Isso facilita a reutilização dos testes em diferentes ambientes.

### 8. Pense em regressão

Depois de uma alteração, execute novamente os testes relevantes para verificar se comportamentos existentes continuam funcionando.

Testes de regressão ajudam a identificar problemas introduzidos por mudanças na aplicação.

### 9. Automatize o que for repetitivo

Testes repetitivos e importantes podem ser automatizados.

O Postman permite executar testes manualmente, por Collections, em agendamentos e também integrá-los a pipelines de CI/CD.

### 10. Teste integrações

Quando uma API depende de outros serviços, valide também a comunicação entre os componentes.

Exemplo:

```text
Frontend
   ↓
API
   ↓
Serviço externo
   ↓
Banco de dados
   ↓
Response
```

Testes de integração verificam justamente se os componentes conseguem trabalhar juntos e se os dados fluem corretamente entre eles.

## 🔬 Exemplos de cenários

### Criar usuário

**Dado:** dados válidos.

**Quando:** enviar `POST /users`.

**Então:** validar:

* status esperado;
* ID gerado;
* dados retornados;
* estrutura do Response.

### Criar usuário sem campo obrigatório

**Dado:** Request sem um campo obrigatório.

**Quando:** enviar a requisição.

**Então:** validar:

* código HTTP;
* mensagem;
* estrutura do erro;
* ausência de criação indevida.

### Consultar recurso inexistente

**Dado:** identificador inexistente.

**Quando:** enviar `GET`.

**Então:** validar o comportamento esperado para o recurso inexistente.

### Fluxo completo

Um teste ponta a ponta pode encadear várias requisições:

```text
Criar recurso
     ↓
Obter recurso
     ↓
Alterar recurso
     ↓
Consultar novamente
     ↓
Excluir recurso
     ↓
Confirmar exclusão
```

O Postman permite organizar requisições em sequência e utilizar dados de uma resposta em requisições seguintes.

## 📊 Tipos de teste

### Funcional

Verifica se a API executa corretamente uma funcionalidade.

### Integração

Verifica a comunicação entre componentes e sistemas.

### Regressão

Verifica se alterações não introduziram novos problemas.

### Ponta a ponta

Valida um fluxo completo envolvendo diferentes componentes.

### Desempenho

Avalia comportamento sob diferentes volumes de requisições, observando métricas como tempo de resposta, disponibilidade e capacidade de processamento.

## 🛠️ Ferramentas relacionadas

* Postman
* Swagger / OpenAPI
* Insomnia
* JMeter
* Git
* GitHub Actions

## 📖 Glossário completo

Consulte:

[`terms.md`](./terms.md)

## 📌 Próximos estudos

Depois de compreender os conceitos deste glossário, uma sequência natural de aprendizado é:

```text
Fundamentos de API
        ↓
Postman
        ↓
Testes positivos e negativos
        ↓
Testes de integração
        ↓
Automação
        ↓
CI/CD
        ↓
Testes de desempenho
```

## 👩‍💻 Autora

**Erica de Souza**

QA Analyst com foco em qualidade de software, testes de API, automação e aplicações de Inteligência Artificial.

---

> Material desenvolvido para estudo, consulta e aplicação prática de conceitos de API e QA.
