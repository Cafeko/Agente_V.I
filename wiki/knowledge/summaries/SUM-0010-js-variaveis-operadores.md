---
id: SUM-0010
type: summary
source: SRC-0010
title: Summary — Variables and Operators (Odin + assignments)
created: 2026-09-14
related_subjects:
  - SUB-0006
---

# O que esta fonte apresenta (SRC-0010)

> Síntese com palavras próprias da lesson do The Odin Project e das 4 páginas dos assignments
> (MDN ×2, JavaScript.info ×2).

## Papel do JavaScript (MDN)

- Terceira camada da web: HTML estrutura, CSS estiliza, JavaScript cria conteúdo dinâmico
  (atualizações, multimídia, animação, interatividade).

## Como executar (Odin)

- No Foundations, o JS roda no **navegador**: script inline em `<script>` ou arquivo externo
  (`<script src="...">`, extensão `.js`).
- `console.log()` imprime no console das DevTools (inspecionar → aba Console); é a ferramenta
  de verificação dos exercícios.

## Variáveis (Odin + JavaScript.info)

- Variável = "armazenamento nomeado" (analogia da caixa com etiqueta); `=` atribui.
- `let`: declara e permite reatribuição (redeclarar exige `let` só na primeira vez).
- `const`: não permite reatribuição — tentar gera erro (erros são úteis: apontam o quê e onde).
- `var`: forma original, reatribuível, com peculiaridades superadas por `let`/`const`; em
  desuso, mas aparece em código legado. Regra prática: `const` por padrão, `let` quando o valor muda.
- Estilo: uma variável por linha; nomes seguem convenções (ver seção de naming do JavaScript.info).

## Números e operadores (Odin + MDN + JavaScript.info)

- JS tem um único tipo numérico (`Number`), inteiros e decimais tratados igual.
- Ordem de operações padrão (parênteses → exponenciação → ×/÷ → +/−); `**` é exponenciação
  (inclusive raízes fracionárias, ex. `4 ** (1/2)`); `%` é **resto** da divisão inteira, não porcentagem.
- `+` binário com string **concatena** (o outro operando é convertido): `'1' + 2` → `"12"`.
- Unário vs binário: mesmo símbolo, operadores distintos (negação `-x` vs subtração).
- `+` unário converte para número (ex. `+"10"` → `10`); `Number()` faz o mesmo explicitamente.
- Incremento/decremento (`++`/`--`) com formas prefixa e pós-fixa (ordem de avaliação difere);
  precedência de operadores define a ordem; `Math` oferece utilidades (`random`, `floor`, `ceil`).
- Exercícios da lesson: somas, expressão `(4+6+9)/77 ≈ 0.24675`, reatribuição de `let a`,
  cadeia `const max/actual/percentage ≈ 0.7719` — todos verificáveis no console.

## Proveniência

- Toda informação acima deriva de SRC-0010 (Odin, MDN, JavaScript.info), sem acréscimo externo.
