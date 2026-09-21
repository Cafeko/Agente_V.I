---
id: SUM-0012
type: summary
source: SRC-0012
title: "Summary — Relatório GC1: Agência compartilhada entre humanos e IA"
created: 2026-09-21
related_subjects:
  - SUB-0007
---

# O que esta fonte apresenta (SRC-0012)

> Síntese com palavras próprias do relatório discente de 9 p. do Grupo GC1 (CIn-UFPE: Caio Ferreira, Gabriel Laporte, Ekistoclecio Heleno, Victor Amarante, Lucas de Holanda).

## 1. Enquadramento do GC1 e recorte

- GC1 do GranDIHC-BR = repensar **como** a IHC pesquisa: teorias/métodos consolidados foram feitos para sistemas determinísticos e subordinados, premissas que IA atual desfaz (SRC-0012:1).
- Duas frentes complementares (p.1): teórica (fundamentos em antropologia, linguística, psicologia, sociologia, design; fenomenologia; criar/sintetizar/aplicar teorias) e metodológica (novas formas de coleta/análise, design e avaliação). Não exige inventar teoria do zero.
- Recorte escolhido: **agência compartilhada humano-IA** porque é o ponto onde as duas frentes se encontram. Pergunta orientadora: “O que já sabemos sobre agência compartilhada em Interfaces Inteligentes e o que ainda precisamos investigar, desenvolver ou repensar?”
- Problema teórico: falta definição consensual — agência, autonomia, controle, iniciativa usados como sinônimos. Problema metodológico: falta de métodos/métricas para observar distribuição de iniciativa/decisão/responsabilidade em interações reais (Quadro p.1).

## 2. Sete problemas concretos (P1–P7, §2)

1. **P1 Ambiguidade** — iniciativa alterna a cada turno; ao final não se sabe quem definiu objetivo, escolheu alternativa e executou (piora quando um pedido dispara cadeia de decisões invisíveis).
2. **P2 Erosão do senso de agência** — sistema antecipa/completa/corrige antes da intenção; pessoa deixa de se sentir autora (impacta motivação/engajamento/responsabilidade).
3. **P3 Supervisão nominal** — human-in-the-loop vira cliques em “aprovar”; quanto mais confiável a automação, menos monitoramento/consciência situacional — ironia da automação (Bainbridge 1983).
4. **P4 Lacuna de responsabilidade** — culpa recai no humano mais próximo mesmo com pouco controle real; questão de design: responsabilidade proporcional ao controle oferecido?
5. **P5 Opacidade em cadeia** — ações longas em segundo plano sem registro legível nem ponto de parada/interrupção.
6. **P6 Dependência excessiva** — aceitação sem avaliação (transferência silenciosa de decisão, sem intenção explícita e sem aparecer na interface).
7. **P7 Autoria/propriedade** — em criação conjunta (texto/design/código) contribuição não rastreável → dimensões psicológica/propriedade, social/reconhecimento e jurídica/direitos sem resposta.

**Quem é afetado (Quadro 1, §2.8)**: clínica (profissionais/pacientes → erros aceitos, perda de habilidade); programação com assistentes (devs → revisão superficial, efeitos não previstos); serviços públicos digitais (cidadãos/servidores → responsabilidade difusa, falta de reparação); educação/escrita (estudantes/docentes → conflitos de autoria/integridade). Ponto cego transversal: maioria da evidência vem de alta escolaridade/alto letramento; quem menos letramento tem é quem menos consegue contestar e menos aparece nos estudos.

## 3. O que a literatura já investigou (§3, Quadro 2)

Marcos:
- 1983 Bainbridge — ironias da automação, humano fora do circuito;
- 1999 Horvitz — princípios de iniciativa mista sob incerteza;
- 2000 Sheridan & Verplank / Parasuraman et al. — níveis de automação por estágio (aquisição/análise/decisão/execução) → agência distribuída por etapas, não atributo único;
- 2017 Haggard — senso de agência (experiência de controlar ações e efeitos; medidas implícitas vs explícitas);
- 2022 Shneiderman — IA centrada no humano: alto controle + alta automação podem coexistir; agência como ampliação, não substituição.

Detalhamentos 3.1–3.5: graus por estágio, quando sistema deve iniciar (custo/benefício, escalonamento gradual), medição da experiência (decisões de interface como variáveis observáveis), dimensões independentes (controle vs automação), limites da supervisão (perda de habilidade/consciência).

**Revisões recentes (§3.6)**: Gomez et al. 2024 (105 art. decisão assistida → paradigmas simples, falta vocabulário comum); Zhang, Wang & Yi 2025 (134 art. cocriação → framework/catálogo de mecanismos); Feng et al. 2025 (5 níveis por papel do usuário: operador/colaborador/consultor/aprovador/observador, autonomia como decisão de design). Fora da academia: diretrizes Amershi et al. 2019, modos de aprovação/visualização de planos, regulação (AI Act art.14 supervisão efetiva, LGPD art.20 revisão de decisões automatizadas, PL 2338/2023). Contribuição brasileira: Engenharia Semiótica (De Souza 2005; Barbosa & Prates 2022) estendida a sistemas que geram suas próprias mensagens.

