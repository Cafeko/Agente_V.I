---
id: USR-0004
type: user_input
title: Testes Baseados em Propriedades com QuickCheck — guia com exemplo por conceito (resumo do usuário)
date: 2026-10-06
author: usuário
topics:
  - QuickCheck
  - Teste baseado em propriedades
  - Leis condicionais
  - Monitoramento (classify, collect, forAll)
  - Estruturas infinitas
related_subjects:
  - SUB-0010
derived_from:
  - SRC-0020
  - SUM-0020
---

# USR-0004 — Testes Baseados em Propriedades com QuickCheck (resumo do usuário)

> Informação fornecida diretamente pelo usuário em 2026-10-06: guia elaborado pelo próprio usuário em que cada conceito traz seu exemplo prático. Registrado como `user_input` conforme `AGENTS.md:8` — interpretação/síntese do usuário a partir dos slides SRC-0020. Não tratado automaticamente como fato externo confirmado; uso em subjects deve indicar a origem em USR-0004.

## 1. O que é e para que serve

- QuickCheck (Claessen e Hughes, Haskell): paradigma de **Testes Baseados em Propriedades**. Em vez de caso a caso, definem-se **regras formais (propriedades)** para qualquer entrada válida; a ferramenta gera centenas/milhares de entradas aleatórias para tentar falhar a regra.
- Contraste do usuário: teste tradicional verifica um exemplo (`reverse [1,2,3] == [3,2,1]`); propriedade verifica a lei geral (`reverse (reverse xs) == xs` para qualquer `xs`).

## 2. Casos de uso (com exemplos do usuário)

- **Edge cases**: `qsort xs == sort xs` encontra `[6, 6]` e revela que a implementação descartou duplicatas.
- **Documentação executável**: `prop_max1 x y = x <= maxi x y && y <= maxi x y` documenta que o máximo é >= ambas as entradas; quebra futura falha o teste.
- **Equivalência entre implementações**: `mNot` vs `not`:

```haskell
mNot :: Bool -> Bool
mNot True  = False
mNot False = True

prop_mNot :: Bool -> Bool
prop_mNot x = not x == mNot x
```

## 3. Padrões de propriedades

- **Involução**: `prop_RevRev xs = reverse (reverse xs) == xs` (inverter 2x volta ao início).
- **Idempotência**: `prop_qsort_idemp xs = qsort (qsort xs) == qsort xs` (reaplicar não muda).
- **Invariantes de saída**: `prop_qsort_min xs = head (qsort xs) == minimum xs` (cabeça da ordenada = mínimo).

## 4. Pré-condição ==> e leis condicionais

- Nem toda regra vale para toda entrada (ex. `head` de lista vazia). Usa-se `==>` e o retorno vira `Property`:

```haskell
prop_qsort_nn_min :: [Int] -> Property
prop_qsort_nn_min xs = not (null xs) ==> head (qsort xs) == minimum xs
```

- Se a entrada for vazia, o caso é descartado e outro é gerado.

## 5. Monitoramento (exemplos do usuário)

- **classify**: rotula cenários e mostra porcentagens.

```haskell
prop_Insert2 :: Int -> [Int] -> Property
prop_Insert2 x xs =
  isOrdered xs ==>
    classify (null xs) "trivial" $
      isOrdered (insert x xs)
```

Resultado: `*** Gave up! Passed only 74 tests (45% trivial).` — 45% eram listas vazias; teste não avaliava listas complexas.

- **collect**: histograma da distribuição.

```haskell
prop_Insert3 :: Int -> [Int] -> Property
prop_Insert3 x xs =
  isOrdered xs ==>
    collect (length xs) $
      isOrdered (insert x xs)
```

```text
34% 2
32% 0
26% 1
7% 3
1% 5
```

Leitura do usuário: maioria tamanhos 0–2; `isOrdered xs` descartava listas maiores.

- **forAll**: gerador customizado em vez de filtro.

```haskell
prop_Insert4 :: Int -> [Int] -> Property
prop_Insert4 x xs =
  forAll orderedList $ \xs ->
    isOrdered (insert x xs)
```

Com `forAll orderedList`, 100% dos testes são aproveitados (`+++ OK passed 10000 tests`).

## 6. Estruturas infinitas

- Igualdade direta entre infinitas trava; testa-se prefixo finito com `take n`. Para `cycle [1,2] -> [1,2,1,2,...]`, a propriedade intuitiva `cycle xs == cycle (xs ++ xs)` vira:

```haskell
prop_DoubleCycle :: [Int] -> Int -> Property
prop_DoubleCycle xs n =
  not (null xs) && n >= 0 ==>
    take n (cycle xs) == take n (cycle (xs ++ xs))
```

Com `n = 50`, comparam-se só os 50 primeiros elementos.

## Tabela do usuário

| Conceito | O que é | Exemplo |
| --- | --- | --- |
| Propriedade simples | Regra geral booleana | `prop_mNot x = not x == mNot x` |
| Contraexemplo | Dado que faz falhar | `[6, 6]` contra `qsort` |
| Pré-condição (`==>`) | Filtra entradas | `not (null xs) ==> head (qsort xs) == minimum xs` |
| `classify` | Porcentagens de cenários | `classify (null xs) "trivial"` |
| `collect` | Histograma da distribuição | `collect (length xs)` |
| `forAll` | Dados pré-formatados sem filtro | `forAll orderedList` |
| Teste infinito (`take n`) | Limita comparação a prefixo finito | `take n (cycle xs) == take n (cycle (xs ++ xs))` |

---

### Notas de registro

- Tipo de conteúdo: guia de estudo com exemplos (conhecimento + interpretações do usuário, derivado de SRC-0020).
- Exemplos e tabela preservados do texto encaminhado, com ajustes mínimos de formatação.
