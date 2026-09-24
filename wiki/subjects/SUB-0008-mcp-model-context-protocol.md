---
id: SUB-0008
type: subject
title: "MCP — Model Context Protocol"
created: 2026-09-21
updated: 2026-09-24
transcripts_updated: 2026-09-24
sources:
  - SRC-0005
  - SRC-0015
  - SRC-0016
knowledge:
  - SUM-0005
  - SUM-0015
  - SUM-0016
user_input:
  - USR-0002
related_subjects:
  - SUB-0003
  - SUB-0007
---

# MCP — Model Context Protocol

> O que a Wiki sabe sobre MCP a partir de menção nas aulas CriaComp e de explicação fornecida pelo usuário via Gemini. **Nota de proveniência**: a explicação detalhada deriva exclusivamente de `USR-0002` (resposta do Gemini encaminhada), registrada como `user_input` — não como source editorial verificada. A Wiki distingue fato verificado de conteúdo fornecido pelo usuário (`AGENTS.md:8`).

## 1. Definição (conforme user input)

**Model Context Protocol (MCP)** é descrito em [USR-0002](../user_input/USR-0002-explicacao-mcp-gemini.md) como um **protocolo de comunicação aberto inventado pela Anthropic no final de 2024** para resolver a **fragmentação das conexões** entre assistentes de IA e serviços externos.

- **Problema antes do MCP**: cada integração exigia código customizado via *Function Calling* / *Tool Use* para cada serviço (ex. consultar banco, ler arquivos, buscar no GitHub). Ao trocar de cliente de IA (ex. do Claude Desktop para o Cursor), era preciso refazer as integrações do zero.

## 2. Analogia “Porta USB-C” (conforme USR-0002)

A explicação usa a analogia do USB-C para contrastar proprietário vs padrão único:

- **Antes do USB-C**: cada aparelho tinha carregador/cabo proprietário.
- **Com USB-C**: um cabo conecta pendrives, monitores, teclados e carregadores a qualquer notebook.
- **Transposição para MCP**:
  - **Clientes MCP (Hosts)**: aplicativos como **Claude Desktop, Cursor, VS Code (com extensões Roo Code/Cline) e LM Studio** atuam como a “entrada USB”.
  - **Servidores MCP (Servers)**: pequenos programas leves que se conectam a um serviço específico (**Google Drive, PostgreSQL, GitHub, BrasilAPI, Notícias**, etc.).
  - **Efeito**: qualquer Cliente que suporte MCP consegue usar qualquer Servidor MCP instantaneamente, sem reescrever código.

> Esta analogia e lista de exemplos são transcrição do user input; não foram verificadas contra documentação oficial do protocolo pela Wiki.

## 3. Como funciona — três capacidades do servidor (conforme USR-0002)

O protocolo define três tipos de capacidades que um servidor pode oferecer ao modelo:

1. **Tools (Ferramentas)**: ações que o modelo pode executar.
   - Exemplos citados: “Criar uma issue no GitHub”, “Buscar CEP no BrasilAPI”, “Executar uma query SQL”.

2. **Resources (Recursos)**: dados de leitura contínua ou arquivos que o modelo pode ler para contexto.
   - Exemplos citados: “Ler o arquivo de log local”, “Acessar o schema do banco”.

3. **Prompts**: modelos de instruções pré-definidos fornecidos pelo servidor para orientar a interação.

## 4. Menção nas aulas CriaComp (conhecimento verificado)

Em contraste com a explicação acima (user input), a Wiki possui menção verificada de MCP via [SRC-0005](../sources/metadata/SRC-0005-aulas-05-06-criacomp.md) / [SUM-0005](../knowledge/summaries/SUM-0005-aulas-05-06-criacomp.md) e registrada em [SUB-0003](SUB-0003-criacomp-disciplina.md:60):

- MCP é apresentado como **protocolo que dá ao agente o *quando* usar uma API, não só o como**; houve demo ao vivo nas aulas 05–06 com barreiras reais (robots.txt, recusa por privacidade), relacionado à discussão de autonomia e responsabilidade.

Essa menção é curta e não detalha especificação técnica; a explicação detalhada sobre Tools/Resources/Prompts vem apenas de USR-0002.

## 5. Vídeos indicados pelo usuário (fontes públicas por link)

### 5.1 SRC-0015 — Código Fonte TV: "MCP - Model Context Protocol (O USB das IAs)"

Vídeo público do canal **Código Fonte TV** (`@codigofontetv`), série "Dicionário do Programador", 12/08/2025 — [SRC-0015](../sources/metadata/SRC-0015-video-mcp-usb-das-ias.md) via [SUM-0015](../knowledge/summaries/SUM-0015-video-mcp-usb-das-ias.md), transcrição PT auto-gerada integral (393 trechos):

