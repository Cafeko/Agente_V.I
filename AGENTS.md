# AGENTS.md

## 1. Objetivo

Esta é uma LLM Wiki: uma base de conhecimento persistente mantida por um agente de IA.

O agente deve:

* consultar a Wiki para responder perguntas;
* adicionar novas fontes e informações;
* criar e atualizar subjects;
* criar summaries, comparisons e syntheses quando apropriado;
* manter os relacionamentos entre os conteúdos;
* manter o índice de navegação;
* preservar a origem das informações;
* evitar duplicações e inconsistências;
* manter a estrutura da Wiki organizada.

A Wiki deve ser tratada como uma base de conhecimento viva. O agente deve preferir **atualizar e relacionar informações existentes** em vez de criar conteúdos duplicados.

---

# 2. Estrutura

A estrutura principal é:

```text
llm-wiki/
│
├── wiki/
│   ├── sources/
│   │   ├── metadata/
│   │   └── files/
│   │       ├── public/
│   │       └── private/
│   │
│   ├── subjects/
│   │
│   ├── user_input/
│   │
│   ├── knowledge/
│   │   ├── summaries/
│   │   ├── comparisons/
│   │   └── syntheses/
│   │
│   └── index/
│       └── navigation_index.md
│
├── AGENTS.md
├── README.md
└── .gitignore
```

Cada diretório possui uma função específica. O agente não deve criar novas categorias ou diretórios sem necessidade.

---

# 3. Princípios gerais

## 3.1 Preservar a origem

Toda informação importante incorporada à Wiki deve ter sua origem identificável sempre que possível.

As possíveis origens incluem:

* uma fonte externa;
* um arquivo;
* uma informação fornecida diretamente pelo usuário;
* outro conhecimento já existente na Wiki.

Não apresentar como fato independente uma informação cuja origem não possa ser determinada quando essa origem for relevante.

---

## 3.2 Não modificar fontes originais

Arquivos armazenados em `wiki/sources/files/` são fontes originais e devem ser tratados como imutáveis.

O agente deve criar conhecimento derivado da fonte em vez de modificar a fonte original.

---

## 3.3 Evitar duplicação

Antes de criar um novo conteúdo, o agente deve verificar se já existe:

* um source equivalente;
* um subject equivalente;
* um summary da mesma fonte;
* uma comparison equivalente;
* uma synthesis equivalente.

Quando existir conteúdo relacionado, preferir atualizá-lo ou relacioná-lo ao novo conteúdo.

---

## 3.4 Não inventar informações

O agente não deve preencher lacunas com informações inventadas.

Quando uma informação não puder ser determinada a partir das fontes disponíveis, deve indicar a incerteza.

---

## 3.5 Preservar informações conflitantes

Se duas fontes apresentarem informações diferentes, o agente não deve simplesmente escolher uma e apagar a outra.

Deve:

1. identificar o conflito;
2. preservar as fontes;
3. indicar as informações conflitantes;
4. informar, quando possível, qual fonte apresenta cada afirmação.

---

# 4. IDs

Os elementos persistentes devem possuir identificadores únicos.

Usar os seguintes formatos:

```text
SRC-0001    → Source
SUB-0001    → Subject
USER-0001   → User input
SUM-0001    → Summary
CMP-0001    → Comparison
SYN-0001    → Synthesis
```

O número deve ser incrementado para novos elementos do mesmo tipo.

Nunca reutilizar um ID que já tenha sido utilizado.

O ID deve permanecer estável mesmo que o nome ou caminho do arquivo seja alterado.

---

# 5. Sources

Sources representam as fontes originais utilizadas pela Wiki.

Uma source pode ser:

* página web;
* artigo;
* livro;
* vídeo;
* documento;
* arquivo fornecido pelo usuário;
* outra fonte externa identificável.

## 5.1 Fontes públicas

Quando existir uma URL pública e adequada para recuperar a fonte, preferir armazenar seus metadados e o endereço da fonte em vez de manter uma cópia local desnecessária.

Exemplo:

```yaml
id: SRC-0001
type: article
title: Nome do artigo
author: Nome do autor
url: https://example.com/article
visibility: public
accessed_at: 2026-09-14
```

---

## 5.2 Arquivos

Um arquivo deve ser armazenado localmente quando não houver uma forma pública adequada de recuperá-lo posteriormente.

Arquivos ficam em:

```text
wiki/sources/files/public/
wiki/sources/files/private/
```

---

## 5.3 Fontes privadas

Arquivos privados devem ficar em:

```text
wiki/sources/files/private/
```

Eles não devem ser disponibilizados publicamente.

Informações derivadas de uma fonte privada podem ser utilizadas na Wiki, mas devem indicar sua origem.

Exemplo:

```yaml
id: SRC-0005
type: file
visibility: private
path: sources/files/private/SRC-0005.pdf
```

Quando necessário, indicar no conteúdo:

