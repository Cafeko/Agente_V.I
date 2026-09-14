# AGENTS.md — LLM Wiki

## 1. Objetivo

Esta Wiki é uma base de conhecimento persistente mantida por um agente LLM.

O agente deve:

* registrar fontes e seus metadados;
* transformar fontes em conhecimento útil;
* relacionar conhecimentos, assuntos e fontes;
* incorporar informações fornecidas pelo usuário;
* atualizar conhecimentos existentes quando necessário;
* preservar a proveniência das informações;
* manter a Wiki navegável e consistente.

**Regra principal:** a Wiki deve armazenar conhecimento real, não apenas metadados, índices ou referências.

---

## 2. Estrutura

```text
llm-wiki/
├── wiki/
│   ├── sources/
│   │   ├── metadata/
│   │   └── files/
│   │       ├── public/
│   │       └── private/
│   ├── subjects/
│   ├── user_input/
│   ├── knowledge/
│   │   ├── summaries/
│   │   ├── comparisons/
│   │   └── syntheses/
│   └── index/
│       └── navigation_index.md
├── AGENTS.md
├── README.md
└── .gitignore
```

Não crie novas categorias ou diretórios sem necessidade real.

---

## 3. Regra de operação

Antes de criar ou alterar qualquer conteúdo:

1. Leia este `AGENTS.md`.
2. Examine a estrutura existente.
3. Procure documentos relacionados ao assunto.
4. Reutilize documentos existentes quando apropriado.
5. Evite duplicação.
6. Preserve IDs já existentes.
7. Após alterações, atualize os índices afetados.

Nunca presuma que um assunto, fonte ou conhecimento ainda não existe sem pesquisar.

---

## 4. Tipos de informação

### Source

Representa uma fonte externa ou arquivo original.

Exemplos:

* artigo;
* livro;
* documentação;
* página web;
* vídeo;
* PDF;
* repositório.

A source registra **de onde a informação veio**.

### User Input

Representa informação fornecida diretamente pelo usuário.

Pode conter:

* conhecimento;
* observações;
* opiniões;
* hipóteses;
* correções;
* contexto.

Não trate automaticamente uma opinião do usuário como fato externo.

### Summary

Resume uma única source.

Pergunta respondida:

> "O que esta fonte apresenta?"

Cada summary possui seu próprio ID.

Exemplo:

```yaml
id: SUM-0001
type: summary
source: SRC-0001
```

**Não use o ID da source como ID do summary.**

### Subject

Representa um assunto, entidade, conceito ou objeto persistente sobre o qual a Wiki acumula conhecimento.

Um subject **deve conter conhecimento substantivo**.

Pode receber informações de:

* várias sources;
* vários summaries;
* user inputs;
* comparisons;
* syntheses.

Um subject **não deve ser apenas YAML, metadados ou uma lista de referências**.

### Comparison

Registra uma comparação estruturada entre dois ou mais assuntos, conceitos, entidades ou informações.

Deve apresentar:

* o que está sendo comparado;
* critérios relevantes;
* semelhanças;
* diferenças;
* conclusão, quando apropriado.

### Synthesis

Integra informações provenientes de múltiplas fontes ou conhecimentos.

Uma synthesis deve produzir uma conclusão ou entendimento integrado, e não apenas juntar resumos.

---

## 5. IDs

Use IDs estáveis e únicos por tipo:

```text
SRC-0001  → source
SUB-0001  → subject
USR-0001  → user input
SUM-0001  → summary
CMP-0001  → comparison
SYN-0001  → synthesis
```

Regras:

* nunca reutilize um ID;
* não altere IDs existentes sem necessidade;
* não confunda IDs de tipos diferentes;
* antes de criar um ID, verifique os existentes;
* referências devem usar os IDs corretos.

---

## 6. Sources

Ao adicionar uma source:

1. registre seus metadados;
2. armazene o arquivo, quando aplicável;
3. identifique os subjects relacionados;
4. produza um summary quando houver conteúdo suficiente;
5. incorpore o conhecimento relevante aos subjects;
6. crie comparisons ou syntheses quando justificadas;
7. atualize o índice.

A source original deve ser preservada sempre que possível.

Não invente informações sobre uma source.

---

## 7. Subjects

Subjects são páginas de conhecimento persistente.

Um subject deve responder, de forma progressivamente acumulativa:

> "O que a Wiki sabe sobre este assunto?"

Pode conter:

* definição;
* características;
* funcionamento;
* histórico;
* exemplos;
* aplicações;
* informações relevantes;
* relações;
* divergências;
* conclusões;
* referências às sources que sustentam cada informação.

Quando uma nova fonte acrescentar conhecimento a um subject existente, **atualize o subject em vez de criar outro subject duplicado**.

Exemplo insuficiente:

```yaml
---
id: SUB-0001
type: subject
title: Exemplo
sources:
  - SRC-0001
knowledge:
  - SUM-0001
---
```

Isso apenas referencia conhecimento.

O subject deve possuir conteúdo substantivo além dessas referências.

---

## 8. User Input

Informações fornecidas pelo usuário devem ser registradas quando forem relevantes para a base de conhecimento.

Diferencie claramente:

