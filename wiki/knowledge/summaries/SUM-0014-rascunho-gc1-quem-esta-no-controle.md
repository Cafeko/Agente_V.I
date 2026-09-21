---
id: SUM-0014
type: summary
source: SRC-0014
title: "Summary — Rascunho privado GC1: Quem está no controle?"
created: 2026-09-21
related_subjects:
  - SUB-0007
privacy: private
---

# O que esta fonte apresenta (SRC-0014) — rascunho privado

> Síntese redigida com palavras próprias a partir do rascunho privado SRC-0014 (20 p., Set. 2026). Sem reprodução literal; todos os exemplos são paráfrases. Conteúdo privado do grupo — arquivo em `private/` não versionado.

## 1. Enquadramento

- Retoma GC1 do GranDIHC-BR: IHC precisa revisar não só o que pesquisa, mas **como pensa e como pesquisa** a relação pessoa-tecnologia [SRC-0014:1.1]. Duas frentes: teórica (aplicar teorias de outras áreas, fenomenologia, criar/sintetizar modelos) e metodológica (novos métodos de coleta/análise, design e avaliação). Contribuição legítima inclui levar teoria existente a novo contexto.
- Justifica importância: repertório metodológico da IHC foi feito para sistemas **determinísticos e subordinados**; medir eficiência sem explicar quem fez o quê gera métrica precisa sobre fenômeno errado. Importância transversal aos demais GCs (ética, sociocultural, emergentes) [SRC-0014:1.2].
- Recorte: **agência compartilhada humano-IA** como ponto onde problema teórico e metodológico se encontram (definição inconsistente de agência/autonomia/controle/iniciativa; falta de métodos para observar distribuição de iniciativa/decisão/execução/responsabilidade em interações contínuas não determinísticas), com dimensões interdisciplinar e fenomenológica [SRC-0014:1.4]. Formulação adotada: “À medida que IA deixa de ser ferramenta passiva, modelos tradicionais são insuficientes; permanece aberta a definição/representação/medição da distribuição” (p.5).
- Pergunta central: “O que já sabemos sobre agência compartilhada em Interfaces Inteligentes e o que ainda precisamos investigar/desenvolver/repensar?”

## 2. Sete problemas (P1–P7 + síntese §2.1)

Paráfrase dos P1–P7 (pp.6–7) e tabela síntese p.7:
- **P1 Ambiguidade**: alternância constante em assistentes; difícil dizer quem definiu objetivo/escolheu/executou; agente com um pedido dispara cadeia invisível.
- **P2 Erosão do senso de agência**: experiência subjetiva de controle (Haggard; Moore); IA que antecipa/completa faz usuário não se sentir autor, com implicações para motivação/responsabilidade; preocupação amplia-se com IA percebida como superior.
- **P3 Supervisão nominal**: human-in-the-loop vira clique em “aprovar”; supervisão degrada quando IA acerta — “fora do circuito” (Endsley & Kiris) e ironia da automação (Bainbridge).
- **P4 Lacuna de responsabilidade**: tende a recair no humano próximo com pouco controle; zona de amortecimento moral (Elish) e lacuna de responsabilidade (Matthias); questão de design de compatibilidade controle–responsabilidade.
- **P5 Opacidade**: agentes que agem em cadeia em segundo plano sem registro compreensível ou ponto de parada.
- **P6 Dependência excessiva**: overreliance/viés de automação — aceitação sem avaliação; decisão transferida sem decisão explícita; explicações sozinhas não garantem avaliação crítica; forçamento cognitivo pode reduzir efeito (Buçinca; Vasconcelos).
- **P7 Autoria/propriedade**: dimensões psicológica, social e jurídica; modo de inserção da IA altera percepção de autoria.

Quadro p.7 detalha por problema quem é afetado, contextos típicos (assistentes de escrita/código, autocompletar, apoio clínico, crédito/justiça, automação de tarefas, diagnóstico/recrutamento, educação/indústria criativa), consequências para usuário e manifestação em sistema inteligente. Ponto transversal p.7–8: estudos do Norte Global com alta escolaridade; populações com menor letramento digital têm menos recursos para contestar e são menos estudadas.

## 3. Literatura por vertentes (§3, 11 subseções + Quadro 1 p.11)

