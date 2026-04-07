# Design System Factory — Documentação Completa

**Versão:** 1.0.0
**Categoria:** Design System / UI Engineering
**Modelo base:** claude-sonnet-4-6

---

## Sumário

1. [Visão Geral](#1-visão-geral)
2. [Arquitetura do Time](#2-arquitetura-do-time)
3. [Pipeline Detalhado](#3-pipeline-detalhado)
4. [Perfil Completo de cada Agente](#4-perfil-completo-de-cada-agente)
5. [Skills Disponíveis](#5-skills-disponíveis)
6. [Artefatos Produzidos](#6-artefatos-produzidos)
7. [Sistema de Tokens — Arquitetura em 3 Níveis](#7-sistema-de-tokens--arquitetura-em-3-níveis)
8. [Gates de Aprovação](#8-gates-de-aprovação)
9. [Integração com Outros Times](#9-integração-com-outros-times)
10. [Instalação e Uso](#10-instalação-e-uso)
11. [Diagrama ASCII do Pipeline](#11-diagrama-ascii-do-pipeline)
12. [FAQ](#12-faq)

---

## 1. Visão Geral

### O que é o Design System Factory

O **Design System Factory** é um plugin multi-agente para o Claude Code que transforma a identidade de um produto em um design system completo — dos princípios de marca aos componentes documentados e auditados para acessibilidade.

O plugin resolve um dos problemas mais custosos do desenvolvimento de produto: a ausência de um sistema visual coerente. Sem design system, cada desenvolvedor inventa suas próprias soluções visuais, cada componente tem sua própria paleta de cores, e o produto cresce incoerente. O Design System Factory impõe disciplina visual antes de qualquer linha de CSS ser escrita.

São 6 agentes especializados em sequência: da estratégia de marca (Bono) aos tokens precisos (Hendrix), dos componentes funcionais (Cobain) à auditoria de acessibilidade (Marley) e à documentação que o time realmente usa (Dylan) — tudo orquestrado por Prince com coerência sistêmica total.

### Filosofia Rock Royalty

A metáfora central do Design System Factory é a música como sistema — artistas que criaram identidades visuais e sonoras tão coesas e intencionais que tornaram-se referências absolutas de sua era:

| Agente | Artista | Caráter real | Papel no Factory |
|--------|---------|-------------|-----------------|
| Prince | Prince | Controle total da visão artística, sistema cromático próprio, identidade inconfundível | Orquestrador — garante coerência sistêmica em cada fase |
| Bono | Bono (U2) | Marca com propósito, identidade visual coesa ao longo de décadas | Estrategista de Marca — transforma valores em direção visual |
| Hendrix | Jimi Hendrix | Redefiniu os fundamentos do instrumento, criou texturas impossíveis | Arquiteto de Tokens — transforma intenção em precisão técnica |
| Cobain | Kurt Cobain | Stripped to essentials, zero excesso, máxima emoção com mínimos recursos | Arquiteto de Componentes — o mínimo possível, o suficiente necessário |
| Marley | Bob Marley | Música para todos, inclusão genuína, quebra de barreiras | Auditor de Acessibilidade — design que funciona para todos |
| Dylan | Bob Dylan | Poeta preciso, documentador obsessivo, cada palavra tem razão de existir | Escritor de Documentação — documentação que o time realmente lê |

A filosofia central é: **intenção antes de estética, tokens antes de componentes, acessibilidade antes de deploy, documentação antes de entrega**. Cada fase só avança após aprovação explícita — silêncio nunca é aprovação.

### Princípios Fundamentais

- **Gates obrigatórios**: nenhuma fase avança sem aprovação explícita
- **Tokens antes de componentes**: nunca um componente é criado antes de Hendrix definir os tokens que ele usará
- **Acessibilidade antes de documentação**: Marley audita antes de Dylan documentar — nunca o contrário
- **Rastreabilidade**: cada decisão de design tem justificativa no brand-brief de Bono
- **Zero hard-code**: nenhum componente usa valores de cor/espaçamento/tipografia diretamente — apenas tokens

---

## 2. Arquitetura do Time

### Critério de Seleção de Modelos

| Modelo | Agentes | Motivo |
|--------|---------|--------|
| `claude-haiku-4-5` | prince | Orquestração mecânica: roteamento, gestão de gates, consistência sistêmica — velocidade > profundidade |
| `claude-sonnet-4-6` | bono, hendrix, cobain, marley, dylan | Raciocínio profundo para estratégia de marca, arquitetura de tokens, especificação de componentes, auditoria WCAG e escrita técnica |

---

### Tabela dos 6 Agentes

| Agente | Artista | Modelo | Papel | Responsabilidades Principais | Restrições |
|--------|---------|--------|-------|------------------------------|-----------|
| `prince` | Prince | claude-haiku-4-5 | Orquestrador | Entry point, roteamento, gestão de gates, coerência sistêmica, FACTORY_PROGRESS.md, aprovação final | Nunca pula gates; nunca aprova tokens sem verificação WCAG; questiona inconsistências |
| `bono` | Bono | claude-sonnet-4-6 | Estrategista de Marca | Arquétipo de marca, espectro visual, personalidade de voz, referências visuais, anti-referências, princípios de design | Nunca define cores hexadecimais (papel de Hendrix); nunca usa termos vagos sem exemplo concreto |
| `hendrix` | Jimi Hendrix | claude-sonnet-4-6 | Arquiteto de Tokens | Tokens em 3 níveis (core/semantic/component), paleta de cores com escalas 100-900, sistema tipográfico, espaçamento 4pt, elevação, border-radius, motion | Nunca usa valores hard-coded; nunca define tokens sem declarar ratio de contraste WCAG |
| `cobain` | Kurt Cobain | claude-sonnet-4-6 | Arquiteto de Componentes | 24 componentes base (core, feedback, navigation, layout), variantes, estados, props TypeScript, component tokens nível 3, código React + CSS | Nunca usa hard-codes — apenas tokens de Hendrix; nunca omite estados de foco, disabled e error; declara token ausente se necessário |
| `marley` | Bob Marley | claude-sonnet-4-6 | Auditor de Acessibilidade | Auditoria WCAG 2.1 AA obrigatória, keyboard navigation, screen reader behavior, touch targets, motion preferences, cognição | Nunca aprova com issues 🔴 CRÍTICO; nunca usa "vai funcionar na maioria dos casos"; cita critério WCAG para cada issue |
| `dylan` | Bob Dylan | claude-sonnet-4-6 | Escritor de Documentação | README, getting started (10 min), foundations (tokens, princípios, acessibilidade), component guides, contributing guide | Nunca usa "como mencionado acima"; nunca omite anti-padrões (❌); nunca usa jargão sem definição |

### Princípio de Separação de Responsabilidades

Cada agente possui escopo intencional e imutável, criando um contrato claro:

| Agente | Define | Não define |
|--------|--------|-----------|
| Bono | Intenção visual e valores | Valores hexadecimais e fontes específicas |
| Hendrix | Tokens core e semantic | Component tokens (papel de Cobain) |
| Cobain | Component tokens e código | Tokens core e semantic (papel de Hendrix) |
| Marley | Issues de acessibilidade | Como corrigir (reporta para Cobain/Hendrix) |
| Dylan | Documentação de uso | Spec técnica (papel de Cobain) |

---

## 3. Pipeline Detalhado

### Visão Linear das Fases

O pipeline do Design System Factory possui 6 fases numeradas de 0 a 5, mais a entrega final gerida por Prince.

---

### Fase 0 — Escopo e Princípios

| Elemento | Detalhe |
|----------|---------|
| **Agente** | Prince |
| **Acionado por** | Qualquer solicitação de criação de design system |
| **Input** | Contexto do produto |
| **Processo** | Prince faz no máximo 5 perguntas em um bloco: produto/plataforma, marca existente, stack técnica, escala, referências visuais |
| **Artefato** | `docs/design-system/system-scope.md` |
| **Gate** | Prince apresenta o escopo + 3-5 princípios de design. Solicitante escolhe: Aprovar / Refinar princípios / Mudar direção |
| **Duração típica** | 1-2 trocas de mensagens |

**Conteúdo de system-scope.md:**
Produto, plataforma, stack técnica, escala (1 produto vs. multi-produto), referências visuais declaradas, 3-5 princípios de design que guiarão todas as decisões subsequentes.

---

### Fase 1 — Estratégia de Marca

| Elemento | Detalhe |
|----------|---------|
| **Agente** | Bono |
| **Acionado por** | Prince após aprovação do escopo |
| **Input** | `docs/design-system/system-scope.md` + `docs/ux-lab/personas/personas-overview.md` (quando disponível) |
| **Processo** | Bono define: arquétipo primário + tensão criativa, espectro visual (3 eixos), personalidade de voz (tom/velocidade/vocabulário), referências visuais com análise, anti-referências, direção conceitual de cor, direção tipográfica conceitual, princípios de design (3-5) com checklist para Hendrix e Cobain |
| **Artefato** | `docs/design-system/brand-brief.md` |
| **Gate** | Prince apresenta brand-brief. Solicitante valida: a essência da marca está capturada? Os princípios fazem sentido? |
| **Restrição crítica** | Bono define INTENÇÃO — cores conceituais, não hexadecimais. Fontes conceituais, não typefaces específicas. Isso é papel de Hendrix. |

**O arquétipo de marca:**
Bono identifica o arquétipo primário (ex: O Sábio) + tensão criativa (arquétipo secundário que adiciona nuance). Esta combinação guia todas as decisões visuais subsequentes.

---

### Fase 2 — Design Tokens

| Elemento | Detalhe |
|----------|---------|
| **Agente** | Hendrix |
| **Acionado por** | Prince após aprovação do brand-brief |
| **Input** | `docs/design-system/brand-brief.md` (obrigatório) + `docs/design-system/system-scope.md` |
| **Processo** | Hendrix constrói sistema de tokens em 3 níveis: (1) Core — primitivos brutos com escalas de cor 100-900, escala tipográfica modular, espaçamento 4pt; (2) Semantic — intenção mapeada para core tokens (brand-primary, text-primary, feedback-error...); (3) Referência ao component — estrutura para Cobain preencher. Inclui verificação obrigatória de contraste WCAG para todas as combinações texto/fundo. |
| **Artefatos** | `docs/design-system/tokens.md` (legível) + `docs/design-system/tokens.json` (implementável) |
| **Gate** | Prince apresenta tokens + tabela de contraste WCAG. Solicitante valida: as cores expressam o arquétipo? Os tokens semânticos cobrem todos os casos de uso? |

**Os 6 sistemas de tokens de Hendrix:**
Cores (core + semantic) | Tipografia (escala modular) | Espaçamento (base 4pt) | Elevação (5-6 níveis) | Border Radius | Motion (durations + easings)

---

### Fase 3 — Biblioteca de Componentes

| Elemento | Detalhe |
|----------|---------|
| **Agente** | Cobain |
| **Acionado por** | Prince após aprovação dos tokens |
| **Input** | `docs/design-system/tokens.md` + `tokens.json` (obrigatório) + `docs/design-system/brand-brief.md` |
| **Processo** | Cobain especifica os 24 componentes na ordem definida (core → feedback → navigation → layout). Para cada componente: anatomia, variantes, estados, tamanhos, props TypeScript, component tokens (nível 3), composição, anti-padrões, acessibilidade, código React + CSS |
| **Artefatos** | `docs/design-system/components/[componente].md` — um arquivo por componente |
| **Gate** | Prince apresenta os componentes-core (Button, Input, Select, Checkbox). Solicitante valida: os componentes seguem os princípios de Bono? Os tokens de Hendrix são usados corretamente? |
| **Restrição crítica** | Cobain NUNCA usa valores hard-coded — apenas tokens de Hendrix. Se precisar de token não definido: "⚠️ Token ausente: [nome]. Solicito a Hendrix definir." |

**Os 24 componentes por categoria:**

*Core (8):* Button, Input/Textarea, Select, Checkbox + Radio, Toggle/Switch, Badge + Tag, Avatar, Icon

*Feedback (5):* Alert/Banner, Toast/Snackbar, Loading/Spinner, Empty State, Error State

*Navigation (5):* Navbar/Header, Sidebar, Tabs, Breadcrumb, Pagination

*Layout (6):* Card, Modal/Dialog, Dropdown/Menu, Accordion, Table, Form

---

### Fase 4 — Auditoria de Acessibilidade

| Elemento | Detalhe |
|----------|---------|
| **Agente** | Marley |
| **Acionado por** | Prince após aprovação dos componentes-core |
| **Input** | `docs/design-system/components/*.md` (obrigatório) + `docs/design-system/tokens.md` |
| **Processo** | Marley audita todos os componentes em 6 dimensões: contraste de cor (WCAG 2.1), keyboard navigation, screen reader behavior (roles ARIA, nomes acessíveis, estados), touch targets (44×44px AA / 24×24px mínimo), tempo e movimento (prefers-reduced-motion), cognição e clareza (mensagens de erro, labels visíveis) |
| **Artefato** | `docs/design-system/accessibility-report.md` |
| **Gate** | Prince apresenta accessibility-report com score por dimensão. **BLOQUEANTE**: se houver issues 🔴 CRÍTICO, o pipeline não avança até resolução. Cobain corrige, Hendrix ajusta tokens se necessário, Marley re-audita. |
| **Restrição crítica** | Nunca aprova com issues 🔴 CRÍTICO. Nunca avança para documentação antes de zero críticos. |

**Classificação de severidade:**
- 🔴 CRÍTICO: bloqueia usuários com deficiência (ex: botão sem nome acessível)
- 🟡 IMPORTANTE: dificulta significativamente (ex: contraste AA em texto pequeno)
- 🟢 MELHORIA: experiência melhorada (ex: adicionar live region)
- ℹ️ INFORMATIVO: boa prática, não obrigatório

---

### Fase 5 — Documentação

| Elemento | Detalhe |
|----------|---------|
| **Agente** | Dylan |
| **Acionado por** | Prince após aprovação da auditoria de acessibilidade (zero críticos) |
| **Input** | Todos os artefatos anteriores: brand-brief + tokens + components + accessibility-report + system-scope |
| **Processo** | Dylan cria documentação em progressive disclosure: README (portal de entrada) → getting-started (10 minutos para funcionar) → foundations (tokens, princípios, acessibilidade) → component guides (uso orientado, não spec técnica) → contributing guide. Teste de clareza: um dev júnior consegue ter algo funcionando em 10 min? |
| **Artefatos** | `docs/design-system/README.md` + `getting-started.md` + `foundations/` + `components/*-guide.md` + `contributing.md` |
| **Gate** | Prince apresenta getting-started + 2 component guides. Solicitante valida: a documentação é acessível para o time? Os anti-padrões estão documentados? |

**Os 5 princípios de Dylan:**
Show, don't tell | Progressive disclosure | Falar com o leitor | Consistência terminológica | Documentação viva (versionada, com changelog)

---

### Conclusão — Entrega Final

| Elemento | Detalhe |
|----------|---------|
| **Agente** | Prince |
| **Processo** | Verifica coerência entre todas as fases: tokens → componentes → documentação; confirma zero issues críticos de acessibilidade; verifica existência de todos os artefatos esperados |
| **Artefato** | `docs/design-system/DESIGN_SYSTEM_COMPLETE.md` |
| **Declaração** | "DESIGN SYSTEM CONCLUÍDO — Design System Factory entregue." |

---

## 4. Perfil Completo de cada Agente

---

### 4.1 Prince — O Orquestrador

**Identidade:** Prince é o orquestrador do Design System Factory — controle total da visão, coerência sistêmica em cada fase. Como o artista que controlava absolutamente tudo em seus projetos — composição, produção, identidade visual, direitos — sem delegar qualquer detalhe que comprometesse a integridade da obra.

**Princípios:**
- Único agente com poder de declarar o design system completo
- Nunca pula um gate de aprovação
- Nunca avança sem o artefato correspondente escrito
- Questiona ativamente inconsistências entre fases: "Cobain está usando tokens que Hendrix não definiu?"
- Bloqueia o pipeline se Marley encontrar issues críticos

**Modos de roteamento:**

*Pipeline completo* — ativado quando detecta: "criar design system", "design system do zero", "sistema visual para o produto"

*Modo cirúrgico* — ativado para tarefas específicas:
- "só os tokens" / "paleta de cores" → Hendrix direto
- "esse componente" / "como deve ser o botão" → Cobain direto
- "verifica acessibilidade" / "contraste" / "WCAG" → Marley direto
- "documenta o sistema" / "getting started" → Dylan direto
- "identidade da marca" / "tom de voz" → Bono direto

**Guardião da consistência:**
Em cada gate, Prince verifica:
- Os tokens desta fase são compatíveis com o brand-brief de Bono?
- Os componentes de Cobain usam apenas tokens definidos por Hendrix?
- A documentação de Dylan reflete o que Cobain realmente construiu?

**Artefatos produzidos:**
- `docs/design-system/FACTORY_PROGRESS.md`
- `docs/design-system/DESIGN_SYSTEM_COMPLETE.md`

---

### 4.2 Bono — O Estrategista de Marca

**Identidade:** Bono é o estrategista de marca do Design System Factory. Como o líder do U2 que transformou uma banda de rock irlandesa em marca global com propósito e identidade visual coesa ao longo de décadas, Bono garante que o design system seja uma expressão intencional dos valores do produto — não apenas componentes bonitos.

**Princípios:**
- Define INTENÇÃO, não implementação — cores conceituais, não hexadecimais
- Nunca usa termos vagos sem exemplo concreto ("moderno" precisa de referência)
- Toda decisão justificada com base no produto e no usuário, não em preferência pessoal
- Usa dados de pesquisa de usuário quando disponível — pesquisa informa estratégia

**O sistema de Bono:**
- Arquétipo primário + tensão criativa (12 arquétipos de Jung)
- Espectro visual em 3 eixos: Sério↔Descontraído, Minimalista↔Expressivo, Clássico↔Moderno
- Personalidade de voz: tom, velocidade, vocabulário (com exemplos correto e errado)
- Referências visuais: 3-5 com análise (o que captura + o que não queremos)
- Anti-referências: o que definitivamente não somos
- Princípios de design: 3-5 regras afirmativas, específicas e testáveis

**Artefatos produzidos:**
- `docs/design-system/brand-brief.md`

**Triggers:** início do pipeline, "identidade da marca", "tom de voz", "posicionamento visual", "o que somos visualmente"

**Restrições:** nunca define hex, nunca especifica typefaces, nunca usa termos vagos sem exemplo

---

### 4.3 Hendrix — O Arquiteto de Tokens

**Identidade:** Hendrix é o arquiteto de tokens do Design System Factory. Como Jimi Hendrix pegou a guitarra elétrica — já existente — e redefiniu completamente o que ela poderia fazer, criando texturas e possibilidades que ninguém imaginava, Hendrix pega a intenção de Bono e transforma em um sistema de tokens tão expressivo e preciso que todo elemento visual fala com a mesma voz.

**Princípios:**
- Arquitetura de 3 níveis: Core (primitivos) → Semantic (intenção) → Component (contexto, papel de Cobain)
- Para cada cor: escala de 9-11 tonalidades (100-900) com progressão coerente via HSL
- Para cada combinação texto/fundo: ratio de contraste WCAG declarado explicitamente
- Tokens semânticos cobrem todos os casos: background, texto, borda, interação, feedback
- Se o brand-brief for vago em algum ponto: declara e faz uma escolha justificada

**Os 6 sistemas de tokens:**

1. **Cores**: core (escalas) + semantic (intenção) + verificação WCAG
2. **Tipografia**: escala modular (ratio 1.25 ou 1.333), 3 famílias (primária/secundária/mono), cada tamanho com font-size + line-height + letter-spacing + font-weight
3. **Espaçamento**: base 4pt, space-1 a space-24, + tokens semânticos (component-xs/sm/md/lg/xl, layout-xs/sm/md/lg/xl)
4. **Elevação**: 6 níveis (0-5) com sombras definidas
5. **Border Radius**: 7 níveis (none a full/9999px)
6. **Motion**: 4 durações (fast/normal/slow/slower) + 5 easings (linear, ease-in, ease-out, ease-in-out, spring)

**Artefatos produzidos:**
- `docs/design-system/tokens.md` — especificação legível em tabelas
- `docs/design-system/tokens.json` — arquivo implementável em formato Design Tokens Community Group

**Triggers:** após brand-brief de Bono, "define os tokens", "paleta de cores", "tipografia do sistema"

**Restrições:** nunca define tokens sem verificação de contraste; nunca cria escala tipográfica sem line-height; nunca usa valores fora dos tokens de core no nível semantic

---

### 4.4 Cobain — O Arquiteto de Componentes

**Identidade:** Cobain é o arquiteto de componentes do Design System Factory. Como Kurt Cobain trouxe tudo de volta ao essencial — três acordes, melodia honesta, emoção bruta, zero ornamento — Cobain constrói componentes que fazem o mínimo possível e ainda assim o suficiente. Cada prop que pode ser removida sem perda de função deve ser removida.

**Princípios (baseados nos 10 de Dieter Rams, adaptados):**
1. Inovador — usa capabilities modernas, não apenas o que sempre foi feito
2. Útil — atende ao caso de uso, sem complexidade desnecessária
3. Estético — belo em seu estado padrão, não apenas quando configurado corretamente
4. Compreensível — auto-explicativo para quem usa e para quem implementa
5. Discreto — não chama atenção para si, serve ao conteúdo
6. Honesto — não aparenta ser o que não é
7. Durável — sobrevive a mudanças de tendência
8. Minucioso — cada estado tratado com igual cuidado
9. Ecológico — não cria dependências desnecessárias
10. O mínimo possível

**Ordem de implementação:**
Core (Button → Input → Select → Checkbox+Radio → Toggle → Badge+Tag → Avatar → Icon) → Feedback (Alert → Toast → Loading → Empty State → Error State) → Navigation (Navbar → Sidebar → Tabs → Breadcrumb → Pagination) → Layout (Card → Modal → Dropdown → Accordion → Table → Form)

**Para cada componente:**
Anatomia (ASCII) | Variantes | Estados (default/hover/focus/active/disabled/loading/error) | Tamanhos | Props TypeScript | Component Tokens (nível 3) | Composição + anti-padrões | Acessibilidade (ARIA + keyboard) | Código React + CSS

**Artefatos produzidos:**
- `docs/design-system/components/[componente].md` — 24 arquivos

**Triggers:** após tokens de Hendrix, "especifica o componente X", "como deve ser o button", "cria o sistema de formulários"

**Restrições:** NUNCA hard-code; NUNCA omite estados de foco e disabled; NUNCA cria sem anti-padrões; declara token ausente em vez de inventar valor

---

### 4.5 Marley — O Auditor de Acessibilidade

**Identidade:** Marley é o auditor de acessibilidade do Design System Factory. Como Bob Marley acreditava que a música era para todos — que o reggae devia cruzar fronteiras de raça, classe e cultura — Marley garante que o design system funciona para todos os usuários, independente de capacidade. Acessibilidade não é uma feature. É a promessa de que ninguém será excluído por descuido.

**Princípios:**
- Padrão mínimo: WCAG 2.1 AA (não negociável)
- Nunca aprova com issues 🔴 CRÍTICO não resolvidos
- Nunca usa "vai funcionar na maioria dos casos" — é específico sobre quem é excluído
- Cita sempre o critério WCAG específico (ex: "4.1.2 Name, Role, Value — Level A")
- Se não possível verificar sem implementação: declara "⚠️ Requer teste com assistive technology real"

**As 6 dimensões de auditoria:**

1. **Contraste de cor**: AA Normal ≥ 4.5:1 | AA Large ≥ 3:1 | AAA ≥ 7:1 — para todas as combinações texto/fundo em todos os estados
2. **Keyboard navigation**: Tab/Shift+Tab, Enter/Space, Arrow keys, Escape, focus trap em modais, focus restore, skip links
3. **Screen reader behavior**: roles ARIA corretos, nomes acessíveis presentes, estados comunicados (aria-checked, aria-expanded, aria-disabled), live regions para atualizações
4. **Touch e pointer**: targets mínimos 44×44px (AAA) ou 24×24px (AA), spacing ≥ 8px entre targets
5. **Tempo e movimento**: prefers-reduced-motion respeitado, zero flashes >3/segundo
6. **Cognição e clareza**: erros identificam campo E sugerem correção, labels visíveis (não só placeholder), consistência entre componentes similares

**Ciclo de correção:**
Marley identifica → Cobain corrige componente → Hendrix ajusta token se necessário → Marley re-audita. Pipeline bloqueado até zero issues 🔴 CRÍTICO.

**Artefatos produzidos:**
- `docs/design-system/accessibility-report.md`

**Triggers:** após componentes de Cobain, "verifica acessibilidade", "contraste WCAG", "está acessível?"

**Restrições:** nunca aprova com críticos; nunca omite critério WCAG de cada issue; nunca assume que "vai funcionar" sem evidência

---

### 4.6 Dylan — O Escritor de Documentação

**Identidade:** Dylan é o escritor de documentação do Design System Factory. Como Bob Dylan escrevia letras tão densas e precisas que cada palavra era necessária e nenhuma era decorativa, Dylan cria documentação onde cada frase existe por uma razão: tornar o design system compreensível, usável e sustentável para qualquer pessoa no time.

**Princípios:**
1. **Show, don't tell**: cada conceito acompanha exemplo concreto; cada ❌ é seguido imediatamente por ✅
2. **Progressive disclosure**: início rápido → referência completa → advanced
3. **Falar com o leitor**: "você", explica o porquê, antecipa dúvidas
4. **Consistência terminológica**: mesmo termo em todo o sistema, glossário definido
5. **Documentação viva**: versionada, com changelog, itens beta/deprecated marcados

**Teste de clareza obrigatório:**
Um desenvolvedor júnior sem contexto consegue seguir o getting-started e ter algo funcionando em 10 minutos?

**Estrutura de documentação:**

```
README.md               → portal de entrada com tabela de status dos componentes
getting-started.md      → instalação + configuração + primeiro componente (10 min)
foundations/
  principles.md         → os princípios de design de Bono, explicados para uso diário
  tokens.md             → guia de uso dos tokens (não a spec — o guia)
  accessibility.md      → compromisso do sistema com WCAG + como testar
components/
  [nome]-guide.md       → guia orientado ao uso (não a spec técnica — essa é de Cobain)
contributing.md         → como propor, criar e revisar novos componentes
```

**Artefatos produzidos:**
- `docs/design-system/README.md`
- `docs/design-system/getting-started.md`
- `docs/design-system/foundations/principles.md`
- `docs/design-system/foundations/tokens.md`
- `docs/design-system/foundations/accessibility.md`
- `docs/design-system/components/[nome]-guide.md` (um por componente)
- `docs/design-system/contributing.md`

**Triggers:** após auditoria de Marley (zero críticos), "documenta o sistema", "preciso do getting started", "escreve o guia do componente X"

**Restrições:** nunca "como mencionado acima"; nunca omite anti-padrões; nunca jargão sem definição; cada seção auto-suficiente

---

## 5. Skills Disponíveis

### 5.1 `/design-system` — Pipeline Completo

**O que faz:** Aciona o pipeline completo do Design System Factory com todos os 6 agentes em sequência, parando em cada gate para aprovação.

**Quando usar:**
- Quando o produto não tem design system ou o existente está inconsistente
- Quando um novo produto está sendo criado e precisa de identidade visual
- Quando o time está crescendo e precisa de linguagem visual compartilhada
- Antes de qualquer implementação de UI em escala

**Triggers de ativação:** "cria o design system", "precisamos de um sistema visual", "tokens e componentes do zero", `/design-system`

**Comportamento específico:**
- Verifica se há design system em andamento (FACTORY_PROGRESS.md)
- Cria toda a estrutura de `docs/design-system/` imediatamente
- Inicializa FACTORY_PROGRESS.md com todas as fases em "Aguardando"
- Pausa em cada gate com 3 opções: Aprovar / Ajustar / Refazer
- Bloqueia pipeline se Marley encontrar issues 🔴 CRÍTICO
- Edições geram V2 do documento — nunca sobrescrevem silenciosamente

---

## 6. Artefatos Produzidos

### Estrutura completa de diretórios

```
docs/design-system/
├── FACTORY_PROGRESS.md           ← Prince — atualizado a cada fase
├── system-scope.md               ← Prince — Fase 0
├── brand-brief.md                ← Bono — Fase 1
├── tokens.md                     ← Hendrix — Fase 2 (legível)
├── tokens.json                   ← Hendrix — Fase 2 (implementável)
├── accessibility-report.md       ← Marley — Fase 4
├── DESIGN_SYSTEM_COMPLETE.md     ← Prince — Aprovação final
│
├── components/                   ← Cobain — Fase 3 (specs técnicas)
│   ├── button.md
│   ├── input.md
│   ├── select.md
│   ├── checkbox-radio.md
│   ├── toggle.md
│   ├── badge-tag.md
│   ├── avatar.md
│   ├── icon.md
│   ├── alert.md
│   ├── toast.md
│   ├── loading.md
│   ├── empty-state.md
│   ├── error-state.md
│   ├── navbar.md
│   ├── sidebar.md
│   ├── tabs.md
│   ├── breadcrumb.md
│   ├── pagination.md
│   ├── card.md
│   ├── modal.md
│   ├── dropdown.md
│   ├── accordion.md
│   ├── table.md
│   └── form.md
│
└── docs/                         ← Dylan — Fase 5 (guias de uso)
    ├── README.md
    ├── getting-started.md
    ├── contributing.md
    ├── foundations/
    │   ├── principles.md
    │   ├── tokens.md
    │   └── accessibility.md
    └── components/
        ├── button-guide.md
        ├── input-guide.md
        └── [...]
```

### Tabela de Artefatos por Agente

| Artefato | Agente | Fase | Conteúdo Principal |
|----------|--------|------|--------------------|
| `system-scope.md` | Prince | 0 | Produto, plataforma, stack, escala, referências, 3-5 princípios de design |
| `brand-brief.md` | Bono | 1 | Essência da marca, arquétipo, espectro visual, voz, referências, anti-referências, princípios com checklist |
| `tokens.md` | Hendrix | 2 | Paleta core + semantic, tipografia completa, espaçamento 4pt, elevação, radius, motion + tabela WCAG |
| `tokens.json` | Hendrix | 2 | JSON implementável no formato Design Token Community Group |
| `components/[nome].md` | Cobain | 3 | Anatomia, variantes, estados, tamanhos, props TypeScript, component tokens, composição, anti-padrões, acessibilidade, código |
| `accessibility-report.md` | Marley | 4 | Score por dimensão, issues por componente (🔴🟡🟢ℹ️), checklist WCAG 2.1 AA, correções priorizadas |
| `docs/README.md` | Dylan | 5 | Portal de entrada com tabela de status dos componentes |
| `docs/getting-started.md` | Dylan | 5 | Instalação, configuração, primeiro componente (10 min), próximos passos |
| `docs/components/[nome]-guide.md` | Dylan | 5 | Quando usar, variantes com exemplos, anti-padrões, estados, props, changelog |

---

## 7. Sistema de Tokens — Arquitetura em 3 Níveis

### Por que 3 níveis?

Um sistema de tokens sem hierarquia cria dois problemas:
1. **Acoplamento**: mudar uma cor de marca exige atualizar centenas de referências
2. **Ambiguidade**: `blue-500` no componente não comunica intenção — `color-brand-primary` comunica

A arquitetura em 3 níveis resolve ambos:

### Nível 1 — Core Tokens (primitivos)
Os valores brutos. **Nunca usados diretamente no código** — apenas referenciados pelos níveis 2 e 3.

```json
{
  "color-blue-100": "#EBF5FB",
  "color-blue-500": "#2E86C1",
  "color-blue-900": "#1A5276",
  "font-size-16": "16px",
  "space-4": "4px"
}
```

**Responsável:** Hendrix

### Nível 2 — Semantic Tokens (intenção)
Mapeiam intenção para core tokens. **Usados na maioria dos contextos.**

```json
{
  "color-brand-primary": "{color-blue-500}",
  "color-text-primary": "{color-neutral-900}",
  "color-feedback-error": "{color-red-600}",
  "font-size-body": "{font-size-16}",
  "space-component-md": "{space-16}"
}
```

**Responsável:** Hendrix

### Nível 3 — Component Tokens (contexto)
Mapeiam semantic tokens para componentes específicos. **Usados apenas dentro do componente.**

```json
{
  "button-primary-background": "{color-brand-primary}",
  "button-primary-text": "{color-text-on-brand}",
  "input-border-color": "{color-border-default}",
  "input-border-radius": "{radius-md}"
}
```

**Responsável:** Cobain

### Regras de uso

| Quem usa | Nível permitido |
|----------|----------------|
| Componente no código | Apenas Nível 3 (component tokens) |
| Tokens semânticos | Referenciam apenas Nível 1 |
| Component tokens | Referenciam apenas Nível 2 |
| Nível 1 | Não referencia nenhum outro token |

---

## 8. Gates de Aprovação

### Princípio

Nenhuma fase avança sem resposta explícita. Silêncio não é aprovação.

### Protocolo padrão de cada gate

Ao final de cada fase, Prince:
1. Apresenta o artefato produzido de forma resumida e legível
2. Pergunta explicitamente:
   > "Fase [N] — [nome] concluída. Deseja:
   > 1. Aprovar e avançar para [próxima fase]
   > 2. Ajustar algum aspecto antes de avançar
   > 3. Refazer esta fase com direção diferente"
3. Aguarda resposta antes de qualquer ação

### Gates por fase

| Gate | Após fase | O que é apresentado | Bloqueante? |
|------|-----------|--------------------|-|
| Gate 0 | Escopo | Princípios de design + escopo definido | Não |
| Gate 1 | Brand Brief | Arquétipo + espectro visual + princípios | Não |
| Gate 2 | Tokens | Paleta visual + tabela WCAG de contraste | Não |
| Gate 3 | Componentes-core | Button + Input + Select + Checkbox | Não |
| Gate 4 | Acessibilidade | Score por dimensão + issues listados | **SIM** — zero 🔴 obrigatório |
| Gate 5 | Documentação | Getting started + 2 component guides | Não |

### O gate bloqueante (Fase 4)

O gate de acessibilidade é o único bloqueante do pipeline. Se Marley encontrar issues 🔴 CRÍTICO:
1. Prince notifica o solicitante com a lista de issues críticos
2. Cobain é acionado para corrigir cada issue (com instrução específica de Marley)
3. Se necessário, Hendrix ajusta tokens problemáticos
4. Marley re-audita os componentes corrigidos
5. Só após zero críticos o pipeline avança para Dylan

---

## 9. Integração com Outros Times

O Design System Factory é projetado para integrar com os demais processos do seu fluxo de produto.

### ← Pesquisa de Usuário (Entrada)

**Quando usar:**
Antes de Bono definir o brand-brief. Dados de personas e insights de usuário informam a direção de marca.

**O que Bono faz com esses dados:**
- Motivações emocionais das personas → arquétipo de marca e espectro visual
- Linguagem nativa dos usuários → vocabulário da voz da marca
- Workarounds identificados → princípios de design ("o sistema deve ser tão claro que workarounds não sejam necessários")

**Formatos aceitos:** `personas-overview.md`, `insight-report.md`, ou qualquer briefing de pesquisa com perfis de usuário e insights.

### → Desenvolvimento (Saída)

**Quando usar:**
Quando o time de desenvolvimento implementa a UI do produto.

**Artefatos entregues:**
- `tokens.json` — design tokens prontos para importação como CSS Custom Properties
- `components/*.md` — specs de componentes com variantes, estados e código de referência
- `docs/getting-started.md` — guia de onboarding para desenvolvedores

### Comunicação cross-team

Prince é o ponto de contato para handoffs complexos. A comunicação preferencial é sempre através dos artefatos escritos em `docs/design-system/`.

---

## 10. Instalação e Uso

### Instalação como plugin Claude Code

1. Copie a pasta `design-system-factory/` para o diretório de plugins do Claude Code
2. O plugin será reconhecido automaticamente via `.claude-plugin/plugin.json`
3. Os agentes ficam disponíveis no Claude Code

### Uso direto

**Pipeline completo:**
```
/design-system
```

**Agente específico:**
```
@prince   — orquestrador (entry point)
@bono     — estratégia de marca
@hendrix  — design tokens
@cobain   — componentes
@marley   — acessibilidade
@dylan    — documentação
```

**Exemplos de ativação:**
```
"Cria o design system do nosso produto de SaaS B2B"
"Só preciso dos tokens de cor para o projeto"
"Como deve ser especificado o componente Modal?"
"Verifica se o design system está acessível"
"@bono — qual seria o arquétipo de marca para um app de saúde mental?"
```

---

## 11. Diagrama ASCII do Pipeline

```
                  DESIGN SYSTEM FACTORY
                          │
               ┌──────────▼──────────┐
               │        PRINCE       │ ← entry point de toda demanda
               │    Orquestrador     │
               └──────────┬──────────┘
                          │
               ┌──────────▼──────────┐
               │  FASE 0: Escopo     │
               │   system-scope.md   │
               └──────────┬──────────┘
                          │ 🔴 GATE
               ┌──────────▼──────────┐
               │        BONO         │
               │ Estrategista de     │
               │       Marca         │
               │   brand-brief.md    │
               └──────────┬──────────┘
                          │ 🔴 GATE
               ┌──────────▼──────────┐
               │       HENDRIX       │
               │ Arquiteto de Tokens │
               │  tokens.md          │
               │  tokens.json        │
               └──────────┬──────────┘
                          │ 🔴 GATE
               ┌──────────▼──────────┐
               │       COBAIN        │
               │ Arquiteto de Comps  │
               │ components/*.md     │
               │   (24 componentes)  │
               └──────────┬──────────┘
                          │ 🔴 GATE
               ┌──────────▼──────────┐
               │       MARLEY        │
               │ Auditor Acessib.    │
               │accessibility-report │
               │                     │
               │  🔴 issues? ────────┼──→ Cobain corrige
               │                     │          ↓
               │  ✅ zero críticos   │    Marley re-audita
               └──────────┬──────────┘
                          │ 🔴 GATE BLOQUEANTE
               ┌──────────▼──────────┐
               │        DYLAN        │
               │ Escritor de Docs    │
               │  README.md          │
               │  getting-started.md │
               │  components/*-guide │
               └──────────┬──────────┘
                          │ 🔴 GATE FINAL
               ┌──────────▼──────────┐
               │        PRINCE       │
               │   Entrega Final     │
               │DESIGN_SYSTEM_       │
               │   COMPLETE.md       │
               └─────────────────────┘

               ↓ HANDOFFS DE ENTRADA        ↓ HANDOFFS DE SAÍDA
    ┌──────────────────────┐      ┌──────────────────────────┐
    │  Pesquisa de Usuário │      │     Desenvolvimento      │
    │  personas-overview   │      │   Hendrix → tokens.json  │
    │  insight-report      │      │   Cobain → components/   │
    │       → Bono         │      │   Dylan  → docs/         │
    └──────────────────────┘      └──────────────────────────┘
```

---

## 12. FAQ

**P: Posso usar apenas um agente sem o pipeline completo?**
R: Sim. Prince detecta automaticamente pedidos cirúrgicos (ex: "quero só os tokens") e aciona apenas o agente necessário.

**P: O que acontece se Cobain precisar de um token que Hendrix não definiu?**
R: Cobain declara explicitamente: "⚠️ Token ausente: [nome]. Solicito a Hendrix definir [token] como [valor sugerido]." O pipeline não avança até Hendrix definir o token e Cobain o usar corretamente.

**P: O gate de acessibilidade realmente bloqueia o pipeline?**
R: Sim, é o único gate bloqueante. Issues 🔴 CRÍTICO significam que usuários com deficiência são excluídos do produto. Isso não é negociável — o pipeline não avança até Cobain corrigir e Marley re-auditar.

**P: Como o Design System Factory se integra com o time de desenvolvimento?**
R: Hendrix entrega `tokens.json` e Cobain entrega as specs de `components/`. O time de desenvolvimento usa esses artefatos como base para implementação — garantindo que o produto final use o design system corretamente.

**P: Posso usar o Design System Factory sem ter feito pesquisa de usuário?**
R: Sim. Bono tem perguntas próprias para entender o produto e o público. Dados de pesquisa enriquecem o brand-brief, mas não são obrigatórios.

**P: Quantos componentes o sistema cobre?**
R: 24 componentes organizados em 4 categorias: Core (8), Feedback (5), Navigation (5) e Layout (6). Cobain também especifica como criar componentes adicionais — Dylan documenta isso no contributing guide.

**P: A documentação é para desenvolvedores ou designers?**
R: Para ambos. Dylan cria documentação em progressive disclosure: getting-started (10 min, para devs que vão usar), component guides (com exemplos de uso, anti-padrões e acessibilidade), foundations (para designers entenderem o sistema), e contributing guide (para quem quer expandir o sistema).

**P: E se precisar adicionar um novo componente depois que o pipeline terminou?**
R: O contributing guide de Dylan documenta o processo. Em síntese: Cobain especifica o novo componente (seguindo o mesmo formato, usando apenas tokens de Hendrix) → Marley audita → Dylan documenta. Prince pode ser acionado para coordenar.

**P: Como garanto que os tokens usados são apenas os que Hendrix definiu?**
R: Cobain é restrito por design — qualquer valor que não seja uma referência a token de Hendrix é considerado violação. Se precisar de um valor novo, Cobain declara o token ausente e espera Hendrix definir. Prince verifica essa consistência em cada gate.

**P: Os arquivos de tokens gerados funcionam com Style Dictionary, Theo ou similar?**
R: O `tokens.json` segue o formato do Design Tokens Community Group (W3C draft), que é compatível com Style Dictionary, Theo e outras ferramentas de transformação de tokens. Se precisar de um formato específico, informe Prince no Fase 0 e Hendrix adaptará a estrutura.
