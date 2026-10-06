---
id: SUB-0010
type: subject
title: QuickCheck — testes baseados em propriedades e geradores de dados (Haskell)
created: 2026-10-06
updated: 2026-10-06
sources:
  - SRC-0020
  - SRC-0021
user_inputs:
  - USR-0003
  - USR-0004
  - USR-0005
knowledge:
  - SUM-0020
  - SUM-0021
related_subjects:
  - SUB-0001
---

# QuickCheck — testes baseados em propriedades e geradores de dados (Haskell)

> O que a Wiki sabe sobre este assunto: síntese das duas aulas de Márcio Lopes Cornélio (CIn-UFPE) — introdução a propriedades (SRC-0020 via SUM-0020) e geradores de dados (SRC-0021 via SUM-0021). Conhecimento redigido com palavras próprias; trechos de código são propriedades-padrão de Haskell apresentadas nas fontes como objetos de teste.

## 1. Definição

- QuickCheck é uma ferramenta de **teste baseado em propriedades** para Haskell: em vez de casos manuais, o testador escreve uma **propriedade esperada** (função) e a ferramenta verifica se ela vale em um grande número de casos gerados aleatoriamente.
- Possui uma linguagem de domínio específico de especificações testáveis; propriedades ficam no mesmo módulo das funções testadas e servem como **documentação testável** (verificável por máquina).
- Motivação: testar custa caro; automação reduz tempo e permite repetir tudo após cada modificação. Programas funcionais puros são ideais porque não há estado anterior/posterior para controlar.

## 2. Como funciona

- O humano fornece um critério decidível por máquina; a ferramenta gera entradas, executa e diz se passou ou falhou, devolvendo **contraexemplo** quando falsificável (ex.: `*** Failed! Falsifiable (after 2 tests): [0] [1]`).
- Comandos usados nas fontes: `quickCheck prop`, `quickCheck (withMaxSuccess 10000 prop)`, `sample gen`, `generate arbitrary`.
- Dois tipos de propriedade:
  - `... -> Bool`: propriedade incondicional.
  - `... -> Property`: propriedade condicional com `cond ==> corpo` — tenta verificar 100 casos que satisfazem a condição (não 100 casos quaisquer).
- Leis só valem para valores **finitos e totais** (ressalva explícita das fontes para `reverse`/`++` e para provas em SUB-0001).

## 3. Exemplos de propriedades (da introdução)

- `mNot` vs `not`: `prop_mNot x = not x == mNot x`.
- `exOr`: definição `(x || y) && not (x && y)`; alternativas `exOr1` por casos e `x /= y`.
- `maxi` (guardas) vs `max'` (`if-then-else`): `prop_compareMax x y = maxi x y == max' x y`; variantes `prop_max1` (com `&&`) e `prop_max2` (com `||`).
- Contraexemplo didático `prop_max3`: `(x == maxi x y) 'exOr' (y == max x y)` falha com `0 0` — quando as entradas são iguais, ambos os lados são verdadeiros e o ou-exclusivo é falso. Lição: revisar funções e a própria propriedade.
- Listas: `reverse [x] == [x]`; `reverse (reverse xs) == xs`; `reverse (xs ++ ys) == reverse ys ++ reverse xs`. A forma com ordem trocada (`reverse xs ++ reverse ys`) é refutada por `[0]` e `[1]`.
- Inserção ordenada: `ordered xs ==> ordered (insert x xs)`.
- `qsort`: idempotência `qsort (qsort xs) == qsort xs`; `head (qsort xs) == minimum xs` e `last ... == maximum xs` sob `not (null xs)`. Comparação com referência `sort` de `Data.List` revela bug: a partição com `<` e `>` estritos descarta duplicatas (`[6,6]` falha). Correção estudada: restringir a listas distintas (`isDistinct`) e testar `isDistinct xs ==> qsort xs == sort xs`.
- Infinitas: `cycle xs == cycle (xs ++ xs)` não é diretamente testável; reformula-se com `take n` e `n >= 0`.
- Exercícios propostos: `threeDifferent` (três inteiros dois a dois diferentes) e `fourEqual` (quatro iguais) via `threeEqual`.

## 4. Geradores de dados

- Tipo `Gen a` (mentalmente `Rand -> a`, mônada); default `arbitrary` da classe `Arbitrary` (`arbitrary`, `coarbitrary`); instâncias prontas para `()`, `Bool`, `Int`, `Integer`, `Float`, `[]`; usuário cria instâncias para tipos próprios.
- Primitiva `choose (a, b)`; ex.: dado `choose (1,6)`; índice aleatório em lista.
- Combinadores:
  - `oneof`: escolhe um gerador uniformemente (ex. booleano meio a meio).
  - `frequency`: escolhe com pesos (ex. 2x `True` vs 1x `False`; 4x `(:)` vs 1x `[]` para listas maiores).
  - `elements`: um valor de uma lista dada.
  - `sized`: acessa o `size` implícito (começa pequeno, cresce); ex. `sized $ \n -> choose (0, n)`. Para listas, `size` é limite superior.
  - `forAll gen corpo`: usa gerador explícito em vez de condição.
  - `liftM`/`liftM2`: promovem funções à mônada (ex. `liftM2 (,) arbitrary arbitrary` para pares).
