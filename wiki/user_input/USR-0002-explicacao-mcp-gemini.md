---
id: USR-0002
type: user_input
title: "Explicação sobre MCP (Model Context Protocol) solicitada ao Gemini"
created: 2026-09-21
author: usuário (encaminhou resposta do Gemini)
privacy: public
related_subjects:
  - SUB-0008
---

# USR-0002 — Explicação sobre MCP solicitada ao Gemini

> Informação fornecida diretamente pelo usuário em 2026-09-21: texto gerado pelo **Gemini** a pedido do usuário para explicar o que é MCP. Registrado como `user_input` conforme `AGENTS.md:8` — distingue fato fornecido pelo usuário, opinião, interpretação e conteúdo gerado por IA externa. Não foi verificado como source editorial independente.

## Conteúdo encaminhado (transcrição literal fornecida)

O MCP (Model Context Protocol) é um protocolo de comunicação aberto inventado pela Anthropic no final de 2024 para resolver um problema crônico do desenvolvimento de Inteligência Artificial: a fragmentação das conexões.

Antes do MCP, se você quisesse que um assistente de IA consultasse seu banco de dados, lesse seus arquivos e buscasse algo no GitHub, era necessário escrever um código customizado (via Function Calling ou Tool Use) para cada uma dessas integrações. Se mudasse de cliente de IA (do Claude Desktop para o Cursor, por exemplo), era preciso refazer as integrações do zero.

A analogia da "Porta USB-C" — Imagine o MCP como o padrão USB-C da Inteligência Artificial:
- Antes do USB-C: Cada celular/aparelho tinha seu próprio carregador e cabo proprietário.
- Com o USB-C: Um único cabo conecta pendrives, monitores, teclados e carregadores a qualquer notebook.
- No MCP é a mesma coisa:
  - Os Clientes MCP (Hosts): Aplicativos como Claude Desktop, Cursor, VS Code (com extensões como Roo Code/Cline) e LM Studio atuam como a "entrada USB".
  - Os Servidores MCP (Servers): Pequenos programas leves que se conectam a um serviço específico (Google Drive, PostgreSQL, GitHub, BrasilAPI, Notícias, etc.).
  - A Magia: Qualquer Cliente que suporte MCP consegue usar qualquer Servidor MCP instantaneamente, sem precisar reescrever código.

Como o MCP funciona na prática? O protocolo define três tipos de capacidades principais que um servidor pode oferecer ao modelo:
1. Tools (Ferramentas): Ações que o modelo pode executar (ex.: "Criar uma issue no GitHub", "Buscar CEP no BrasilAPI", "Executar uma query SQL").
2. Resources (Recursos): Dados de leitura contínua ou arquivos que o modelo pode ler para contexto (ex.: "Ler o arquivo de log local", "Acessar o schema do banco").
3. Prompts: Modelos de instruções pré-definidos fornecidos pelo servidor para orientar a interação.

## Observação de proveniência

- Origem: resposta do Gemini, encaminhada pelo usuário; não é artigo, documentação oficial ou fonte primária verificada pela Wiki.
- Status: `user_input` — opinião/explicação gerada por IA externa, registrada como fornecida. Não tratada automaticamente como fato confirmado (`AGENTS.md:8`). Uso em subjects deve indicar que deriva de USR-0002, com distinção entre conhecimento da Wiki baseado em user input e conhecimento baseado em source verificada.
- Relacionado a: [SUB-0008](../subjects/SUB-0008-mcp-model-context-protocol.md) (derivação com marcação de origem) e [SUB-0003](../subjects/SUB-0003-criacomp-disciplina.md) (onde MCP já é mencionado nas aulas 05-06 via SRC-0005/SUM-0005).
