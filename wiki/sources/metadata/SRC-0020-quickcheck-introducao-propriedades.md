---
id: SRC-0020
type: source
title: QuickCheck — Introdução a testes baseados em propriedades (slides)
author: Márcio Lopes Cornélio (Centro de Informática — UFPE)
format: PDF (slides de aula, 25 páginas numeradas + capa)
privacy: private
source_url: none (material didático interno, sem link público informado)
local_file: none (fonte privada fornecida pelo usuário via chat — sem cópia versionada; originais mantidos apenas localmente pelo usuário; pasta wiki/sources/files/private/ ignorada pelo Git)
received: 2026-10-06
availability: privada; usuário solicitou não salvar para o GitHub — nenhuma cópia em wiki/sources/files/public/ ou private/ foi versionada
topics:
  - QuickCheck
  - Teste baseado em propriedades
  - Haskell
  - Leis condicionais
  - Contraexemplos
  - Monitoramento de dados de teste
related_subjects:
  - SUB-0001
  - SUB-0010
knowledge:
  - SUM-0020
bibliography_noted:
  - Claessen, K., and Hughes, J. Quickcheck: A lightweight tool for random testing of haskell programs. ICFP '00, ACM, pp. 268–279.
---

# SRC-0020 — QuickCheck: Introdução a testes baseados em propriedades (slides)

- **Fonte**: slides de aula "QuickCheck — Introdução a testes baseados em propriedades", de Márcio Lopes Cornélio (CIn-UFPE). Conteúdo recebido como texto extraído + imagens de 25 slides.
- **Privacidade**: material do professor; usuário indicou que os arquivos são privados e não podem ir para o GitHub. Nenhum PDF foi copiado para `wiki/sources/files/`; o conhecimento derivado (SUM-0020, SUB-0010) foi redigido com palavras próprias, sem reprodução literal dos slides.
- **Escopo geral**: motivação do teste automático (custo, repetição após modificações, adequação de programas funcionais puros); QuickCheck como DSL de especificações testáveis no mesmo módulo do código; geração aleatória de dados; benefícios (pensar no comportamento esperado, achar casos limítrofes, documentação verificável por máquina); exemplos `mNot`, `exOr`, `maxi`/`max'`, contraexemplo `prop_max3`; leis de `reverse`/`++`; leis condicionais com `==>` e tipo `Property`; propriedades de `qsort` (idempotência, min/max, comparação com `sort` de `Data.List`, bug com duplicatas); monitoramento com `classify`/`collect`/`forAll`/`orderedList`; estruturas infinitas com `cycle`/`take`; exercícios (`threeDifferent`, `fourEqual` via `threeEqual`); bibliografia do artigo seminal.
- **Relação**: complementa SRC-0021 (geradores de dados); ambos sustentam SUB-0010. Relaciona-se a SUB-0001 (fundamentos de Haskell) como aplicação de teste.
