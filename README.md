# Da Entrega ao Teste — Triagem para QA

Ferramenta web autocontida que transforma o texto (ou PDF/imagens) de uma entrega — user story, card, ticket, funcionalidade — em triagem estruturada, cenários de teste, código de automação pronto e manual de usuário, usando IA.

Arquivo único em HTML/JS, sem backend, sem instalação. Abre direto no navegador.

## O que ela faz

1. **Entrada** — cole o texto da entrega e/ou anexe um PDF e imagens (prints, mockups). Se o conteúdo tiver mais de um item de entrega (vários cards no mesmo documento), cada um é identificado separadamente.
2. **Triagem** — quebra cada item em descrição, critérios de aceite, impactos, pontos de atenção e dados insuficientes. Dá pra reformular item por item antes de seguir.
3. **Cenários** — gera checklist e cenários Gherkin por item. Para itens de chatbot de IA ou app mobile, gera antes um guia de preparação de ambiente (pré-requisitos, passos, o que pedir a quem solicitou o teste). Também gera sob demanda código pronto (não executa nada sozinho) de:
   - **Cypress** — automação de interface
   - **Postman** — validação de API
   - **k6** — teste de performance
4. **Manual** — gera um manual do usuário por item, em linguagem de usuário final, pronto para virar artigo de base de conhecimento.

Também exporta checklist + Gherkin de todos os itens gerados em uma planilha `.xlsx`.

## Como usar

Basta abrir o arquivo `qa_triagem.html` em qualquer navegador. Não precisa de servidor, instalação nem configuração — dentro do ambiente do Claude funciona direto.

## Publicando no GitHub Pages

1. Suba o arquivo `qa_triagem.html` para um repositório (pode ser o único arquivo, ou renomeie para `index.html`).
2. Em **Settings → Pages**, selecione a branch e a pasta onde o arquivo está.
3. Acesse a URL gerada pelo GitHub Pages.

### Sobre a chave de API

Fora do ambiente do Claude, cada chamada de IA precisa de autenticação própria. Ao abrir a ferramenta publicada, clique no ícone ⚙️ no menu lateral e cole uma chave de API da Anthropic (gerada em [console.anthropic.com](https://console.anthropic.com)).

- A chave fica salva **apenas no navegador de quem está usando** (`sessionStorage`), nunca é enviada a nenhum lugar além da própria API da Anthropic.
- Cada pessoa que for usar a ferramenta publicada precisa da própria chave — não há uma chave compartilhada embutida no código.

## Privacidade e escopo

- A ferramenta **não se conecta a nenhum sistema, API ou ferramenta interna**. A única chamada de rede é direto do navegador para `api.anthropic.com`.
- O código gerado para Cypress/Postman/k6 é sempre estático — usa placeholders comentados no lugar de URLs, seletores e endpoints reais. Nada é executado ou disparado automaticamente.
- Não há armazenamento em nuvem: todo o processamento acontece na sessão do navegador. Fechou a aba, perdeu o progresso (exceto a chave de API, que fica salva para a próxima sessão).

## Estrutura técnica

- Arquivo único (`qa_triagem.html`): HTML + CSS + JavaScript puro, sem build, sem dependências instaladas.
- Biblioteca externa: [SheetJS](https://sheetjs.com/) via CDN, usada apenas para gerar o `.xlsx` de exportação.
- Chamadas de IA feitas diretamente para a API de mensagens da Anthropic (`claude-sonnet-4-6`).

## Limitações conhecidas

- Cada chamada de IA tem um limite de tamanho de resposta; itens muito extensos ou anexos muito grandes podem gerar respostas cortadas — a ferramenta avisa quando isso acontece e permite tentar novamente.
- Não faz parsing manual de PDF: o próprio modelo lê o conteúdo do arquivo anexado.
- Cópia e download automático podem ser bloqueados por restrições do navegador; nesses casos, a ferramenta abre uma caixa de texto para copiar manualmente.