> Esta informação foi obtida de uma fonte privada fornecida pelo usuário. O arquivo original não pode ser disponibilizado.

Nunca substituir uma fonte privada por uma URL inventada ou tentar tornar público seu conteúdo sem autorização.

---

# 6. Subjects

Subjects representam assuntos ou entidades sobre os quais a Wiki mantém conhecimento acumulado.

Exemplos:

```text
subjects/
├── retrieval-augmented-generation.md
├── openai.md
├── machine-learning.md
└── ...
```

Um subject pode representar:

* pessoa;
* empresa;
* organização;
* conceito;
* tecnologia;
* projeto;
* filme;
* série;
* franquia;
* ou qualquer outro assunto persistente.

## 6.1 Criar um subject

Antes de criar um subject, verificar se já existe um subject equivalente.

Criar um novo subject quando:

* o assunto possui identidade própria;
* provavelmente será reutilizado;
* possui ou poderá possuir múltiplas informações relacionadas;
* merece uma página própria na Wiki.

Não criar um subject para cada informação isolada.

---

## 6.2 Atualizar um subject

Quando uma nova fonte trouxer informações sobre um subject existente, atualizar o subject em vez de criar outro.

Manter referências para as fontes e conhecimentos relevantes.

Exemplo de frontmatter:

```yaml
---
id: SUB-0001
type: subject
title: Retrieval-Augmented Generation
created: 2026-09-14
updated: 2026-09-14

sources:
  - SRC-0001
  - SRC-0004

related_subjects:
  - SUB-0002

knowledge:
  - SUM-0001
  - CMP-0001
  - SYN-0002
---
```

---

# 7. User Input

Informações fornecidas diretamente pelo usuário devem ser registradas em:

```text
wiki/user_input/
```

Exemplo:

```text
USER-0001.md
```

User input deve ser utilizado para preservar informações que não vieram de uma fonte externa.

Uma pergunta do usuário, por si só, não precisa ser armazenada.

Exemplo:

```text
"Compare RAG e fine-tuning."
```

é uma solicitação.

Não transformar automaticamente essa solicitação em conhecimento persistente.

Se o resultado da solicitação for considerado útil para a Wiki, ele pode ser armazenado como uma comparison ou synthesis.

---

# 8. Knowledge

O diretório `knowledge/` contém informações produzidas ou organizadas a partir das fontes, subjects e user inputs.

Ele possui três tipos principais:

```text
knowledge/
├── summaries/
├── comparisons/
└── syntheses/
```

---

# 9. Summaries

Um summary é um resumo de uma fonte específica.

Ele responde:

> O que esta fonte apresenta?

Um summary deve estar associado principalmente a uma única source.

Exemplo:

```text
knowledge/summaries/SRC-0001.md
```

Um summary pode conter:

* ideia principal;
* principais informações;
* argumentos;
* resultados;
* conclusões;
* informações relevantes para a Wiki.

Não adicionar informações externas ao resumo sem indicar claramente que elas vieram de outra origem.

---

# 10. Comparisons

Uma comparison compara dois ou mais elementos.

Ela responde:

> Como X e Y são semelhantes ou diferentes?

Uma comparison pode utilizar:

* subjects;
* sources;
* summaries;
* outras informações da Wiki.

Exemplo:

```text
knowledge/comparisons/rag-vs-fine-tuning.md
```

A comparison deve deixar claro quais elementos estão sendo comparados e quais informações serviram de base.

Quando a comparação contiver conclusões que dependem de informações externas, registrar suas fontes.

---

# 11. Syntheses

Uma synthesis combina informações provenientes de diferentes elementos para produzir uma visão integrada.

Ela responde:

> O que podemos concluir considerando essas informações em conjunto?

Uma synthesis pode utilizar:

* sources;
* user inputs;
* subjects;
* summaries;
* comparisons;
* outras syntheses.

A synthesis não deve simplesmente concatenar conteúdos.

Ela deve produzir uma interpretação ou conclusão baseada nas informações disponíveis, deixando claras suas bases.

Quando houver incertezas ou conflitos entre as fontes, eles devem ser explicitados.

---

# 12. Relacionamentos

Não existe um arquivo separado de relacionamentos.

Os relacionamentos devem ser registrados nos próprios documentos através de:

* frontmatter;
* links Markdown;
* referências por ID.

Exemplo:

```yaml
related_subjects:
  - SUB-0002

sources:
  - SRC-0001

knowledge:
  - SUM-0001
  - CMP-0001
```

Isso evita que exista uma segunda fonte de verdade contendo os relacionamentos.

Sempre que possível, utilizar links Markdown para permitir navegação direta entre os conteúdos.

---

# 13. Navigation Index

O arquivo:

```text
wiki/index/navigation_index.md
```

serve para responder:

> O que existe na Wiki e onde está?

Ele deve conter referências para os principais conteúdos da Wiki e uma descrição curta.

