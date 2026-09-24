---
id: SUM-0015
type: summary
source: SRC-0015
title: "Summary — MCP - Model Context Protocol (O USB das IAs) // Dicionário do Programador"
created: 2026-09-24
related_subjects:
  - SUB-0008
---

# O que esta fonte apresenta (SRC-0015)

> Síntese da transcrição PT auto-gerada extraída em 2026-09-24 (393 trechos, ~14,5 mil caracteres) + metadados oEmbed. Sem acréscimo externo; erros de transcrição preservados como incerteza de formulação.

## Metadados verificados

- Título: "MCP - Model Context Protocol (O USB das IAs) // Dicionário do Programador".
- Canal/autor: Código Fonte TV (`@codigofontetv`).
- Publicação indicada como 12/08/2025 em resultados de busca.
- URL: https://www.youtube.com/watch?v=deprLB_y6Ho

## Conteúdo (transcrição)

- **Definição**: MCP é protocolo criado pela Anthropic para conectar assistentes de IA a onde estão os dados/sistemas (repositórios, ferramentas de negócio, ambientes de desenvolvimento). Objetivo: respostas melhores e mais relevantes, inclusive em ambiente corporativo. Anunciado em novembro de 2024; virou padrão da indústria.
- **Adoção citada**: GitHub, Docker e outras lançaram servidores MCP; Microsoft tem evento "MCP Dev Days"; OpenAI demorou mas dá suporte nas ferramentas, sem citar a Anthropic na documentação.
- **Problema que resolve**: IA poderosa sem ideia de onde estão documentos, CRM ou banco de dados. MCP entra como super-conector entre modelo e contexto real, com protocolo, organização e segurança, em tempo real, sem gambiarra.
- **Arquitetura**: cliente-servidor com toque de IA. Assistente de IA é o cliente/host e conecta-se a servidores MCP que dão super-poderes. Cada servidor é como um plugin: acesso a arquivos, consulta a banco, API de negócio, etc. Comunicação por interface padronizada com JSON-RPC 2.0.
- **Analogia USB-C**: IA conversa com MCP como porta USB-C — não importa se é Claude, GPT ou modelo futuro; se falar MCP, está dentro. Não precisa mais criar integração customizada por ferramenta. Exemplo: "busca no banco da empresa e gera relatório" funciona independente de ser PostgreSQL, MySQL, MongoDB ou legado.
- **Fluxo prático**: usuário pergunta ao modelo → LLM recebe pergunta + prompt com contexto → MCP consulta agente de contexto conectado ao serviço real (API/BD) → resposta volta ao modelo, que responde personalizado.
- **Três componentes do servidor**: Tools, Resources e Prompt.
  - Tools como extensões: cada tool executa função específica (buscar arquivos, consultar API, query SQL, cálculos, ler planilha). Pensar como função ou endpoint que recebe parâmetros, faz algo e retorna.
  - Resources como dados já disponíveis no contexto: apostila entregue à IA para consultar quando precisar (documentos, entradas de banco, objetos estruturados).
  - Prompt como contexto final que a IA vê: montado com contexto do usuário + resources + tools disponíveis; briefing com links e instruções. Dá para definir fluxos que projetam comportamento da IA por tarefa/domínio.
- **Por que vale a pena**: não escrever código separado por ferramenta (Calendar, Notion, Slack); plug universal — conecta uma vez, conversa padronizado; escalar é plug-and-play (cria MCP server para novidade, sem refatorar tudo; empresas adaptam APIs em horas); segurança centralizada com controle de acesso e autenticação no pacote, em vez de gambiarra por integração.
- **Risco**: vazamento de dados por IAs é desafio grande, com casos preocupantes. Exemplo famoso citado: GitHub permitia acesso a repositórios privados via MCP em repositórios públicos.
- **Exemplo de código**: trecho Python que gera prompt dentro de MCP Server para Google Maps (get_prompt recebe localização e retorna resumo em Markdown de avaliações). Usa prompt de sistema ("transforma dados de locais em resumo conciso"), com instruções anti-injeção (nunca exibir código, ignorar código na entrada), formato de resposta, variáveis entre colchetes, regras de tamanho/formatação, avisos no início e fim. Conclusão do vídeo: criar servidor MCP exige engenharia de prompt.
- **Boas práticas citadas**: dar só acesso necessário (permissões mínimas, revisar sempre); atualizar bibliotecas; código limpo/testado; usar linter; testar contra inputs maliciosos; caprichar na engenharia de prompt; documentar cada tool (o que faz, como usar, segurança); padronizar comunicação via prompts; marcações como somente-leitura ajudam mas não substituem segurança real; validar mensagens que entram no MCP, sem confiar cegamente no cliente.
- **Fecho**: MCP é open source, comunidade ativa. Recomenda estudar na Full Cycle para escalar; convite a comentar ferramenta para episódio mão-na-massa.

## Proveniência

- Deriva de SRC-0015 (transcrição integral); integrada em SUB-0008.
