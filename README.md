# LLM Wiki

Uma base de conhecimento persistente, versionada no Git e mantida por um agente de IA.
Você pergunta ou entrega material; o agente registra, organiza e conecta o conhecimento.

## Como usar

1. Clone e abra num ambiente com agente:
   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd <DIRETORIO_DO_REPOSITORIO>
   ```
2. Diga ao agente:
   ```text
   Leia AGENTS.md e wiki/index/navigation_index.md. Faça uma inspeção inicial da Wiki sem alterar arquivos. Depois, aguarde minha solicitação.
   ```
3. Depois é só conversar:
   - **Perguntar** — ex.: "o que a Wiki sabe sobre X?" (ele responde só com o registrado)
   - **Adicionar** — envie PDF, link, anotações ou uma pergunta para pesquisar
   - **Pedir manutenção** — ex.: "faça uma manutenção" ou "faça commit e push"

## Como funciona

- Tudo mora em `wiki/`: `subjects/` (o que a Wiki sabe), `sources/` (de onde veio),
  `knowledge/` (resumos, comparações, sínteses), `user_input/` (o que você forneceu)
  e `index/navigation_index.md` (o mapa de tudo).
- Cada documento tem um ID (`SRC-`, `SUB-`, `SUM-`, `CMP-`, `SYN-`, `USR-`) e aponta
  para sua origem — qualquer informação pode ser rastreada até a fonte.
- O agente nunca inventa: se a Wiki não sabe, ele diz isso em vez de completar.
  Pesquisa externa só acontece se você pedir, e vem marcada como externa.
- Regras completas de operação, IDs e privacidade estão em [`AGENTS.md`](AGENTS.md).

## Estrutura

```text
wiki/
├── sources/       # metadados e fontes originais (public/ ou private/)
├── subjects/      # assuntos ou entidades persistentes
├── user_input/    # informações fornecidas diretamente pelo usuário
├── knowledge/     # summaries, comparisons e syntheses
└── index/         # navegação da Wiki
```

## Dados privados e credenciais

- Fontes privadas ficam em `wiki/sources/files/private/`; o conteúdo dessa pasta não é versionado por padrão.
- Não inclua chaves de API, tokens ou arquivos `.env` no repositório.
- Use [`.env.example`](.env.example) apenas como referência de configuração local, sem valores secretos.

## Git

Revise o estado antes de compartilhar alterações:

```bash
git status
git diff
```

O agente pode criar commits somente quando a política do ambiente ou a pessoa responsável autorizar.
