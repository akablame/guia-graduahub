# GraduaHUB — Identidade Visual

> Documento de referência para recriação completa do design e estilo do aplicativo. Serve como briefing para agente de IA implementar o sistema visual do zero.

---

## 1. Brand

| Atributo | Valor |
|---|---|
| Nome | GraduaHUB |
| Tagline | CONHECIMENTO QUE TRANSFORMA. TRADIÇÃO QUE PERMANECE. |
| Valores | VERITAS • DISCIPLINA • EXCELÊNCIA • PROPÓSITO |
| Personalidade | Acadêmico, clássico, confiável, elevado, rigoroso |

### Logotipo
- Monograma **"GH"** onde o "H" tem uma coluna clássica grega integrada em seu interior (substituindo as hastes verticais por colunas com capitel)
- Abaixo do monograma: tipografia "GraduaHUB" em Playfair Display, tamanho grande, peso regular/medium
- O monograma e o nome ficam centralizados verticalmente alinhados
- Separador decorativo: losango (♦) pequeno entre o monograma e o tagline
- Ornamentos tipográficos: fleur-de-lis (✦) usados como divisores de seção

---

## 2. Paleta de Cores

### Cores Primárias

| Nome | Hex | Uso |
|---|---|---|
| Navy Charcoal | `#2C3539` | Cor primária, fundos escuros, header, navbar, cards dark, ícones preenchidos |
| Cream Parchment | `#F0EAD6` | Fundo principal do app e das telas |
| Near Black | `#111111` | Texto principal sobre fundos claros |

### Cores de Destaque

| Nome | Hex | Uso |
|---|---|---|
| Sage Olive | `#8A9A5B` | Accent principal — itens ativos, progress bars, labels de categoria, ícone da tab ativa |
| Warm Khaki | `#B8B888` | Secundário — bordas sutis, ícones inativos, texto de suporte |

### Cores Funcionais (derivadas)

| Nome | Hex aproximado | Uso |
|---|---|---|
| Fundo de Card | `#FFFFFF` ou `#FAF8F3` | Cards de conteúdo sobre o fundo cream |
| Texto Secundário | `#6B7280` | Subtítulos, metadados, legendas |
| Separador | `#E5E1D8` | Linhas divisórias entre seções |
| Overlay escuro | `#2C3539` com 90% opacidade | Drawer lateral, modais |

### Regras de Uso
- **Nunca** usar fundo branco puro (`#FFFFFF`) nas telas principais — sempre usar o cream `#F0EAD6` ou `#FAF8F3`
- O verde sage `#8A9A5B` é exclusivo para estados ativos, progresso e destaques funcionais — não usar como cor decorativa genérica
- O navy `#2C3539` domina todos os elementos de navegação (top bar, bottom bar, drawer)

---

## 3. Tipografia

### Famílias

| Família | Tipo | Uso |
|---|---|---|
| **Playfair Display** | Serif (Google Fonts) | Títulos de tela (H1, H2), nome do app, logotipo, títulos de artigos e seções importantes |
| **Inter** | Sans-serif (Google Fonts) | Todo o restante — corpo de texto, labels, botões, metadados, navegação, inputs |

### Escala Tipográfica

| Token | Família | Tamanho | Peso | Uso |
|---|---|---|---|---|
| `display-xl` | Playfair Display | 32–36px | 700 | Títulos principais de tela |
| `display-lg` | Playfair Display | 24–28px | 600 | Subtítulos de seção, título de artigo |
| `display-md` | Playfair Display | 20–22px | 500 | Títulos de card |
| `label-caps` | Inter | 11–12px | 700 | Labels em CAPS (ex: "ARTIGO CIENTÍFICO", "RESUMO") — letter-spacing: 1.5px |
| `body-lg` | Inter | 16px | 400 | Texto de leitura principal |
| `body-md` | Inter | 14px | 400 | Descrições, parágrafos secundários |
| `body-sm` | Inter | 12px | 400 | Metadados, legendas |
| `ui-md` | Inter | 14px | 500 | Botões, navegação, labels de ação |
| `ui-sm` | Inter | 11px | 500 | Labels de tab bar, ícones com texto |

