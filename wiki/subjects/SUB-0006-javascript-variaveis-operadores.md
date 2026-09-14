---
id: SUB-0006
type: subject
title: JavaScript — variáveis e operadores (fundamentos)
created: 2026-09-14
updated: 2026-09-14
sources:
  - SRC-0010
knowledge:
  - SUM-0010
related_subjects: []
---

# JavaScript — variáveis e operadores (fundamentos)

> O que a Wiki sabe sobre os fundamentos de JS estudados pelo usuário: lesson "Variables and
> Operators" do The Odin Project + assignments (SRC-0010 via SUM-0010).

## Onde o JS vive e como testar

JavaScript é a camada dinâmica da web (HTML estrutura, CSS estiliza, JS interage). No estágio
Foundations ele roda no navegador — inline ou em `.js` externo — e o console das DevTools com
`console.log()` é o instrumento de verificação de cada exercício.

## Variáveis

"Armazenamento nomeado": `let` para valores que mudam, `const` por padrão (reatribuir é erro —
e erro útil, pois localiza o problema), `var` legado em desuso. Uma declaração por linha.

## Números e operadores

Tipo único `Number`; precedência matemática padrão; `**` (potência/raízes) e `%` (resto, não
porcentagem); `+` com string concatena e converte o outro lado; unário `+` e `Number()` convertem
para número; `++`/`--` prefixos e pós-fixos; `Math` para utilidades. Exercícios-guia da lesson:
somas, `(4+6+9)/77`, reatribuição de variável e a cadeia `max/actual/percentage`.

---

## Proveniência

- Todo o conteúdo deriva de [SRC-0010](../sources/metadata/SRC-0010-odin-variables-operators.md)
  via [SUM-0010](../knowledge/summaries/SUM-0010-js-variaveis-operadores.md).
- Material aberto (Odin, MDN, JavaScript.info); sem cópia local, acesso pelas URLs em SRC-0010.