* fato fornecido pelo usuário;
* opinião;
* hipótese;
* interpretação;
* correção;
* informação proveniente de fonte externa.

Não transforme automaticamente user input em conhecimento factual confirmado.

Quando apropriado, registre a origem da informação.

---

## 9. Knowledge

Conhecimento deve ser organizado de acordo com sua função:

```text
knowledge/
├── summaries/
├── comparisons/
└── syntheses/
```

Não coloque tudo em summaries.

Use:

* `summary` → uma fonte;
* `comparison` → comparação;
* `synthesis` → integração de múltiplas informações.

O conhecimento mais importante e persistente sobre um assunto deve também estar disponível no respectivo `subject`.

---

## 10. Proveniência

Toda informação derivada de uma fonte deve permitir descobrir sua origem.

Sempre que possível, mantenha relações como:

```text
Source
  ↓
Summary
  ↓
Subject
  ↓
Comparison / Synthesis
```

Uma informação pode ter múltiplas fontes.

Uma source pode contribuir para múltiplos subjects.

Não atribua uma informação a uma fonte que não a sustenta.

Quando houver conflito entre fontes, preserve o conflito e indique as diferentes posições em vez de escolher arbitrariamente uma delas.

---

## 11. Relações

Relações devem ser registradas diretamente nos documentos usando:

* IDs;
* frontmatter;
* links Markdown;
* referências explícitas no texto.

Exemplos:

```yaml
sources:
  - SRC-0001

related_subjects:
  - SUB-0002

knowledge:
  - SUM-0001
  - SYN-0001
```

Não crie um índice separado de relações apenas para duplicar essas informações.

---

## 12. Navigation Index

`wiki/index/navigation_index.md` serve para responder:

> "O que existe na Wiki e onde está?"

O índice deve apontar para:

* sources;
* subjects;
* user inputs;
* summaries;
* comparisons;
* syntheses.

O índice **não é a fonte de verdade**.

O conteúdo real deve permanecer nos documentos correspondentes.

Após criar, remover ou renomear documentos, atualize o índice.

---

## 13. Pesquisa antes de criação

Antes de criar qualquer documento, pesquise por:

* título;
* assunto;
* entidades relacionadas;
* IDs;
* conceitos equivalentes;
* documentos semelhantes.

Se já existir conteúdo relacionado:

* atualize-o, se representar o mesmo objeto;
* complemente-o, se houver nova informação;
* crie um novo documento somente se representar algo realmente distinto.

Evite criar documentos duplicados.

---

## 14. Atualização

Ao adicionar nova informação:

1. localize o conhecimento existente;
2. determine se a informação é nova, complementar ou conflitante;
3. atualize o documento apropriado;
4. preserve informações anteriores quando ainda forem relevantes;
5. registre a nova proveniência;
6. atualize `updated`;
7. atualize o índice se necessário.

Não substitua conteúdo antigo simplesmente porque encontrou uma fonte nova.

---

## 15. Contradições e incerteza

Não invente respostas para preencher lacunas.

Quando houver incerteza:

```text
Não confirmado
Possível interpretação
Fonte A afirma X
Fonte B afirma Y
```

Quando houver conflito entre fontes, mantenha as posições separadas e explique a diferença quando houver evidência suficiente.

---

## 16. Segurança e privacidade

Informações privadas devem permanecer em:

```text
wiki/sources/files/private/
```

Não exponha conteúdo privado em:

* fontes públicas;
* summaries públicos;
* README;
* índices públicos;
* Git, quando o conteúdo não deveria ser versionado.

Revise `.gitignore` antes de adicionar arquivos potencialmente privados.

---

## 17. Git

O Git deve preservar o histórico da Wiki.

Antes de alterações importantes:

* verifique o estado do repositório;
* evite sobrescrever alterações do usuário;
* não remova arquivos sem motivo;
* não faça commits contendo dados privados.

Commits devem representar mudanças coerentes na base.

---

## 18. Manutenção

Periodicamente procure por:

* IDs duplicados;
* referências quebradas;
* documentos duplicados;
* subjects sem conhecimento substantivo;
* summaries sem source;
* referências para documentos inexistentes;
* arquivos privados expostos;
* índice desatualizado;
* metadados inconsistentes.

Corrija problemas sem apagar conhecimento válido.

---

## 19. Regra de decisão

Ao receber uma nova informação, siga esta sequência:

```text
Nova informação
      ↓
Pesquisar Wiki
      ↓
Já existe?
 ┌────┴────┐
SIM       NÃO
 ↓          ↓
Atualizar   Criar
 ↓          ↓
Relacionar ao subject
      ↓
Gerar summary/comparison/synthesis
quando necessário
      ↓
Atualizar índice
```

Não crie automaticamente todos os tipos de documento para toda informação.

Crie somente o que acrescentar valor.

---

## 20. Regra de ouro

**A Wiki deve acumular conhecimento útil, rastreável e navegável.**

Não confunda:

```text
metadados ≠ conhecimento
referência ≠ conteúdo
summary ≠ subject
source ≠ summary
comparison ≠ synthesis
índice ≠ fonte de verdade
```

Sempre prefira:

**pesquisar → entender → relacionar → atualizar → registrar a origem → manter a Wiki consistente.**
