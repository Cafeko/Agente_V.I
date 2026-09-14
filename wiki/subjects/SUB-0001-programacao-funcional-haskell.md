---
id: SUB-0001
type: subject
title: Programação Funcional (Haskell) — fundamentos anotados
created: 2026-09-14
updated: 2026-09-14
user_inputs:
  - USR-0001
sources:
  - SRC-0001
  - SRC-0002
knowledge:
  - SUM-0001
  - SUM-0002
related_subjects: []
---

# Programação Funcional (Haskell) — fundamentos anotados

> O que a Wiki sabe sobre este assunto: anotações de estudo do usuário (USR-0001),
> confirmadas e ampliadas pelos slides de aula (SRC-0001, SRC-0002) via SUM-0001 e SUM-0002.

## 1. Avaliação preguiçosa (lazy evaluation)

De USR-0001, confirmado por SRC-0001 ([SUM-0001](../knowledge/summaries/SUM-0001-avaliacao-preguicosa.md)):

- **Redex** (expressão redutível): função aplicada a argumentos, pronta para redução.
  Confirma a anotação do usuário — o termo "Regex" em USR-0001 era "redex". Incerteza resolvida.
- **Innermost** (mais interno, desempate à esquerda) = call-by-value: argumentos avaliados
  antes da aplicação, passagem por valor.
- **Outermost** (mais externo, desempate à esquerda) = call-by-name: funções aplicadas
  antes de avaliar os argumentos, passagem por nome.
- Em Haskell, a ordem de avaliação não altera o resultado final (desde que termine);
  a ordem é de fora para dentro e, no mesmo nível, da esquerda para a direita.

Exemplo (de USR-0001):

```haskell
f x y = x + y
f (1+2) 3 → (1+2) + 3 → 3 + 3 [= 6]
```

Complemento de SRC-0001: call-by-name termina sempre que alguma ordem termina, mas pode
duplicar trabalho; **avaliação preguiçosa = call-by-name + compartilhamento** — cada
argumento é avaliado no máximo uma vez, nunca exigindo mais passos que call-by-value.
É o que viabiliza estruturas infinitas e a separação entre dados e controle
(ex.: `take 3 ones`), além de dirigir casamento de padrões, guardas e `where` sob demanda.

## 2. Compreensão de listas

Forma geral (USR-0001, confirmada por SRC-0001):

```haskell
[e | q1, q2, ..., qn]
```

- `e`: expressão aplicada aos valores gerados (ex.: `x + 1`).
- `qi`: **gerador** (`x <- [1..10]`) ou **filtro** (predicado como `x*x > 15`, que descarta
  valores falsos — ex.: `x = 3` gera `9 > 15` e fica fora da lista final).

## 3. Tradução de compreensões para funções básicas

Equivalências de USR-0001, **confirmadas literalmente** por SRC-0001:

```haskell
[x | x <- xs] = xs
[f x | x <- xs] = map f xs
[e | x <- xs, p x, ...] = [e | x <- filter p xs, ...]
[e | x <- xs, y <- ys, ...] = concat [[e | y <- ys, ...] | x <- xs]
```

## 4. Prova por indução sobre listas

Esquema de USR-0001, confirmado e precisado por SRC-0002
([SUM-0002](../knowledge/summaries/SUM-0002-raciocinio-programas.md)):

- Princípio da **indução estrutural** (vale para listas **finitas**): provar `P([])`
  (caso base) e provar `P(x:xs)` assumindo a **hipótese de indução** `P(xs)`.
- Técnica: reduzir os dois lados de cada caso até coincidirem, aplicando a hipótese no passo indutivo.
- Casos registrados nos slides: `sum`/`doubleAll`, `length` sobre `++`,
  `reverse` sobre `++` (exige associatividade de `++`), `flatten` com acumulador em árvores,
  e corretude de compilador para máquina de pilha via lema de distributividade.

---

## Proveniência

- Seções 1–4 derivam de [USR-0001](../user_input/USR-0001-anotacoes-programacao-funcional-haskell.md).
- Confirmações e complementos derivam de [SRC-0001](../sources/metadata/SRC-0001-avaliacao-preguicosa.md)
  (via [SUM-0001](../knowledge/summaries/SUM-0001-avaliacao-preguicosa.md)) e de
  [SRC-0002](../sources/metadata/SRC-0002-raciocinio-programas.md)
  (via [SUM-0002](../knowledge/summaries/SUM-0002-raciocinio-programas.md)).
- Arquivos originais dos slides: pasta privada `wiki/sources/files/private/` (não versionada).
- Incerteza resolvida: "Regex" → "redex". Nenhum conflito entre as fontes até o momento.
