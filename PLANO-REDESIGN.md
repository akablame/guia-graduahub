# Plano de Redesign — GraduaHUB

> Redesign completo do portal `index.html` seguindo a identidade visual definida em `guias/IDENTIDADE-VISUAL.md`.
> Transição de estética **tech/gaming/neon** para **acadêmico clássico moderno**.

---

## Skills Envolvidas

| Skill | Uso |
|---|---|
| `frontend-design` | Direção estética geral, tipografia, composição, atmosfera visual |
| `ui-ux-pro-max` | Decisões de UI/UX, layout, hierarquia, micro-interações |
| `accessibility` | WCAG 2.2, contraste, foco, screen reader, prefers-reduced-motion |
| `fixing-motion-performance` | Animações performáticas (compositor-only, will-change, GPU) |
| `web-design-guidelines` | Revisão final contra boas práticas web |
| `performance` | Otimização de carregamento, font-display, lazy loading |

---

## Etapas

### Etapa 1 — Inventário e Análise

**O quê:** Catalogar todos os componentes, seções e funcionalidades do index.html atual para garantir que nada se perca na migração.

**Entregável:** Lista completa de:
- 12 seções de conteúdo (Visão, Guideline, Estudos, Execução, Testes, Git, Troubleshooting, Deploy, 5 Roadmaps, Checklist)
- ~30 componentes de UI (hero, cards, flow, road, sprints, study-week, milestones, stats, progress bars, people grid, contingency, tech grid, checklist, timeline, shimmer, popup, etc.)
- ~15 interações JS (typewriter, particles, scroll reveal, counters, confetti, ripple, swipe, timeline animation, progress bar, back-to-top, theme toggle, checklist persistence, keyboard shortcuts, achievement toast, drawer gesture)
- Assets externos (Google Fonts, favicon SVG)

**Skill:** Nenhuma (análise manual)

---

### Etapa 2 — Sistema de Design Tokens

**O quê:** Criar o sistema de variáveis CSS completo baseado no IDENTIDADE-VISUAL.md.

**Cores:**
```css
--nv:       #2C3539    /* navy charcoal - primary */
--nv-hover: #3d484d    /* navy hover */
--cream:    #F0EAD6    /* cream parchment - background */
--cream2:   #FAF8F3    /* off-white para cards */
--sage:     #8A9A5B    /* sage olive - accent */
--sage-dim: #B8B888    /* warm khaki - muted */
--ink:      #111111    /* near black - texto */
--ink2:     #6B7280    /* texto secundário */
--border:   #E5E1D8    /* separadores */
--white:    #FFFFFF    /* superfície de card */
```

**Tipografia:**
```css
--f-serif:  'Playfair Display', Georgia, serif;
--f-sans:   'Inter', system-ui, sans-serif;
```

**Escala:**
- `display-xl`: Playfair 700, 32-36px → hero/títulos de tela
- `display-lg`: Playfair 600, 24-28px → subtítulos de seção
- `display-md`: Playfair 500, 20-22px → títulos de card
- `label-caps`: Inter 700, 11-12px → ALL CAPS, letter-spacing 1.5px
- `body-lg`: Inter 400, 16px → texto principal
- `body-md`: Inter 400, 14px → descrições
- `body-sm`: Inter 400, 12px → metadados
- `ui-md`: Inter 500, 14px → botões, navegação
- `ui-sm`: Inter 500, 11px → tab bar labels

**Espaçamento:** 4/8/12/16/20/24/32px (múltiplos de 4)
**Raio:** 8/12/16/9999px (sm/md/lg/full)

**Skill:** `frontend-design`, `ui-ux-pro-max`

---

### Etapa 3 — Logo e Identidade Visual

**O quê:** Criar o monograma GH com coluna grega integrada + assinatura verbal.

- Monograma: **GH** onde o H tem colunas clássicas (capitéis) nas hastes verticais
- Abaixo: "GraduaHUB" em Playfair Display
- Separador: losango ♦
- Tagline: "CONHECIMENTO QUE TRANSFORMA. TRADIÇÃO QUE PERMANECE." (Inter, caps, letter-spacing 3px, sage)
- Ornamento: fleur-de-lis ✦ como divisor de seção
- Favicon: versão simplificada do monograma