### Regras Tipográficas
- Taglines e valores da marca: Inter, ALL CAPS, letter-spacing generoso (2–3px), peso 400–500
- Títulos de artigos científicos: Playfair Display, peso normal (400–500), line-height 1.35
- Categorias de conteúdo (ex: "ARTIGO CIENTÍFICO"): Inter ALL CAPS, cor sage `#8A9A5B`, letter-spacing 1.5px, tamanho 11px

---

## 4. Iconografia

### Estilo
- Ícones **outlined** (linha) para navegação e ações
- Ícones **filled** (preenchido) no estado ativo da tab bar
- Traço fino, cantos levemente arredondados
- Tamanho base: 24×24px (tab bar), 20×20px (ações inline)

### Ícones dos Módulos Principais (preenchidos em círculo navy `#2C3539`)
| Módulo | Ícone | Descrição |
|---|---|---|
| ORGANIZE | Livro aberto | Centralizar materiais e referências |
| PESQUISE | Coluna/instituição clássica | Acesso a bases científicas |
| PRODUZA | Pena/quill | Escrita e produção acadêmica |
| EVOLUA | Coroa de louros | Progresso acadêmico |

### Tab Bar (5 itens)
| Tab | Ícone |
|---|---|
| Início | Coluna/prédio (ícone institucional) |
| Biblioteca | Livros |
| Tarefas | Clipboard/checklist |
| Pesquisa | Lupa (ativo = sage `#8A9A5B`) |
| Perfil | Pessoa/silhueta |

---

## 5. Componentes de UI

### Top Bar / Header
- Fundo: `#2C3539` (navy)
- Esquerda: ícone hamburger menu (branco/cream)
- Centro: logotipo GH + "GraduaHUB" em cream/branco
- Direita: ícone sino (notificações) + avatar circular do perfil
- Altura: ~56–60px

### Bottom Tab Bar
- Fundo: `#2C3539` (navy)
- Ícones inativos: `#B8B888` (khaki) ou branco com 50% opacidade
- Ícone/label ativo: `#8A9A5B` (sage)
- Label: Inter, 11px, abaixo do ícone
- Borda superior: nenhuma ou sutil (1px sage/20%)

### Cards de Conteúdo
- Fundo: branco `#FFFFFF` ou off-white `#FAF8F3`
- Border radius: 12–16px
- Sombra: leve, `rgba(0,0,0,0.06)` 0 2px 8px
- Padding interno: 16–20px
- Sem borda explícita (usa sombra)

**Estrutura interna do card de artigo:**
```
[LABEL CATEGORIA]   [ícone bookmark] [ícone menu ⋮]
[Título do artigo em Playfair Display bold]
[Publicação — Vol. — Data]
[Autores]
─────────────────────────────────
[RESUMO]  ← label caps sage
[Parágrafo de resumo em Inter]
─────────────────────────────────
[Baixar PDF]  [Citar]  [Salvar]  [Compartilhar]  ← ações com ícone + texto
─────────────────────────────────
[Progresso de Leitura]          [65% concluído]
[████████░░░░░░░] barra sage
[Tempo estimado]        [X de Y páginas]
```

### Search Bar
- Fundo: branco ou `#F5F3EE`
- Borda: 1px `#E5E1D8` ou sem borda com sombra interna
- Border radius: 10–12px
- Ícone lupa à esquerda (cinza)
- Placeholder: "Buscar artigos, temas ou autores..."
- Ícone de filtro à direita

### Barra de Progresso
- Track (fundo): `#E5E1D8` (cinza warm)
- Fill (preenchimento): `#8A9A5B` (sage green)
- Altura: 6–8px
- Border radius: full (pill)

### Botões de Ação Inline (Baixar PDF, Citar, etc.)
- Layout: ícone acima + texto abaixo, centralizados
- Cor do ícone: `#2C3539` ou `#6B7280`
- Texto: Inter 12px, cinza
- Sem fundo, sem borda (ghost)
- Dispostos em linha horizontal com espaçamento igual

