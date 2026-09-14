---
id: SUM-0002
type: summary
source: SRC-0002
title: Summary — Raciocinando sobre programas (slides)
created: 2026-09-14
related_subjects:
  - SUB-0001
---

# O que esta fonte apresenta (SRC-0002)

> Síntese redigida com palavras próprias a partir dos slides privados SRC-0002.
> Sem citações literais; equações abaixo são propriedades-padrão da linguagem,
> apresentadas na fonte como objetos de prova.

## Definições como descrições

- Funções podem ser lidas como **descrições lógicas** do que fazem: cada equação de
  definição (ex.: os dois casos de `length`) descreve o comportamento da função.
- Três formas de entender uma definição: testar no interpretador, avaliar manualmente
  ou argumentar sobre o comportamento; a fonte segue a terceira.
- **Avaliação simbólica**: calcular com variáveis em vez de valores concretos
  (ex.: deduzir `length [x] = 1` a partir dos dois casos de `length`), chegando a
  propriedades gerais como `length (xs ++ ys) = length xs + length ys`.

## Terminação

- Avaliar pode terminar com resposta ou prosseguir para sempre (ex.: `fact` com
  entrada negativa); valores de avaliações que não terminam são **indefinidos**.
  As provas da fonte concentram-se em valores definidos.

## Indução estrutural sobre listas

- Princípio (para listas **finitas**): provar `P([])` (caso base) e provar
  `P(x:xs)` assumindo `P(xs)` como **hipótese de indução**.
- Casos provados na fonte, sempre reduzindo os dois lados até coincidirem:
  - `sum (doubleAll xs) = 2 * sum xs`;
  - `length (xs ++ ys) = length xs + length ys`;
  - `reverse (xs ++ ys) = reverse ys ++ reverse xs` — cujo passo indutivo exige a
    associatividade de `++` (provada à parte, com a identidade `xs ++ [] = xs`);
  - eliminação de `++` em `flatten` de árvores via versão acumuladora `flatten'`,
    com indução sobre a estrutura da árvore.
- Exercícios propostos (não resolvidos na fonte): `sum` distribuído sobre `++`
  e as duas leis de `++` (identidade e associatividade).

## Corretude de compilador

- Objeto: expressões (`Val`/`Add`) avaliadas diretamente (`eval`) ou compiladas
  (`comp`) para código de máquina de pilha (`PUSH`/`ADD`, executado por `exec`).
- Teorema: `exec (comp e) [] = [eval e]` — compilar e executar sobre pilha vazia
  equivale a avaliar e empilhar o resultado.
- Prova por indução sobre a expressão, na forma generalizada
  `exec (comp e) s = eval e : s`, usando o lema da **distributividade**
  (`exec (c++d) s = exec d (exec c s)`), ele próprio provado por indução sobre o código.
