---
id: SUM-0020
type: summary
source: SRC-0020
title: Summary — QuickCheck: Introdução a testes baseados em propriedades
created: 2026-10-06
related_subjects:
  - SUB-0010
  - SUB-0001
---

# O que esta fonte apresenta (SRC-0020)

> Síntese redigida com palavras próprias a partir dos slides privados SRC-0020.
> Sem citações literais; trechos de código abaixo são propriedades-padrão de Haskell
> apresentadas na fonte como objetos de teste.

## Ideia central

- Testar custa caro; automatizar (em parte ou no todo) economiza tempo e permite repetir os testes após cada modificação.
- Programas funcionais puros são especialmente adequados: sem estado anterior/posterior para controlar.
- A ferramenta precisa decidir sozinha se um teste passou; o humano fornece um critério verificável por máquina.
- QuickCheck oferece uma linguagem de especificações testáveis: o testador escreve **propriedades esperadas** no mesmo módulo das funções, e a ferramenta verifica a propriedade em um grande número de casos gerados aleatoriamente. As propriedades viram documentação testável.

## Geração de dados

- A ferramenta gera os dados de entrada sozinha; não é preciso escolher casos manualmente.
- Geração é aleatória, com uma linguagem que permite programar o próprio gerador (detalhada em SRC-0021).

## Benefícios destacados

- Obriga a pensar no que o código deveria fazer.
- Encontra casos limítrofes onde a especificação é violada.
- As especificações permanecem como documentação verificável por máquina.

## Exemplos simples

- `mNot` (nova versão de `not`): propriedade compara `not x` com `mNot x` para todo `Bool x`.
- `exOr` (ou-exclusivo) definido como `(x || y) && not (x && y)`; duas formulações alternativas testadas: por casos (`exOr1 True x = not x; exOr1 False x = x`) e como desigualdade (`x /= y`).
- `maxi` por guardas vs. `max'` por `if-then-else`: propriedade de equivalência `maxi x y == max' x y`.
- Outras formulações de `max`: (a) resultado >= ambas as entradas; (b) formulação com `||` registrada na fonte (atenção: a forma com `||` é fraca — ver contraexemplo abaixo).

## Contraexemplos

- QuickCheck devolve um contraexemplo quando a propriedade é falsificável.
- Caso `prop_max3`: combina `(x == maxi x y)` e `(y == max x y)` com `exOr`; falha com `0 0` após 1 teste. Lição da fonte: quando falha, revisar funções e a própria propriedade (aqui, quando `x == y`, ambos os lados são verdadeiros e o ou-exclusivo falha).

## Leis de listas

- Leis apresentadas (válidas para valores finitos e totais): `reverse [x] = [x]`; `reverse (reverse xs) == xs`; `reverse (xs ++ ys) == reverse ys ++ reverse xs`.
- Versão incorreta `reverse (xs ++ ys) == reverse xs ++ reverse ys` é refutada com `xs=[0]`, `ys=[1]` após 2 testes. A fonte sugere rodar com mais casos (`withMaxSuccess 10000`).

## Leis condicionais

- Inserção em lista ordenada: `ordered xs ==> ordered (insert x xs)`.
- O tipo do resultado muda de `Bool` para `Property`; em vez de 100 casos aleatórios quaisquer, tenta-se 100 casos que satisfazem a condição.

## Quicksort como estudo de caso

- Definição lembrada: `qsort [] = []`; `qsort (x:xs) = qsort lhs ++ [x] ++ qsort rhs` com `lhs = [y | y <- xs, y < x]` e `rhs = [z | z <- xs, z > x]`.
- Propriedades: idempotência (`qsort (qsort xs) == qsort xs`); cabeça da saída = mínimo da entrada (não faz sentido para lista vazia, embora devesse valer para todas as entradas — motivação para condicionais).
- Formas condicionais: `not (null xs) ==> head (qsort xs) == minimum xs` e análoga com `last`/`maximum`. Moral da fonte: especificar esclarece as pré-condições.
- Teste contra implementação de referência (`sort` de `Data.List`): `qsort xs == sort xs` falha com `[6,6]` após 8 testes — há bug no `qsort` da fonte (a partição usa `<` e `>` estritos, descartando duplicatas).
- Correção proposta: restringir a listas distintas (`isDistinct`: `[] = True`; `(x:xs) = x notElem xs && isDistinct xs`) e testar `isDistinct . qsort` ou `isDistinct xs ==> qsort xs == sort xs`.

## Monitoramento da distribuição

- `prop_Insert` com 10000 casos: "Gave up! Passed only 70 tests" — se a pré-condição raramente vale, muitos casos são descartados.
- `classify (null xs) "trivial"`: com 10000 tentativas, só 74 passam (45% triviais) — muitas inserções em lista vazia.
- `collect (length xs)`: histograma mostra concentração em listas curtas (ex.: 34% tamanho 2, 32% tamanho 0, 26% tamanho 1, 7% tamanho 3, 1% tamanho 5) — a pré-condição distorce a distribuição para poucos elementos.
- Solução: trocar a condição por gerador de listas ordenadas via `forAll orderedList (\xs -> ...)`; com isso, 10000 testes passam.
- Observação combinada: `collect` + dois `classify` ("at-head" se `x:xs` ordenada, "at-tail" se `xs++[x]` ordenada).

## Exercícios e estruturas infinitas

- Exercícios: definir testes para `threeDifferent :: Integer -> Integer -> Integer -> Bool` (verdadeiro só se os três inteiros diferem) e `fourEqual :: Integer -> Integer -> Integer -> Integer -> Bool` (verdadeiro só se os quatro são iguais), este com base em `threeEqual`.
- `cycle`: `not (null xs) ==> cycle xs == cycle (xs ++ xs)` é intuitivamente verdadeira, mas não verificável diretamente (compara listas infinitas). Reformulação: comparar segmentos finitos com `take n`, exigindo `n >= 0`.

## Bibliografia citada na fonte

- Artigo seminal: Claessen e Hughes, "Quickcheck: A lightweight tool for random testing of haskell programs", ICFP '00, ACM, pp. 268–279.
