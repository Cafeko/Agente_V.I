---
id: USR-0003
type: user_input
title: Guia de Geradores de Dados no QuickCheck (resumo do usuário, com exemplos)
date: 2026-10-06
author: usuário
topics:
  - QuickCheck
  - Geradores de dados
  - Arbitrary
  - Combinadores
  - Tipos recursivos
related_subjects:
  - SUB-0010
derived_from:
  - SRC-0021
  - SUM-0021
---

# USR-0003 — Guia de Geradores de Dados no QuickCheck (resumo do usuário)

> Informação fornecida diretamente pelo usuário em 2026-10-06: resumo elaborado pelo próprio usuário sobre geradores de dados, com um exemplo prático para cada conceito. Registrado como `user_input` conforme `AGENTS.md:8` — interpretação/síntese do usuário a partir dos slides SRC-0021. Não tratado automaticamente como fato externo confirmado; uso em subjects deve indicar a origem em USR-0003.

## 1. Visão geral

- Nos testes baseados em propriedades não se inserem dados manuais; o QuickCheck constrói valores aleatórios automaticamente.
- O tipo monádico responsável é `Gen a` (gerador de valores do tipo `a`).
- Para rodar um gerador em `IO`: `generate :: Gen a -> IO a`.

Exemplos do usuário:

```haskell
> generate arbitrary :: IO Int
23

> generate arbitrary :: IO (Char, Bool)
('_', False)
```

## 2. Classe Arbitrary

```haskell
class Arbitrary a where
    arbitrary :: Gen a
    coarbitrary :: a -> Gen b -> Gen b
```

- QuickCheck já tem instâncias default para tipos primitivos (`Int`, `Float`, `Bool`, `()`, listas `[]`); para tipos novos (ex. `Tree`) o usuário deve programar a instância para que o QuickCheck saiba testar.

Exemplo do usuário com `sample`:

```haskell
> sample (arbitrary :: Gen Int)
0
-2
1
4
-7
...
```

## 3. Geradores básicos (choose, elements)

- `choose`: valor aleatório em intervalo inclusivo. Ex.: `dado = choose (1, 6)`.
- `elements`: um elemento de uma lista finita. Ex.:

```haskell
data Ternary = Yes | No | Unknown deriving (Eq, Show)

instance Arbitrary Ternary where
    arbitrary = elements [Yes, No, Unknown]
```

## 4. Combinando geradores (oneof, frequency)

- `oneof`: escolhe um gerador da lista com probabilidades iguais. Ex.:

```haskell
data Colour = Red | Blue | Green deriving (Show)

instance Arbitrary Colour where
    arbitrary = oneof [return Red, return Blue, return Green]
```

- `frequency`: pondera com pesos (essencial para recursivos e para evitar listas vazias em excesso). Ex.: `frequency [(2, return True), (1, return False)]` (66% `True`, 33% `False`).

## 5. liftM e liftM2

- `Gen` é mônada; `liftM`/`liftM2` (de `Control.Monad`) aplicam construtores sobre geradores.
- `liftM` promove função de 1 argumento; `liftM2` combina dois geradores.

```haskell
instance (Arbitrary a, Arbitrary b) => Arbitrary (a, b) where
    arbitrary = liftM2 (,) arbitrary arbitrary
```

Forma equivalente com `do`:

```haskell
instance (Arbitrary a, Arbitrary b) => Arbitrary (a, b) where
    arbitrary = do
        x <- arbitrary
        y <- arbitrary
        return (x, y)
```

## 6. Recursivos e sized

- Recursivos podem entrar em loop; `sized :: (Int -> Gen a) -> Gen a` captura o `size` interno (começa pequeno e cresce) para controlar a profundidade.

```haskell
data Tree a = Leaf a | Branch (Tree a) (Tree a) deriving (Show)

instance Arbitrary a => Arbitrary (Tree a) where
    arbitrary = sized arbTree
      where
        arbTree 0 = liftM Leaf arbitrary
        arbTree n = frequency
            [ (1, liftM Leaf arbitrary)
            , (4, liftM2 Branch (arbTree (n `div` 2)) (arbTree (n `div` 2)))
            ]
```

## 7. forAll

- `forAll :: Gen a -> (a -> Property) -> Property`: executa a propriedade com um gerador específico, sem precisar vinculá-lo como `arbitrary` default.

```haskell
genOrdList :: (Arbitrary a, Ord a) => Gen [a]
genOrdList = genList3 >>= return . sort

prop_insert :: Int -> Property
prop_insert x = forAll genOrdList $ \xs ->
    isOrdered xs && isOrdered (insert x xs)
```

```haskell
*Main> quickCheck prop_insert
+++ OK, passed 100 tests.
```

## 8. Aplicação: Doc

```haskell
data Doc = Empty
         | Char Char
         | Text String
         | Line
         | Concat Doc Doc
         | Union Doc Doc
         deriving (Show, Eq)

instance Arbitrary Doc where
    arbitrary = oneof
        [ return Empty
        , liftM Char arbitrary
        , liftM Text arbitrary
        , return Line
        , liftM2 Concat arbitrary arbitrary
        , liftM2 Union arbitrary arbitrary
        ]
```

```haskell
prop_empty_id :: Doc -> Bool
prop_empty_id x = (empty <> x == x) && (x <> empty == x)
```

## Tabela do usuário

| Conceito / Combinador | Para que serve | Exemplo |
| --- | --- | --- |
| `Gen a` | Tipo do gerador monádico | `dado :: Gen Int` |
| `Arbitrary` | Classe do gerador padrão (`arbitrary`) | `instance Arbitrary Ternary where ...` |
| `choose` | Valor em intervalo inclusivo | `choose (1, 6)` |
| `elements` | Um item de uma lista de opções | `elements [Yes, No, Unknown]` |
| `oneof` | Escolhe entre geradores com pesos iguais | `oneof [return Red, return Blue, return Green]` |
| `frequency` | Escolhe com pesos específicos | `frequency [(2, return True), (1, return False)]` |
| `sized` | Captura `size` para controlar recursão | `sized arbTree` |
| `forAll` | Aplica gerador customizado na propriedade | `forAll genOrdList $ \xs -> isOrdered (insert x xs)` |

---

### Notas de registro

- Tipo de conteúdo: resumo de estudo com exemplos (conhecimento + interpretações do usuário, derivado de SRC-0021).
- Exemplos e tabela preservados do texto encaminhado, com ajustes mínimos de formatação.
