---
id: SUB-0004
type: subject
title: iStar 2.0 — linguagem de modelagem intencional
created: 2026-09-14
updated: 2026-09-14
sources:
  - SRC-0007
knowledge:
  - SUM-0007
related_subjects: []
---

# iStar 2.0 — linguagem de modelagem intencional

> O que a Wiki sabe sobre iStar 2.0: guia da linguagem (SRC-0007) via SUM-0007.
> Leitura vista em aula em 2026-09-14 (disciplina de origem não registrada).

## Ideia central

Linguagem sócio-técnica para modelar **por quê** (intencional), **quem** (social) e
**como / de que outro jeito** (estratégico). Núcleo padronizado do framework i*,
pensado como referência comum para ensino e ferramentas.

## Vocabulário básico

- **Atores**: Role (abstrato: Estudante) vs Agent (concreto: Mike White, uma agência).
  Fronteira delimita o interior intencional de cada ator.
- **Links entre atores**: is-a (generalização, só role↔role ou ator↔ator) e participates-in
  (plays, part-of); um link por par, sem ciclos.
- **Elementos intencionais**: Goal (critério claro), Quality (nível desejado, preciso ou vago),
  Task (ação), Resource (entidade necessária).
- **Dependências** (depender → dependum → dependee, com porquê/como opcionais): o tipo do
  dependum calibra a autonomia do dependee — goal/quality deixam o como livre; task prescreve;
  resource só exige disponibilidade.
- **Ligações internas**: refinement AND/OR (decomposição e alternativas/meios-fins),
  neededBy (task–resource), contribution Make/Help/Hurt/Break (evidência para qualities) e
  qualification (quality sobre seu sujeito).

## Visões de um modelo

SR (detalhe total), SD (só atores e dependências) e híbrida (alguns atores abertos);
o metamodelo fixa as restrições de integridade (sem ciclos, um refinamento por pai,
links internos ao mesmo ator, sem dependum compartilhado).

---

## Proveniência

- Todo o conteúdo deriva de [SRC-0007](../sources/metadata/SRC-0007-istar2-guide.md)
  via [SUM-0007](../knowledge/summaries/SUM-0007-istar2-guide.md).
- Original público no arXiv ([abs](https://arxiv.org/abs/1605.07767) · [pdf](https://arxiv.org/pdf/1605.07767)); sem cópia local.
- Exemplo de referência do guia: reembolso de viagens universitárias.
