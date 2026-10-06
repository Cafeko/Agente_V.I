---
id: SRC-0021
type: source
title: QuickCheck — Geradores de dados (slides)
author: Márcio Lopes Cornélio (Centro de Informática — UFPE)
format: PDF (slides de aula, 28 páginas numeradas + capa)
privacy: private
source_url: none (material didático interno, sem link público informado)
local_file: none (fonte privada fornecida pelo usuário via chat — sem cópia versionada; originais mantidos apenas localmente pelo usuário; pasta wiki/sources/files/private/ ignorada pelo Git)
received: 2026-10-06
availability: privada; usuário solicitou não salvar para o GitHub — nenhuma cópia em wiki/sources/files/public/ ou private/ foi versionada
topics:
  - QuickCheck
  - Geradores de dados
  - Classe Arbitrary
  - Combinadores (oneof, frequency, elements, sized, forAll)
  - Tipos recursivos
  - Listas ordenadas
related_subjects:
  - SUB-0001
  - SUB-0010
knowledge:
  - SUM-0021
related_sources:
  - SRC-0020
references_noted:
  - https://www.schoolofhaskell.com/user/pbv/an-introduction-to-quickcheck-testing
  - http://www.cse.chalmers.se/~rjmh/QuickCheck/manual.html
  - http://www.seas.upenn.edu/~cis552/15fa/lectures/stub/QuickCheck2.html
  - Claessen, K. and Hughes, J. Quickcheck: A lightweight tool for random testing of haskell programs. ICFP '00, ACM, pp. 268–279.
---

# SRC-0021 — QuickCheck: Geradores de dados (slides)

- **Fonte**: slides de aula "QuickCheck — Geradores de dados", de Márcio Lopes Cornélio (CIn-UFPE). Conteúdo recebido como texto extraído + imagens de 28 slides.
- **Privacidade**: material do professor; usuário indicou que os arquivos são privados e não podem ir para o GitHub. Nenhum PDF foi copiado para `wiki/sources/files/`; o conhecimento derivado (SUM-0021, SUB-0010) foi redigido com palavras próprias, sem reprodução literal dos slides.
- **Escopo geral**: tipo `Gen a` e gerador default `arbitrary` da classe `Arbitrary` (`arbitrary`, `coarbitrary`); função `generate :: Gen a -> IO a` e `sample`; gerador primitivo `choose`; instâncias para tipos do usuário; combinadores `oneof`, `frequency`, `elements`, `sized`, `forAll`; controle de `size`; `liftM`/`liftM2`; geradores para listas, `Colour`, `Ternary` (duas formas), `Tree`/`Tree a` com terminação via `sized`/`div`; evolução `genList1`/`genList2`/`genList3` até `genOrdList` (via `sort`); verificação com `forAll genOrdList isOrdered` e `prop_insert`; tipo `Doc` e propriedade `prop_empty_id` com `empty`/`(<>)`.
- **Relação**: continuação prática de SRC-0020; ambos sustentam SUB-0010. Relaciona-se a SUB-0001 (fundamentos de Haskell).
