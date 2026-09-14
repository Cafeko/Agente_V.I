# LLM Wiki

Uma base de conhecimento persistente, versionada no Git e gerenciada por um agente de IA com acesso a arquivos e Git.

## Começo rápido

1. Clone o repositório:

   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd <DIRETORIO_DO_REPOSITORIO>
   ```

2. Abra o diretório em um ambiente de agente com capacidade de ler, buscar, criar e editar arquivos, além de consultar Git.

3. Na primeira interação, instrua o agente:

   ```text
   Leia AGENTS.md e wiki/index/navigation_index.md. Faça uma inspeção inicial da Wiki sem alterar arquivos. Depois, aguarde minha solicitação.
   ```

4. Forneça uma pergunta, fonte, arquivo ou informação para o agente incorporar.

## Papel do agente

O agente deve seguir integralmente [`AGENTS.md`](AGENTS.md). Ele é responsável por consultar e manter a Wiki, preservar proveniência, evitar duplicações, criar ou atualizar conhecimento derivado, manter relações e atualizar o índice de navegação.

A LLM toma as decisões de manutenção. O ambiente precisa fornecer somente ferramentas de leitura, busca, escrita, movimentação de arquivos e Git. Não há script, provedor de LLM ou modelo obrigatório neste repositório.

## Estrutura

```text
wiki/
├── sources/       # metadados e fontes originais
├── subjects/      # assuntos ou entidades persistentes
├── user_input/    # informações fornecidas diretamente pelo usuário
├── knowledge/     # summaries, comparisons e syntheses
└── index/         # navegação da Wiki
```

A descrição detalhada, formatos de IDs, regras de privacidade e fluxos de manutenção estão em `AGENTS.md`.

## Dados privados e credenciais

- Fontes privadas devem ficar em `wiki/sources/files/private/`; o conteúdo dessa pasta não é versionado por padrão.
- Não inclua chaves de API, tokens ou arquivos `.env` no repositório.
- Use [`.env.example`](.env.example) apenas como referência de configuração local, sem valores secretos.

## Git

Revise o estado antes de compartilhar alterações:

```bash
git status
git diff
```

O agente pode criar commits somente quando a política do ambiente ou a pessoa responsável autorizar.
