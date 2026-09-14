---
id: SUM-0007
type: summary
source: SRC-0007
title: Summary — iStar 2.0 Language Guide
created: 2026-09-14
related_subjects:
  - SUB-0004
---

# O que esta fonte apresenta (SRC-0007)

> Síntese com palavras próprias do guia público iStar 2.0 (arXiv:1605.07767v3).

## Motivação

- i* (anos 1990) modela as dimensões intencional (por quê?), social (quem?) e estratégica
  (como? de que outro jeito?) — mas a proliferação de extensões dificultava o aprendizado e o
  ensino. O iStar 2.0 fixa um núcleo consensual de conceitos, mantida a abertura para adaptar.

## Atores (§2–§3)

- **Ator**: entidade ativa e autônoma que busca objetivos colaborando com outros.
- **Role** (papel): caracterização abstrata de comportamento num contexto (ex.: Estudante,
  PhD Student). **Agent**: manifestação concreta — pessoa, organização, departamento
  (ex.: Mike White, Travel Agency). O ator genérico usa-se quando a distinção não importa ainda.
- **Fronteira do ator**: contêiner gráfico dos seus elementos intencionais e relações internas.
- **is-a**: só entre role↔role ou ator↔ator (agentes não se especializam). **participates-in**:
  qualquer outra associação — com agente→role lê-se *plays*, mesmo tipo lê-se em geral *part-of*.
  No máximo **um** link entre cada par de atores; sem ciclos.

## Elementos intencionais (§4)

- **Goal**: estado de coisas com critério claro de cumprimento. **Quality**: atributo com nível
  desejado de alcance (preciso ou vago) — substitui a dicotomia goal/softgoal e a distinção
  funcional/não-funcional; guia a busca e avalia alternativas. **Task**: ação a executar,
  em geral para cumprir um goal. **Resource**: entidade física ou informacional necessária à task.
- Notação: oval (goal), nuvem (quality), hexágono (task), retângulo (resource).

## Dependências sociais (§5)

- Cinco argumentos: **depender**, **dependerElmt** (o porquê, dentro da fronteira do depender),
  **dependum** (o objeto, fora das fronteiras), **dependee**, **dependeeElmt** (o como).
  Notação "D" como seta do depender ao dependee passando pelo dependum.
- dependerElmt e dependeeElmt são opcionais (conhecimento parcial ou visão SD inicial).
- O tipo do dependum define a liberdade do dependee: goal/quality (máxima — escolhe o como),
  task (média — executa como prescrito), resource (mínima — disponibiliza).
- Regras: cada dependum pertence a uma só dependência; dependerElmt não pode ser refinado nem
  receber contribuição; depender e dependee distintos; nomes iguais em lados distintos continuam
  elementos distintos (pontos de vista separados).

## Ligações entre elementos (§6)

- **Refinement** (genérico, n-ário, um pai em no máximo um refinamento): **AND** (todos os
  filhos cumprem o pai) ou **OR** (basta um; admite filho único) — nunca ambos. O sentido varia
  com o tipo do pai (sub-estado, meio/fim, sub-tarefa, goal descoberto na análise da task).
  Setas dos filhos ao pai: cabeça em T (AND), seta sólida (OR). Vale bottom-up ou top-down.
- **NeededBy**: task precisa do resource (sem dizer o motivo: consumo, leitura etc.).
- **Contribution** (para qualities, acumulando evidência): Make (suficiente a favor), Help
  (fraca a favor), Hurt (fraca contra), Break (suficiente contra). Origem pode ser qualquer
  elemento; qualities falam-se em *satisfeita* (evidência suficiente) ou *negada*.
- **Qualification** (tracejado): quality sobre seu sujeito (task, goal, resource) — ex. "No
  errors" qualifica "Request prepared". Quality pode existir solta, sem qualificar nada.
- Restrição: um par elemento–quality liga-se por contribuição **ou** qualificação, nunca ambos;
  quality não contribui para si mesma.

## Visões (§7) e metamodelo (§8)

- **SR** (Strategic Rationale): tudo, incluindo interiores dos atores. **SD** (Strategic
  Dependency): atores, links e dependências. **Híbrida**: alguns atores abertos, outros não.
  Outras possíveis: só atores, funcional (sem qualities).
- Metamodelo com classes abstratas (GoalTask Element, Intentional Element, Refinement) e
  restrições de integridade (as das seções acima, mais: sem ciclos de refinamento; links entre
  elementos só dentro do mesmo ator).
