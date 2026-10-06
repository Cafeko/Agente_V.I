---
id: SUM-0021
type: summary
source: SRC-0021
title: Summary — QuickCheck: Geradores de dados
created: 2026-10-06
related_subjects:
  - SUB-0010
  - SUB-0001
---

# O que esta fonte apresenta (SRC-0021)

> Síntese redigida com palavras próprias a partir dos slides privados SRC-0021.
> Sem citações literais; trechos de código abaixo são geradores-padrão de Haskell
> apresentados na fonte como exemplos didáticos.

## Base: Gen, arbitrary, generate

- Para gerar valores de um tipo `a`, usa-se um gerador `Gen a`; o gerador default é `arbitrary`, da classe `Arbitrary`.
- Com um gerador em mãos, valores de tipos básicos com instância de `Arbitrary` são produzidos via `generate :: Gen a -> IO a` (exemplos da fonte: `Int`, `(Char, Bool)`, `[Maybe Bool]`).
- A classe tem `arbitrary :: Gen a` e `coarbitrary :: a -> Gen b -> Gen b`; QuickCheck usa sobrecarga para dar um gerador default por tipo (instâncias para `()`, `Bool`, `Int`, `Integer`, `Float`, `[]`). O usuário declara instâncias para os tipos que definir.
- Modelo mental: `Gen a` como função de uma semente numérica (`Rand -> a`); `Gen` é mônada.
- Primitiva `choose :: Random a => (a, a) -> Gen a` escolhe aleatoriamente num intervalo; exemplo da fonte: escolha de índice `i <- choose (0, length xs - 1)` seguida de `return (xs !! i)`.
- Exemplos `choose`: dado `choose (1,6)`; booleano `choose (False, True)`.

## Combinadores

- `oneof :: [Gen a] -> Gen a`: escolhe aleatoriamente um dos geradores (lista não vazia). Ex.: `oneof [return True, return False]` dá booleano com probabilidade meio a meio. `sample` gera alguns valores e imprime.
- `frequency`: como `oneof`, mas pesa cada alternativa (ex.: `[(2, return True), (1, return False)]`).
- `sized :: (Int -> Gen a) -> Gen a`: expõe o parâmetro implícito `size`. QuickCheck começa pequeno e aumenta gradualmente; ex.: `sized $ \n -> choose (0, n)` para naturais até `size`. Objetivo: casos grandes o bastante para revelar erros, pequenos o bastante para serem rápidos. Para listas, `size` vira limite superior.
- `elements :: [a] -> Gen a`: gera um dos valores dados.
- `forAll :: (Show a, Testable prop) => Gen a -> (a -> prop) -> Property`: testa a saída de um gerador (ex.: verificar que só listas ordenadas são produzidas; verificar inserção).

## Definindo geradores (instâncias)

- `Int` didático: `arbitrary = choose (-20, 20)`.
- Par `(a,b)`: versão `do x <- arbitrary; y <- arbitrary; return (x,y)`, ou mais curta com `liftM2 (,) arbitrary arbitrary`.
- `liftM` promove função de 1 argumento para a mônada; `liftM2` promove função de 2 argumentos, lendo da esquerda para a direita (ex. da fonte: `liftM2 (+) [1,2] [4,5] = [5,6,6,7]`).
- Listas: `oneof [return [], liftM2 (:) arbitrary arbitrary]` produz listas com média de um elemento; com `frequency [(1, return []), (4, liftM2 (:) arbitrary arbitrary)]` o construtor `(:)` fica 4x mais provável que `[]`, gerando listas maiores (ex. com pesos 6x1 no `sample`).
- `Colour = Red | Blue | Green`: `oneof [return Red, return Blue, return Green]`.
- `Ternary = Yes | No | Unknown`: duas formas — (a) `elements [Yes, No, Unknown]`; (b) gerar `n <- choose (0,2)` e mapear `0 -> Yes, 1 -> No, _ -> Unknown`.

## Tipos recursivos e controle de tamanho

- `Tree = Leaf Int | Branch Tree Tree`: tentativa ingênua `tree = oneof [liftM Leaf arbitrary, liftM2 Branch tree tree]` pode não terminar ou gerar valores enormes.
- Correção com `sized`: `tree = sized tree'` com `tree' 0 = liftM Leaf arbitrary` e `tree' n = oneof [liftM Leaf arbitrary, liftM2 Branch subtree subtree]` onde `subtree = tree' (n `div` 2)`.
- `Tree a = Leaf a | Branch (Tree a) (Tree a)`: versão com `frequency [(1, liftM Leaf arbitrary), (2, liftM2 Branch arbitrary arbitrary)]`, depois refinada com `sized arbTree` e peso 1x4 (`arbTree 0 = ...`; `arbTree n = frequency [(1, ...), (4, liftM2 Branch (arbTree (n `div` 2)) (arbTree (n `div` 2)))]`).

## Listas ordenadas (evolução didática)

- `genList1 = liftM2 (:) arbitrary genList1`: problema — nunca termina com `[]` (recursão sem base).
- `genList2 = oneof [return [], liftM2 (:) arbitrary genList2]`: melhor, mas tende a lista vazia com frequência.
- `genList3 = frequency [(1, return []), (7, liftM2 (:) arbitrary genList3)]`: controla o tamanho pelo peso.
- `genOrdList = genList3 >>= return . sort`: ordena a lista gerada; verificado por `quickCheck $ forAll genOrdList isOrdered`.
- Propriedade de inserção: `prop_insert x = forAll genOrdList $ \xs -> isOrdered xs && isOrdered (insert x xs)`.

## Exemplo Doc

- Tipo `Doc = Empty | Char Char | Text String | Line | Concat Doc Doc | Union Doc Doc`.
- Instância ingênua com `oneof` sobre os 6 construtores (com `liftM`/`liftM2` e `arbitrary` nos campos).
- Funções `empty = Empty` e `(<>)` com `Empty <> y = y`, `x <> Empty = x`, `x <> y = x `Concat` y`; propriedade `prop_empty_id x = (empty <> x == x) && (x <> empty == x)`.

## Referências citadas na fonte

- Introdução School of Haskell, manual QuickCheck (Chalmers), notas UPenn CIS552 e o artigo Claessen–Hughes ICFP'00.
