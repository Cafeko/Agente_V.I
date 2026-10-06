---
id: USR-0005
type: user_input
title: QuickCheck e Property-Based Testing — resumo explicativo (resumo do usuário)
date: 2026-10-06
author: usuário
topics:
  - QuickCheck
  - Property-Based Testing
  - Benefícios
  - Leis e pré-condições
  - Quicksort
  - Estruturas infinitas
related_subjects:
  - SUB-0010
derived_from:
  - SRC-0020
  - SUM-0020
---

# USR-0005 — QuickCheck e Property-Based Testing (resumo do usuário)

> Informação fornecida diretamente pelo usuário em 2026-10-06: resumo explicativo elaborado pelo próprio usuário. Registrado como `user_input` conforme `AGENTS.md:8` — interpretação/síntese do usuário a partir dos slides SRC-0020. Não tratado automaticamente como fato externo confirmado; uso em subjects deve indicar a origem em USR-0005. Observação: o texto do usuário menciona "Shrinking" (encolhimento) como benefício; esse conceito **não** consta nos slides SRC-0020/SRC-0021 registrados (SUM-0020/SUM-0021) e fica aqui atribuído apenas ao relato do usuário (não confirmado pela Wiki).

## 1. Visão geral (texto do usuário)

- QuickCheck: biblioteca/ferramenta de teste automatizado (Haskell, Koen Claessen e John Hughes) que introduziu **Testes Baseados em Propriedades**.
- Testes tradicionais (JUnit/HUnit): programador especifica entrada e saída esperada por caso (ex. lista `[1, 2]` -> `[2, 1]`). QuickCheck: desenvolvedor define **regras formais (propriedades)** para qualquer entrada válida; a ferramenta gera centenas/milhares de entradas aleatórias para tentar quebrar a propriedade.

## 2. Para que serve e benefícios (texto do usuário)

- Verificar corretude de forma ampla e automatizada, reduzindo exemplos manuais repetitivos.
- **Edge cases**: entradas extremas que o desenvolvedor esqueceria (vazias, negativos, duplicatas).
- **Documentação testável**: propriedades no próprio módulo; documentação executável verificada a cada alteração.
- **Estímulo ao design**: força pensar abstratamente sobre o que o programa deve fazer (especificações).
- **Encolhimento (Shrinking)** — relato do usuário, não confirmado nos slides: ao achar contraexemplo, tenta reduzir ao menor exemplo que ainda falha.
- **Adequação funcional**: funções puras não dependem de estado global, o que torna geração e verificação diretas.

## 3. Conceitos (texto do usuário)

- **Propriedade**: função-invariante/regra lógica, retornando `Bool` ou `Property`.
- **Leis**: inversão/involução `reverse (reverse xs) == xs`; idempotência `qsort (qsort xs) == qsort xs`; invariantes como `x <= maxi (x, y)` e `y <= maxi (x, y)`.
- **Pré-condições (`==>`)**: ex. `not (null xs) ==> head (qsort xs) == minimum xs` — sem a guarda, `head` de vazia daria erro.

## 4. Exemplos (texto do usuário)

- **`mNot`**: nova negação vs `not`, com `prop_mNot x = not x == mNot x` testada sobre `Bool`.
- **Bug no quicksort**:

```haskell
qsort [] = []
qsort (x:xs) = qsort lhs ++ [x] ++ qsort rhs
  where lhs = [y | y <- xs, y < x]
        rhs = [z | z <- xs, z > x]
```

```haskell
prop_qsort_sort :: [Int] -> Bool
prop_qsort_sort xs = qsort xs == sort xs
```

Falha em `[6, 6]` porque `<` e `>` descartam iguais a `x`. Correção: consertar `qsort` ou restringir com `isDistinct xs ==> qsort xs == sort xs`.

- **Infinitas**: `cycle xs == cycle (xs ++ xs)` travaria; solução com prefixo:

```haskell
prop_DoubleCycle :: [Int] -> Int -> Property
prop_DoubleCycle xs n =
  not (null xs) && n >= 0 ==>
    take n (cycle xs) == take n (cycle (xs ++ xs))
```

## 5. Monitoramento e geração (texto do usuário)

- `==>` pode distorcer (condição rara -> descarta maioria, "desiste").
- `classify`: proporção por categoria (ex. "triviais" vazias).
- `collect`: histograma da distribuição.
- `forAll` + gerador customizado (ex. `orderedList`): gera só listas ordenadas, evita descarte e cobre milhares de casos.

## Síntese do usuário

- QuickCheck muda o foco de "exemplos específicos de entradas e saídas" para "leis e regras gerais do domínio"; a automação busca exaustiva e aleatoriamente cenários de falha, como mecanismo de qualidade e corretude.

---

### Notas de registro

- Tipo de conteúdo: resumo de estudo (conhecimento + interpretações do usuário, derivado de SRC-0020).
- Conteúdo preservado do texto encaminhado, com ajustes mínimos de formatação; ponto de incerteza/divergência marcado no cabeçalho (Shrinking).