### Labels de Categoria (ex: "ARTIGO CIENTÍFICO")
- Inter, ALL CAPS, 11px, peso 700
- Cor: `#8A9A5B` (sage)
- Letter-spacing: 1.5px
- Sem fundo ou background (texto puro)

---

## 6. Padrões de Layout

### Fundo Global
- Cor: `#F0EAD6` (cream parchment)
- Não usar gradientes no fundo principal

### Espaçamento Base
- Grid: múltiplos de 4px (4, 8, 12, 16, 20, 24, 32)
- Padding lateral de tela: 16–20px
- Gap entre cards: 12–16px

### Hierarquia Visual de uma Tela
```
[TOP BAR — navy]
[Título da tela — Playfair Display, bold, ~28px, cor #111111]
[Subtítulo/descrição — Inter, 14px, cinza]
[Search bar ou filtros]
[Cards de conteúdo sobre fundo cream]
[BOTTOM TAB BAR — navy]
```

### Drawer Lateral
- Fundo: `#2C3539` (navy)
- Texto/ícones: cream/branco
- Abre da esquerda (slide-in)
- Contém: logo, navegação principal, rodapé com links

---

## 7. Estética e Estilo Geral

### Conceito
O GraduaHUB evoca a tradição acadêmica clássica (universidades europeias, arquitetura neoclássica) com uma interface moderna e funcional. A dualidade é intencional: seriedade e rigor (Playfair, navy, cream) + clareza e usabilidade (Inter, espaçamento generoso, cards limpos).

### Elementos Decorativos
- Ilustração de prédio universitário neoclássico (sketch/gravura, tom sépia/cream) usada como asset de background ou em telas de onboarding
- Ornamentos tipográficos: ✦ (fleur-de-lis estilizada) como divisor de seção
- Losango ♦ pequeno como separador entre logotipo e tagline

### Tom Visual
- **Sóbrio mas não frio** — o cream aquece o navy
- **Clássico mas não antiquado** — Inter moderniza o Playfair
- **Elegante mas acessível** — espaçamento amplo, hierarquia clara

### O que EVITAR
- Cores vibrantes/neón — o accent máximo é o sage `#8A9A5B`
- Fundos brancos puros — sempre cream
- Fontes sans-serif em títulos principais — reservar para UI
- Sombras pesadas ou elevações exageradas
- Bordas coloridas em cards
- Dark mode com cores diferentes — se implementado, usar navy como fundo principal e cream como texto

---

## 8. Módulos do App (contexto funcional)

| Módulo | Ícone | Função |
|---|---|---|
| Início | Coluna | Dashboard principal |
| Biblioteca | Livro | Acesso a artigos e materiais salvos |
| Tarefas | Clipboard | Gestão de tarefas e prazos acadêmicos |
| Pesquisa | Lupa | Busca em bases científicas (tela principal vista na imagem) |
| Perfil | Pessoa | Dados do usuário e configurações |

### Tela de Pesquisa (referência detalhada da imagem)
- Header com título "Assistente de Tese" em Playfair Display bold
- Subtítulo "Leitura, análise e síntese de artigos científicos." em Inter
- Search bar full-width
- Cards de artigo com: categoria label, título, publicação, autores, resumo, ações, progresso de leitura

---

## 9. Tokens de Design (para implementação)

```
colors:
  primary:        #2C3539
  accent:         #8A9A5B
  background:     #F0EAD6
  surface:        #FFFFFF
  text-primary:   #111111
  text-secondary: #6B7280
  text-muted:     #B8B888
  border:         #E5E1D8
  progress-track: #E5E1D8
  progress-fill:  #8A9A5B

typography:
  font-display:   "Playfair Display", Georgia, serif
  font-ui:        "Inter", system-ui, sans-serif

radius:
  sm:   8px
  md:   12px
  lg:   16px
  full: 9999px

spacing:
  xs:   4px
  sm:   8px
  md:   16px
  lg:   24px
  xl:   32px
```
