---
id: USR-0001
type: user_input
title: Anotações de estudo — Programação Funcional (Haskell)
date: 2026-09-14
topics:
  - Programação Funcional
  - Haskell
  - Lazy Evaluation
  - Compreensão de listas
  - Prova por indução
related_subjects:
  - SUB-0001
---

# Anotações de estudo — Programação Funcional (Haskell)

> Informação fornecida diretamente pelo usuário em 2026-09-14.
> Conteúdo transcrito das anotações de estudo do dia anterior, sem verificação externa.
> Status: conhecimento de estudo do usuário, não tratado como fato externo confirmado.

## 1. Lazy Evaluation

- Call-by-name (outermost): calcula Regex mais externo primeiro.
- Só calcula o mais preciso.
- Ordem da esquerda para direita.
- Compartilha resultados, não precisa calcular mesma coisa várias vezes.

Exemplo anotado:

```haskell
f x y = x + y
f (1+2) 3 → (1+2) + 3 → 3 + 3 [= 6]
```

Observação do usuário: `regex = f (1+2) 3` e `(1+2)` são as duas coisas que dá para calcular; usando lazy calcula `f` primeiro e depois `(1+2)`.

## 2. Compreensão de lista

Forma geral anotada:

```haskell
[e | q1, q2, ..., qn]
```

- `e` = expressão (ex.: `x + 1`).
- `qi` = qualificador:
  - Gerador: `x <- [1..10]`
  - Filtro: `x*x > 15` — elimina a ocorrência de entrada para a lista. Ex.: `x = 3`, `x*x > 15` → `9 > 15` é falso e não entra na lista final.

Gera uma lista a partir dos qualificadores, aplicando a expressão aos valores gerados.

## 3. Traduções de compreensão de lista

Anotações do usuário:

```haskell
[x | x <- xs] = xs
[f x | x <- xs] = map f xs   (f = função)
[e | x <- xs, p x, ...] = [e | x <- filter p xs, ...]
[e | x <- xs, y <- ys, ...] = concat [[e | y <- ys, ...] | x <- xs]
```

## 4. Prova por indução

Hipótese anotada: `P(xs) = xs <- Provar` (formulação do usuário).

1. Caso base: `xs = []` — `P([]) = []`. Mostrar que esquerda = direita.
2. Caso indutivo: tem que funcionar para `xs + 1` (`x:xs`) — `P(x:xs) = x:xs`. Mostrar que esquerda = direita ao aplicar a hipótese na esquerda.

Se mostrar que os dois lados são iguais nos 2 casos, a hipótese é provada por indução.

---

### Notas de registro

- Tipo de conteúdo: anotações de estudo (conhecimento + interpretações do usuário).
- Termo "Regex" preservado como está nas anotações; possível interpretação: "redex", não confirmado.
- Exemplo do item 1 preservado literalmente, incluindo a formulação original do usuário.