**Entregável:** SVG inline do logotipo completo + favicon.

**Skill:** `frontend-design`

---

### Etapa 4 — Layout Base e Estrutura HTML

**O quê:** Reescrever a estrutura HTML com novo layout.

- Topbar navy `#2C3539` com hamburger, logo GH + nome, sino + avatar
- Drawer lateral navy (slide-in da esquerda)
- Fundo global cream `#F0EAD6` (nunca branco puro)
- Container centralizado com padding lateral 16-20px, max-width ~960px
- Bottom navigation bar para mobile (não existia antes) - 5 tabs navy
- Hierarquia: Top Bar → Título → Subtítulo → Search/Filtros → Cards → Bottom Bar

**Estrutura principal:**
```
[Skip Link]
[Top Bar - navy]
[Backdrop + Drawer - navy + cream text]
[Main]
  [Hero: tagline + título + descrição]
  [Section: Visão do Projeto]
  [Section: Guideline]
  [Section: Estudos]
  [Section: Execução]
  [Section: Testes]
  [Section: Git]
  [Section: Troubleshooting]
  [Section: Deploy]
  [Section: Roadmaps ×5]
  [Section: Checklist]
  [Footer]
```

**Skill:** `frontend-design`, `ui-ux-pro-max`

---

### Etapa 5 — Sistema de Componentes

**O quê:** Redesign de cada componente seguindo o novo estilo.

| Componente | Novo Visual |
|---|---|
| **Hero** | Tagline sage caps + título Playfair bold + descrição Inter |
| **Card** | Fundo white/off-white, border-radius 12-16px, shadow sutil, sem borda |
| **Stats** | Grid cards com número grande em Playfair, label sage caps |
| **Flow** | Horizontal scroll com itens navy/sage, minimal |
| **Road/Timeline** | Dot navy/sage, linha sage, labels Inter |
| **Sprint Grid** | Cards com top bar colorido (cada sprint uma cor funcional) |
| **Study Week** | Grid compacto, Inter, sage para destaque |
| **Milestones** | Número em círculo navy, texto Inter |
| **Progress Bar** | Track `#E5E1D8`, fill `#8A9A5B`, height 6-8px, pill shape |
| **People** | Avatar circular navy com inicial, grid 2 colunas |
| **Contingency** | 3 colunas, red/yellow/gray indicators |
| **Tech Grid** | 4 colunas, labels sage caps |
| **Checklist** | Checkbox arredondado, sage quando completo, progress ring |
| **Callouts** | Left border colorido (green/blue/purple/yellow/red) |
| **Tables** | Minimal, header navy/10% opacity |
| **Details/Accordion** | Seta sage, texto navy |
| **Tag Filter** | Pill shape, sage quando ativo, borda sutil |

**Skill:** `frontend-design`, `ui-ux-pro-max`, `accessibility`

---

### Etapa 6 — Interações e JavaScript

**O quê:** Refatorar todas as interações mantendo funcionalidade mas atualizando estética.

**Manter:**
- Scroll reveal com IntersectionObserver
- Typewriter (atualizar cores para sage)
- Checklist com localStorage + progress ring
- Back to top com ring progress
- Drawer toggle + swipe gesture
- Navigation active state via observer
- Roadmap click popup
- Achievement toast
- Ripple effect
- Keyboard shortcuts
- Reading progress bar (agora navy → sage)
- Theme toggle (se mantivermos — o novo design é propositalmente claro, sem dark mode)

**Remover:**
- Particles canvas (não combina com estética clássica)
- Confetti (inapropriado para tom sóbrio acadêmico)
- 3D/cursor follower
- Parallax orbs
- Noise overlay
- Geometric rings
- Grid background

**Adicionar:**
- Ilustração de prédio neoclássico (SVG/gravura) como elemento decorativo sutil
- Ornamentos ✦ entre seções
- Animações sutis de fade/slide (nada de neon/glow)
- Scroll-triggered reveal mais sutil (sem escala ou rotação)
- Loader minimalista (nada de shimmer com gradiente roxo)

**Skill:** `frontend-design`, `performance`, `fixing-motion-performance`