## 4. O que já foi desenvolvido (§4)

Quatro tipos:
- **4.1 Modelos conceituais (Quadro 3)**: Human-in-the-loop (pessoa valida cada passo → alto risco/baixo volume); Human-on-the-loop (sistema age, pessoa supervisiona → alto volume, vulnerável a supervisão nominal); Iniciativa mista (alternância de liderança → tarefas exploratórias/criativas); Autonomia ajustável (grau muda por etapa/risco/contexto → uso contínuo); Níveis por papel do usuário (cadeia operador→observador → sistemas que planejam em cadeia). Não concorrentes — adequados a risco/volume/tipo.
- **4.2 Diretrizes humano-IA** (Amershi et al.): deixar claro capacidades/qualidade, permitir correção/dispensa eficiente, controle global do sistema — ponte entre pesquisa de automação e prática.
- **4.3 Padrões de controle (Quadro 4) por momento**: Antes (pré-visualização, pontos de aprovação, permissões por tipo → P1,P3,P5); Durante (botão de parada, geração direcionável, representações compartilhadas editáveis → P1,P2,P5); Depois (desfazer, sandbox, registro legível, marcação de proveniência → P4,P5,P7); Contra dependência (forçamento cognitivo, comunicar incerteza/capacidades → P2,P6). Destaque: representações compartilhadas — mesmo objeto intermediário editável, não alternância pedir/receber.
- **4.4 Instrumentos de medição**: implícitas vs escalas de autorrelato (senso); comportamentais (taxa aceitação, edição, reversões, interrupções, tempo até intervir); medidas de dependência (concordância quando sistema acerta vs erra — distingue confiança apropriada de aceitação automática).
- **4.5 Governança**: supervisão efetiva para alto risco, direito à revisão (LGPD), certificação de nível máximo de autonomia — dependem de definições operacionais ainda faltantes.

## 5. O que ainda não está resolvido (§5)

**5.1 Limitações atuais (6–8 itens)**:
- Fragmentação conceitual (agência da IA vs humana vs senso tratados como mesma coisa → estudos não somam);
- Níveis estáticos para relação dinâmica (taxonomias descrevem configuração, explicam pouco transições de controle);
- Percebida ≠ efetiva (sentir-se no controle ≠ estar; falta modelo que relacione);
- Medidas herdadas de tarefas curtas/motoras (ms) → validade incerta para tarefas cognitivas longas (ex. 1h de escrita);
- Estudos curtos/lab → efeitos de delegação/skill loss só em semanas/meses;
- Pressuposto díade pessoa-sistema → falta modelo para grupos/multiagentes;
- Não-determinismo (mesma solicitação gera saídas diferentes + updates frequentes) → replicabilidade;
- Baixa representatividade brasileira (normas culturais de autoridade/deferência; pouca evidência em brasileiros, baixa literacia, serviço público digitalizado).

**5.2 Lacunas (Quadro 5, 9 linhas)**: definição operacional consensual de agência compartilhada (teórica); modelo de transições (teórica); integração percebida/efetiva/responsabilidade (teórica); métricas para tarefas longas (metodológica); métodos que extraiam agência de logs (metodológica); protocolos para não-determinísticos (metodológica); avaliação empírica de padrões da indústria (design); modelos para grupos/multiagentes (teórica+design); estudos com populações/contextos brasileiros (sociocultural). Cada com “Por que importa”.

**5.3 Questões em aberto (7)**: Como definir/medir agência colaborativa? Qual autonomia adequada e quem decide (designer/usuário/org/reg)? Como projetar transições percebidas/compreendidas/aceitas sem quebrar fluxo? Como garantir supervisão significativa? Interface distribui responsabilidade proporcional ao controle (como avaliar)? Até que ponto preservar senso de agência é desejável se gera ilusão de controle? Como delegação crescente afeta competências/autonomia profissional ao longo do tempo?

**5.4 Síntese**: Sabemos descrever graus por etapas, princípios de alternância, medir parte do senso, que supervisão formal ≠ controle, e que diretrizes/padrões existem. Não sabemos definir agência compartilhada comum, explicar transições, medi-la em uso real longo, avaliar evidência dos padrões, nem descrever arranjos multiagente/grupo — exatamente o par teórico-metodológico do GC1.

**Referências (7)**: Amershi et al. CHI 2019; Bainbridge 1983; Haggard 2017; Heer 2019 (PNAS); Horvitz 1999; Parasuraman et al. 2000 (IEEE SMC-A); Shneiderman 2022 (OUP).

## Proveniência

- Informação deriva de SRC-0012; relacionamento com SRC-0011 (GC1) e SRC-0013 (slides); integrada em SUB-0007.