- Instâncias didáticas: `Int` via `choose (-20,20)`; `(a,b)` via `do` ou `liftM2`; listas via `oneof`/`frequency` + `liftM2 (:)`; `Colour` via `oneof`; `Ternary` via `elements` ou via `choose (0,2)` + `case`; `Tree`/`Tree a` via `oneof`/`frequency` + `sized` com `div` por 2 para garantir terminação.
- Evolução `genList1` (sem base, não termina) → `genList2` (termina mas tende a `[]`) → `genList3` (pesos 1x7) → `genOrdList = genList3 >>= return . sort`, validado por `forAll genOrdList isOrdered`.
- Caso `Doc` (`Empty | Char | Text | Line | Concat | Union`): instância por `oneof` e propriedade de identidade `prop_empty_id` para `empty`/`(<>)`.

## 5. Monitoramento da distribuição

- Pré-condições raras descartam muitos casos: `withMaxSuccess 10000 prop_Insert` dá "Gave up! Passed only 70 tests".
- `classify (null xs) "trivial"`: só 74 passam (45% triviais) — muitas listas vazias.
- `collect (length xs)`: histograma (ex. 34% tamanho 2, 32% tamanho 0, 26% tamanho 1) mostra distorção para listas curtas causada por `ordered xs`.
- Solução: substituir condição por gerador (`forAll orderedList`), passando 10000 testes; combinar `collect` + `classify` ("at-head"/"at-tail") para observar onde a inserção cai.

## 6. Resumos do usuário (não factualizados como fonte externa)

- O usuário elaborou três guias próprios, registrados como `user_input` e relacionados a este subject sem conversão automática em fato confirmado (`AGENTS.md:8`):
  - [USR-0003](../user_input/USR-0003-guia-geradores-dados-quickcheck.md): guia de geradores com um exemplo por conceito (`Gen`/`generate`, `Arbitrary`, `choose`/`elements`, `oneof`/`frequency`, `liftM`/`liftM2`, `sized` para `Tree a`, `forAll` com `genOrdList`, caso `Doc`) + tabela-resumo. Deriva de SRC-0021; complementa a seção 4 com formulações didáticas do usuário.
  - [USR-0004](../user_input/USR-0004-guia-testes-propriedades-exemplos.md): guia de propriedades com exemplo por conceito (contraste teste tradicional vs. lei geral, edge case `[6,6]`, `prop_max1`, `mNot`, involução/idempotência/invariantes, `==>`, `classify` com 45% triviais, `collect` com histograma 0–2, `forAll orderedList` com 10000 testes, `take n` para `cycle`) + tabela-resumo. Deriva de SRC-0020; complementa as seções 2–3 e 5.
  - [USR-0005](../user_input/USR-0005-resumo-quickcheck-property-based-testing.md): resumo explicativo (JUnit/HUnit vs. propriedades, benefícios, leis, `mNot`, bug do `qsort` com `<`/`>` estritos, `take n`, `classify`/`collect`/`forAll`, síntese "de exemplos para leis"). Deriva de SRC-0020.
- Divergência/incerteza preservada: USR-0005 cita **Shrinking** (reduzir o contraexemplo ao menor caso que falha) como benefício; esse conceito **não consta** nos slides registrados (SUM-0020/SUM-0021) e permanece atribuído apenas ao relato do usuário, como não confirmado pela Wiki.

## 7. Relações e proveniência

- Deriva de [SRC-0020](../sources/metadata/SRC-0020-quickcheck-introducao-propriedades.md) via [SUM-0020](../knowledge/summaries/SUM-0020-quickcheck-introducao-propriedades.md) e de [SRC-0021](../sources/metadata/SRC-0021-quickcheck-geradores-dados.md) via [SUM-0021](../knowledge/summaries/SUM-0021-quickcheck-geradores-dados.md), com complementos didáticos de [USR-0003](../user_input/USR-0003-guia-geradores-dados-quickcheck.md), [USR-0004](../user_input/USR-0004-guia-testes-propriedades-exemplos.md) e [USR-0005](../user_input/USR-0005-resumo-quickcheck-property-based-testing.md) (marcados como user input).
- Complementa [SUB-0001](../subjects/SUB-0001-programacao-funcional-haskell.md) (fundamentos, indução, `reverse`/`++`) como técnica de teste das mesmas funções.
- Arquivos originais: privados, **sem cópia versionada** (decisão do usuário; `local_file: none` nos metadados; nada em `wiki/sources/files/` foi criado para estas fontes).
- Bibliografia comum às duas fontes: Claessen–Hughes, ICFP'00.