---

### Etapa 7 — Responsivo e Mobile

**O quê:** Adaptar o novo design para todos os tamanhos de tela.

- **Desktop (≥1024px):** Drawer fixa à esquerda (240px), main scrolla à direita
- **Tablet (640-1023px):** Layout adaptável, grids de 2-3 colunas
- **Mobile (<640px):** Topbar com drawer, bottom tab nav, grids de 1 coluna, touch targets ampliados (44px+), timeline dots maiores

**Pontos de quebra:** 640px e 1024px (mesmo do atual)

**Skill:** `ui-ux-pro-max`, `accessibility`

---

### Etapa 8 — Tipografia e Fontes

**O quê:** Implementar Playfair Display + Inter com carregamento otimizado.

- Google Fonts: `Playfair Display:wght@400;500;600;700;800` + `Inter:wght@400;500;600;700`
- `font-display: swap` para evitar layout shift
- Pré-conexão com `fonts.googleapis.com` e `fonts.gstatic.com`
- Fallbacks: `Georgia, serif` e `system-ui, sans-serif`

**Skill:** `performance`, `frontend-design`

---

### Etapa 9 — Acessibilidade

**O quê:** Garantir conformidade com WCAG 2.2 AA.

- Contraste: Navy `#2C3539` sobre Cream `#F0EAD6` → ~7.5:1 ✓
- Sage `#8A9A5B` sobre Cream → precisa verificar (~3:1, talvez escurecer para legibilidade de texto)
- Skip link
- `prefers-reduced-motion` para todas as animações
- `prefers-color-scheme` — o novo design é essencialmente claro, mas devemos considerar se navy/cream funciona como dark mode natural
- Roles e aria-labels em todos os elementos interativos
- Foco visível com navy outline
- Touch targets ≥ 44px

**Possível ajuste:** Texto em sage pode precisar de uma variante mais escura (`#6B7A4A` ou similar) para atingir 4.5:1 em texto pequeno.

**Skill:** `accessibility`, `ui-ux-pro-max`

---

### Etapa 10 — Revisão Final e Polimento

**O quê:** Verificar consistência, performance e qualidade.

- [ ] Todos os tokens de cor aplicados consistentemente
- [ ] Tipografia respeita a escala definida
- [ ] Sem gradientes ou efeitos de neon/glow
- [ ] Animações performáticas (compositor-only)
- [ ] Nenhum particle/confetti/orb restante
- [ ] Logo GH com coluna grega implementado
- [ ] Ornamentos ✦ posicionados
- [ ] Cards sem borda, só sombra sutil
- [ ] Fundo cream em todas as telas
- [ ] Contraste sage em texto pequeno verificado
- [ ] Responsivo testado em 3 breakpoints
- [ ] Acessibilidade validada (skip link, focus, reduced-motion)
- [ ] SEO (OpenGraph, JSON-LD) mantido/atualizado
- [ ] sitemap.xml e robots.txt mantidos

**Skill:** `web-design-guidelines`, `accessibility`, `performance`

---

## Resumo do Fluxo de Execução

```
Etapa 1 - Inventário      → Análise (sem skill)
Etapa 2 - Design Tokens   → frontend-design + ui-ux-pro-max
Etapa 3 - Logo            → frontend-design
Etapa 4 - Layout HTML     → frontend-design + ui-ux-pro-max
Etapa 5 - Componentes     → frontend-design + ui-ux-pro-max + accessibility
Etapa 6 - Interações      → frontend-design + performance + fixing-motion-performance
Etapa 7 - Responsivo      → ui-ux-pro-max + accessibility
Etapa 8 - Tipografia      → performance + frontend-design
Etapa 9 - Acessibilidade  → accessibility + ui-ux-pro-max
Etapa 10 - Revisão        → web-design-guidelines + accessibility + performance
```

## Ordem de Execução Recomendada

As etapas 2, 3 e 4 podem rodar **em paralelo** (são independentes). As etapas 5 e 6 dependem de 2-4 concluídas. Etapas 7, 8, 9 refinam em cima de 5-6. Etapa 10 é a validação final.

Preparado para iniciar quando autorizar.