Síntese das vertentes (pp.9–11):
- 3.1 Níveis de automação (Sheridan & Verplank 1978, Parasuraman et al. 2000) — autonomia não binária, distribuída por estágios (aquisição/análise/decisão/execução).
- 3.2 Iniciativa mista (Horvitz 1999) — princípios sob incerteza.
- 3.3 Senso de agência — ligação intencional (intentional binding), escalas Tapal et al., Coyle et al. em IHC, Legaspi et al. 2024, Glawe et al. 2025.
- 3.4 HCAI — Shneiderman (2020/2022) framework bidimensional alto controle + alta automação; Heer (2019) agência + automação e representações compartilhadas.
- 3.5 Decisão assistida — Gomez et al. 2024 (105 art., paradigmas simplistas, taxonomia 7 padrões); Bansal et al. 2021 (quando humano+IA supera partes).
- 3.6 Cocriação — Zhang et al. 2025 (134 art., framework + catálogo).
- 3.7 Agentes autônomos — Feng et al. 2025 (5 níveis operador→observador, autonomia como decisão de design); Zhang & Varshney 2025.
- 3.8 Responsabilidade/controle significativo — Matthias (lacuna), Elish (zonas), Santoni de Sio & van den Hoven (controle significativo).
- 3.9 Sociotécnica/filosofia da ação — Hutchins (cognição distribuída), Latour (ator-rede), Suchman (ação situada), Bratman (agência compartilhada), Johnson et al. (coactive design), Klein et al. (automação como team player).
- 3.10 Engenharia Semiótica brasileira — De Souza 2005, estendida por Barbosa & Prates 2022 à integração humano-computador (Mueller et al. 2020) — promissora para GC1 quando “interlocutor” inclui sistema gerativo.
- 3.11 Fora da academia — diretrizes (Amershi et al. 2019 18 diretrizes, Google People+AI), produtos (modos de aprovação, plano, parada), regulação (AI Act art.14, LGPD art.20, PL 2338/2023), governança (certificados de autonomia).

Quadro 1 (p.11) organiza 10 vertentes por pergunta central, contribuição principal e refs-chave.

## 4. O que já foi desenvolvido (§4, 4 tipos, pp.12–13)

- 4.1 Modelos de distribuição: HITL, HOTL, human-out-of-the-loop, autonomia ajustável, iniciativa mista, níveis por papel do usuário — descritos com adequação (ex. HITL para alto risco/baixo volume).
- 4.2 Padrões (Quadro 2 p.12, 11 linhas): pré-visualização de plano (P1,P5), checkpoints (P3,P4,P5), desfazer/sandbox (P5), registro legível (P1,P4,P5), botão de parada (P3,P5), controles granulares (P1,P3), forçamento cognitivo (P2,P6), geração direcionável (P2,P7), representações compartilhadas (P1,P2), marcação de proveniência (P4,P7), comunicação de incerteza/capacidade (P3,P6).
- 4.3 Instrumentos: implícitas (ligação intencional), escalas (Tapal), comportamentais (aceitação/edição/reversão/tempo), medidas de dependência (acerto vs erro), taxonomias como instrumento analítico.
- 4.4 Governança/regulação: AI Act supervisão efetiva, LGPD revisão, certificados de autonomia, índices de controle/segurança.

## 5. O que ainda não está resolvido (§5, pp.14–16)

- **L1–L9 limitações (pp.14–15)**: L1 fragmentação conceitual; L2 níveis estáticos vs dinâmica (transições pouco explicadas); L3 percebida vs efetiva; L4 medidas de tarefas simples (intentional binding); L5 supervisão como “carimbo”; L6 estudos curtos/lab; L7 díade pessoa-sistema; L8 não determinismo/reprodutibilidade; L9 baixa representatividade do Sul Global.
- **Lacunas (Quadro p.15, 10 linhas)**: definição operacional de agência compartilhada; modelo de transições; integração percebida/efetiva/responsabilidade; métricas para tarefas longas; métodos via logs; protocolos com versionamento; estudos longitudinais; avaliação empírica de padrões; modelos para grupos/multiagentes; estudos brasileiros — com tipo (teórica/metodológica/design/sociocultural) e “por que importa”.
- **Q1–Q9 questões em aberto (pp.15–16)**: Q1 definir/medir agência colaborativa; Q2 nível adequado de autonomia e quem decide; Q3 projetar transições percebidas; Q4 supervisão significativa; Q5 proporcionalidade controle–responsabilidade; Q6 quando preservar senso gera ilusão; Q7 efeitos da delegação sobre competências/identidade; Q8 combinar teorias sociotécnicas/fenomenologia/Eng. Semiótica; Q9 fatores culturais/socioeconômicos brasileiros.
- **Proposta analítica (§6 p.17)**: modelo operacional “Agência compartilhada = definição do objetivo + iniciativa + decisão + execução + supervisão + capacidade de intervenção + responsabilidade”, com matriz 8 dimensões (objetivo, iniciativa, decisão, execução, supervisão, intervenção, responsabilidade, experiência transversal) — cada com pergunta-guia, indicadores observáveis e métodos (análise de prompts, logs, diffs, proveniência, ocular, think-aloud, experimentos com falhas, vinhetas, escalas, fenomenológicas, diários). Sugere desenho longitudinal de métodos mistos para atacar L3/L4/L6; valor é vocabulário comum, não teoria acabada (p.17).
- **Considerações finais (§7 p.18)**: o que já sabemos (autonomia graduável, não oposição controle-automação, senso mensurável, supervisão degrada, taxonomias/padrões existem) vs o que falta (definição, modelos de transição, métricas longas, métodos para não determinístico, avaliação empírica, grupos/multiagentes, contextos brasileiros). Confirma pertinência do GC1 e contribuição brasileira via Eng. Semiótica e contextos socioculturais pouco representados.

## Proveniência

- Conteúdo derivado de SRC-0014 (rascunho privado, 20 p., Set. 2026), sem reprodução literal, relacionado a SRC-0011/0012/0013 e integrado apenas de forma controlada em SUB-0007 (sem expor detalhes privados além do necessário). Arquivo em `private/` ignorado pelo Git.
