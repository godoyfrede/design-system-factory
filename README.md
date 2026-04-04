# Design System Factory

**Pipeline multi-agente para criação de design systems completos.**
Da identidade de marca ao component library documentado e acessível — com gates de aprovação em cada fase.

## Instalação

### Local (Claude Code CLI)
```
/plugin marketplace add "C:\Users\fredy\OneDrive\Documentos\Claude\design-system-factory"
```

### Compartilhável (GitHub)
```
/plugin marketplace add https://github.com/godoyfrede/design-system-factory
/plugin install design-system-factory@design-system-factory
```

### IDE (VS Code / JetBrains)
O plugin usa a estrutura padrão `.claude-plugin/` e funciona automaticamente nas
extensões Claude Code para VS Code e JetBrains — sem configuração adicional.

---

## Como Usar

Fale com **Prince** (o Orquestrador):

```
"Preciso criar um design system para o nosso SaaS B2B"
→ Pipeline completo: escopo → marca → tokens → componentes → acessibilidade → docs

"Só preciso atualizar a paleta de cores"
→ Hendrix direto, sem acionar o pipeline completo

"Verifica se o design system está acessível"
→ Marley direto para auditoria WCAG
```

---

## Os 6 Agentes

| Agente | Papel | Responsabilidade Principal |
|--------|-------|---------------------------|
| **prince** | Orquestrador | Roteamento, coerência sistêmica, gates, FACTORY_PROGRESS.md |
| **bono** | Estrategista de Marca | Identidade visual, arquétipo de marca, princípios de design |
| **hendrix** | Arquiteto de Tokens | Tokens de cor, tipografia, espaçamento, elevação, motion |
| **cobain** | Arquiteto de Componentes | 24 componentes com variantes, estados e código de referência |
| **marley** | Auditor de Acessibilidade | WCAG 2.1/3.0, keyboard nav, screen reader — gate bloqueante |
| **dylan** | Escritor de Documentação | Getting started, component guides, contributing guide |

---

## Pipeline com Gates de Usuário

```
Prince (entry point)
    |
    Fase 0: Prince — escopo + princípios do sistema
    🔴 GATE: usuário valida princípios

    Fase 1: Bono — Estratégia de Marca
            → brand-brief.md
    🔴 GATE: usuário aprova direção visual

    Fase 2: Hendrix — Design Tokens
            → tokens.md + tokens.json
    🔴 GATE: usuário aprova tokens + verificação WCAG

    Fase 3: Cobain — Biblioteca de Componentes
            → components/[componente].md
    🔴 GATE: usuário aprova componentes-core

    Fase 4: Marley — Auditoria de Acessibilidade
            → accessibility-report.md
    🔴 GATE: zero issues críticos antes de avançar

    Fase 5: Dylan — Documentação Completa
            → README, getting-started, foundations/, component guides
    🔴 GATE: aprovação final da documentação

    Prince: DESIGN_SYSTEM_COMPLETE.md — entrega final
```

---

## Skill Disponível

| Skill | Uso | Trigger |
|-------|-----|---------|
| `/design-system` | Pipeline completo com todos os gates | "criar design system" / "precisamos de um sistema visual" |

---

## Arquitetura de Tokens (3 Níveis)

O **Hendrix** usa uma arquitetura de tokens em 3 camadas que separa primitivos de intenção:

```
Nível 1 — Core Tokens (primitivos)
  color.blue.500 = #2563EB

Nível 2 — Semantic Tokens (intenção)
  color.brand.primary = {color.blue.500}

Nível 3 — Component Tokens (contexto)
  button.primary.background = {color.brand.primary}
```

Cobain usa **apenas** tokens de Nível 3. Nunca valores hard-coded.

---

## Componentes Cobertos

**Core:** Button, Input, Textarea, Select, Checkbox, Radio, Toggle, Badge, Tag, Avatar, Icon
**Feedback:** Alert, Toast, Spinner, Empty State, Error State
**Navigation:** Navbar, Sidebar, Tabs, Breadcrumb, Pagination
**Layout:** Card, Modal, Dropdown, Accordion, Table, Form

---

## Artefatos Gerados

```
docs/design-system/
├── FACTORY_PROGRESS.md           ← painel de controle (sempre atualizado)
├── system-scope.md               ← Prince (Fase 0)
├── brand-brief.md                ← Bono (Fase 1)
├── tokens.md                     ← Hendrix (Fase 2)
├── tokens.json                   ← Hendrix (Fase 2) — pronto para implementação
├── accessibility-report.md       ← Marley (Fase 4)
├── DESIGN_SYSTEM_COMPLETE.md     ← Prince — declaração de entrega
│
├── components/                   ← Cobain (Fase 3)
│   ├── button.md
│   ├── input.md
│   └── [...]
│
└── docs/                         ← Dylan (Fase 5)
    ├── README.md
    ├── getting-started.md
    ├── contributing.md
    ├── foundations/
    └── components/
```

---

## Integração com Outros Times

### ← UX Research Lab
Mercury entrega `personas-overview.md` → Bono usa para definir tom e voz da marca

### → Sgt. Peppers AI Band
Hendrix entrega `tokens.json` → Paul (Frontend) usa como base para implementação
Dylan entrega `getting-started.md` → Paul usa como referência de uso dos componentes

---

## Skill-Learning

Os agentes aprendem com o uso:
- Cada agente tem `memory: user` ativado
- Prince mantém `FACTORY_PROGRESS.md` atualizado em cada fase
- Inconsistências entre fases são detectadas automaticamente pelo Prince

---

## Compatibilidade

- Claude Code CLI
- Extensão VS Code Claude Code
- Extensão JetBrains Claude Code
- Qualquer ambiente que suporte a estrutura `.claude-plugin/`

---

## Criador

<p align="center">
  Criado com 🎸 por <strong>Frederico Clemente</strong><br/>
  <a href="https://github.com/godoyfrede">github.com/godoyfrede</a>
</p>

> Uso livre com atribuição obrigatória ao criador — veja [LICENSE](./LICENSE).