- **Definição**: protocolo da Anthropic (anunciado nov/2024) para conectar assistentes a dados/sistemas; virou padrão da indústria. Adoção citada: GitHub, Docker, Microsoft ("MCP Dev Days"), OpenAI (com suporte, sem citar Anthropic).
- **Arquitetura**: cliente (host/assistente) + servidores MCP como plugins (arquivos, banco, API de negócio), via JSON-RPC 2.0. Fluxo: pergunta → LLM + prompt com contexto → MCP consulta serviço real → resposta personalizada.
- **Componentes**: Tools (funções/endpoints com parâmetros), Resources (dados já no contexto, como apostila) e Prompt final (briefing com contexto + resources + tools; permite projetar comportamento por tarefa).
- **Benefícios**: sem código customizado por ferramenta; plug universal; escala plug-and-play; segurança centralizada (acesso/autenticação). Exemplo: "busca no banco e gera relatório" vale para PostgreSQL/MySQL/Mongo/legado.
- **Riscos e boas práticas**: vazamento é desafio real — caso GitHub com acesso a privados via MCP em públicos. Práticas: mínimo privilégio, atualizar libs, código limpo, linter, testar inputs maliciosos, engenharia de prompt, documentar tools, marcações somente-leitura, validar mensagens do cliente. Exemplo de código: prompt Python para resumo de locais do Google Maps com anti-injeção.

### 5.2 SRC-0016 — Augusto Galego: "MCP não é mágica"

Vídeo público de **Augusto Galego** (`@GutoGalego`) — [SRC-0016](../sources/metadata/SRC-0016-video-mcp-nao-e-magica.md) via [SUM-0016](../knowledge/summaries/SUM-0016-video-mcp-nao-e-magica.md), transcrição PT auto-gerada integral (318 trechos). Posição do autor, não fato da Wiki:

- **Tese**: "80% hype, 20% útil". Autor com 12 anos em software mostra instalação/uso real para separar hype do útil.
- **Definição dada**: "API entre aspas" para IAs (Claude Code, Codex, Cursor, Copilot) interagirem padronizado com arquivos, GitHub, Slack, Spotify, Figma. Plugin do Codex não é MCP, mas pode conter servidores MCP (wrapper com skills).
- **Demos**: instala via VS Code (`@mcp`, ex. GitHub) e Claude Code (colar comando, reload); GitHub MCP falhou por token e depois listou tools (create branch etc.); File System MCP organizou Downloads caótica em subpastas (com log para desfazer) — sem MCP faria via cd/ls/mkdir, com MCP fica mais controlado/delimitado. Reclamou do custo usando Opus.
- **O que ele usa**: GitHub (ler issues/PRs/reviews sem copiar/colar, combinado com skill que lista e resolve tarefas) e gerenciador de tasks/Linear; Slack só para puxar trechos (prefere copiar/colar por paranoia, não usa); e-mail/WhatsApp/browser-Puppeteer/Figma/Docker citados como condicionais. Conclusão: para fluxo centrado em código, só task manager/GitHub é útil; para Figma, muitos e-mails ou fluxos complexos fora do código, pode ser super útil.

## 6. Limites e como citar

- **Não confirmado como fato editorial**: por ser conteúdo gerado por IA externa e encaminhado, a Wiki registra em [USR-0002](../user_input/USR-0002-explicacao-mcp-gemini.md) sem atribuir-lhe status de source verificada.
- **Uso**: ao consultar “o que a Wiki sabe sobre MCP”, a resposta combina: (a) a explicação de USR-0002, explicitamente marcada como *informação fornecida pelo usuário via Gemini*, (b) a menção verificada das aulas (SRC-0005/SUM-0005), (c) a transcrição de SRC-0015/SUM-0015 (visão geral + arquitetura + boas práticas) e (d) a transcrição de SRC-0016/SUM-0016 (posição prática "80% hype", marcada como opinião da fonte).
- **Relações**: conecta-se a [SUB-0003](SUB-0003-criacomp-disciplina.md) (disciplina onde MCP foi demonstrado) e a [SUB-0007](SUB-0007-grandihc-br-2025-2035.md) (GC1 sobre novas abordagens teóricas/metodológicas e agência, onde protocolos como MCP são relevantes para distribuição de autonomia).

---

## Proveniência

- Explicação detalhada §§1–3 deriva de **USR-0002** (texto do Gemini encaminhado pelo usuário em 2026-09-21); **não** é conhecimento baseado em source verificada. Registrado como `user_input` com distinção exigida por `AGENTS.md:8`.
- Menção curta §4 deriva de **SRC-0005** via **SUM-0005**, integrada em **SUB-0003:60**.
- §5 deriva de **SRC-0015** via **SUM-0015** e **SRC-0016** via **SUM-0016** (transcrições PT auto-geradas integrais extraídas em 2026-09-24 via youtube-transcript-api). Ambas públicas por link, `local_file: none`.
- Nenhuma fonte primária oficial do MCP (documentação Anthropic) foi consultada nesta entrada; se necessária, deve ser adicionada como `SRC` futura e então este subject atualizado para fato verificado.
