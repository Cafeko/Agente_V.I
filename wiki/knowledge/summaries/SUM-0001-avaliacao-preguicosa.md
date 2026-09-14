---
id: SUM-0001
type: summary
source: SRC-0001
title: Summary — Avaliação Preguiçosa (slides)
created: 2026-09-14
related_subjects:
  - SUB-0001
---

# O que esta fonte apresenta (SRC-0001)

> Síntese redigida com palavras próprias a partir dos slides privados SRC-0001.
> Sem citações literais; exemplos abaixo são paráfrases dos apresentados na fonte.

## Ordem de avaliação

- Em Haskell, duas ordens de avaliação diferentes da mesma expressão produzem o mesmo
  resultado final, desde que ambas terminem — o que não vale para linguagens imperativas,
  onde atribuições intermediárias tornam o resultado dependente do momento da avaliação.
- **Redex** (expressão redutível): função aplicada a argumentos, pronta para ser reduzida.
- **Innermost**: escolhe o redex mais interno (que não contém outro); desempata pela esquerda.
  Argumentos são totalmente avaliados antes da aplicação — passagem **por valor**
  (call-by-value).
- **Outermost**: escolhe o redex mais externo (não contido em outro); desempata pela esquerda.
  Funções são aplicadas antes de avaliar os argumentos — passagem **por nome** (call-by-name).
- Em corpos de expressões lambda não se reduz internamente: `(\x -> 1+2)` já está avaliada;
  a única operação sobre uma função é aplicá-la.

## Terminação e custo

- Call-by-name termina sempre que **alguma** ordem de avaliação termina
  (ex.: `fst (0, inf)` termina por nome, mas diverge por valor).
- Call-by-name pode repetir trabalho (ex.: `square (1+2)` duplica `(1+2)`); call-by-value
  avalia cada argumento exatamente uma vez.

## Avaliação preguiçosa

- Definição da fonte: call-by-name **com compartilhamento** (ponteiros para expressões).
- Garante terminação sempre que possível e nunca exige mais passos que call-by-value;
  cada argumento é avaliado **no máximo uma vez** (computação sobre grafos).
- Ordem de avaliação em Haskell: de fora para dentro; no mesmo nível, da esquerda para a direita.
- Argumentos de funções são avaliados só quando necessários — e só nas partes necessárias
  (é o que dirige casamento de padrões, guardas e cláusulas `where`, calculadas sob demanda).
- Viabiliza **estruturas infinitas** (ex.: lista infinita de 1s, consumida via `head`)
  e **programação modular**: separação entre dados (lista infinita) e controle
  (ex.: `take 3 ones`), avaliando o dado só quando o controle requisita.

## Compreensão de listas

- Forma `[e | q1..qk]`, onde cada qualificador é um **gerador** (`p <- lista`) ou um **teste**
  (expressão booleana). Exemplos da fonte: pares, triplas pitagóricas, permutações.
- Tradução para funções básicas (confirma as equivalências das anotações do usuário):
  identidade, `map`, `filter` para testes, e `concat` para geradores múltiplos.
- A fonte também apresenta um cálculo direto por substituição como alternativa à tradução.