Exemplo:

```markdown
# Navigation Index

## Subjects

- [Retrieval-Augmented Generation](../subjects/retrieval-augmented-generation.md)
  Técnica relacionada à recuperação de informações para LLMs.

## Knowledge

- [Resumo SRC-0001](../knowledge/summaries/SRC-0001.md)
  Resumo da fonte SRC-0001.

- [RAG vs Fine-tuning](../knowledge/comparisons/rag-vs-fine-tuning.md)
  Comparação entre as duas abordagens.
```

O índice é um mecanismo de navegação, não a fonte de verdade.

Se necessário, ele deve poder ser reconstruído a partir dos arquivos da Wiki.

---

# 14. Busca e consulta

Ao responder uma pergunta do usuário, o agente deve primeiro utilizar o conhecimento existente na Wiki quando ele for relevante.

Uma estratégia básica é:

```text
Pergunta
   ↓
Navigation Index
   ↓
Subjects relevantes
   ↓
Knowledge relevante
   ↓
Sources necessárias
   ↓
Resposta
```

Não é necessário consultar todos os arquivos da Wiki para cada pergunta.

O agente deve localizar primeiro os conteúdos mais relevantes.

Quando a Wiki não possuir informações suficientes, o agente pode buscar novas fontes externas caso tenha acesso a ferramentas apropriadas.

Informações externas novas devem ser tratadas como novas sources antes de serem incorporadas ao conhecimento persistente.

---

# 15. Adição de novas informações

Ao receber uma nova fonte ou informação:

1. Identificar a origem.
2. Verificar se a fonte já existe.
3. Criar um novo ID somente se necessário.
4. Registrar os metadados.
5. Determinar se o conteúdo deve ser armazenado como arquivo ou apenas como referência.
6. Identificar subjects existentes relacionados.
7. Criar novos subjects somente quando necessário.
8. Criar ou atualizar summaries, comparisons ou syntheses quando apropriado.
9. Adicionar os relacionamentos.
10. Atualizar o navigation index.
11. Verificar se existem inconsistências ou duplicações.

---

# 16. Atualização de informações

Quando uma nova fonte atualizar uma informação existente:

1. localizar o conteúdo existente;
2. verificar sua origem;
3. comparar a nova informação com a anterior;
4. preservar a referência às fontes relevantes;
5. atualizar o conteúdo quando a nova informação for mais atual ou relevante;
6. preservar informações históricas quando elas forem importantes;
7. atualizar `updated`;
8. atualizar os relacionamentos afetados;
9. atualizar o índice caso necessário.

Não apagar informações antigas simplesmente porque existe uma informação nova, especialmente quando elas representam estados diferentes em momentos diferentes.

---

# 17. Manutenção

Periodicamente, o agente deve verificar:

* links quebrados;
* referências para IDs inexistentes;
* arquivos sem metadados;
* metadados sem arquivo correspondente quando necessário;
* subjects duplicados;
* knowledge duplicado;
* conteúdos sem origem quando uma origem deveria existir;
* entradas incorretas no navigation index;
* relacionamentos que apontam para conteúdos inexistentes.

O agente deve corrigir problemas simples automaticamente quando tiver segurança para fazê-lo.

Problemas ambíguos devem ser apresentados ao usuário em vez de serem resolvidos por suposição.

---

# 18. Git

O Git deve ser utilizado para versionar a Wiki.

O agente pode utilizar Git para:

* verificar alterações;
* revisar mudanças;
* identificar arquivos modificados;
* criar commits quando autorizado pelas regras do ambiente.

Exemplos de mensagens de commit:

```text
wiki: add RAG subject
wiki: add summary for SRC-0004
wiki: add RAG vs fine-tuning comparison
wiki: update RAG information
wiki: maintenance - fix broken links
```

O histórico do Git deve ser utilizado para acompanhar a evolução da Wiki.

---

# 19. Segurança e privacidade

Informações privadas devem permanecer privadas.

O agente não deve:

* publicar arquivos privados;
* copiar conteúdo privado para uma fonte pública;
* colocar arquivos privados em commits destinados a repositórios públicos;
* inventar URLs para fontes privadas;
* revelar informações privadas sem autorização.

O conteúdo derivado de uma fonte privada pode ser utilizado na Wiki quando permitido, mas sua origem deve continuar identificável como privada.

---

# 20. Regra de ouro

Ao modificar a Wiki, o agente deve sempre considerar:

```text
1. De onde veio esta informação?
2. Ela já existe na Wiki?
3. A que subject ela pertence?
4. É um summary, comparison ou synthesis?
5. Com quais outros elementos ela se relaciona?
6. Como preservar sua proveniência?
7. O que precisa ser atualizado por causa dessa alteração?
```

O objetivo não é simplesmente adicionar arquivos.

O objetivo é manter uma base de conhecimento **organizada, rastreável, interligada, atualizável e confiável**.
