---
id: CMP-0001
type: comparison
title: Comparison — Haskell vs JavaScript (escopo do registrado)
created: 2026-09-14
related_subjects:
  - SUB-0001
  - SUB-0006
knowledge:
  - SUM-0001
  - SUM-0010
---

# Comparison — Haskell vs JavaScript (escopo do registrado)

> O que está sendo comparado: os dois subjects de linguagens da Wiki — SUB-0001 (Haskell) e
> SUB-0006 (JavaScript) — **somente** no que cada um registra. Criada a pedido do usuário em
> 2026-09-14, com escopo explicitamente limitado.

## Critérios e diferenças

| Critério | Haskell (SUB-0001) | JavaScript (SUB-0006) |
|---|---|---|
| Como se computa | Aplicação e redução de funções; avaliação preguiçosa (de fora para dentro, só o necessário, com compartilhamento) | Execução no navegador; verificação via `console.log()` no console |
| Variáveis | Não registrado | `let` (reatribuível), `const` (não reatribuível, erro ao tentar), `var` (legado, em desuso) |
| Construções registradas | Compreensão de listas (com tradução para `map`/`filter`/`concat`); prova por indução | Operadores (`**`, `%` resto, `+` que concatena com string, `++`/`--`); tipo único `Number` |

## Semelhanças (sustentadas)

- Ambas computam **avaliando expressões**: Haskell por redução até o resultado (ex.: `f (1+2) 3 → 6`);
  JavaScript avaliando expressões no console (ex.: `(4+6+9)/77 ≈ 0.24675`).

## Limites desta comparação

- A cobertura é **assimétrica**: estratégia de avaliação só existe para Haskell; variáveis e
  operadores só para JavaScript. Não há base registrada para comparar paradigma, tipagem,
  contexto de execução de Haskell ou ordem de avaliação de JavaScript.
- Conclusão: comparação válida apenas no escopo acima; uma comparação paradigmática exigiria
  novas fontes para ambos os lados.

---

## Proveniência

- Lado Haskell: [SUB-0001](../subjects/SUB-0001-programacao-funcional-haskell.md) via
  [SUM-0001](../knowledge/summaries/SUM-0001-avaliacao-preguicosa.md) (+ USR-0001).
- Lado JavaScript: [SUB-0006](../subjects/SUB-0006-javascript-variaveis-operadores.md) via
  [SUM-0010](../knowledge/summaries/SUM-0010-js-variaveis-operadores.md).
- Nenhum conhecimento externo foi usado.
