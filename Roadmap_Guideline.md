# Roadmap — Guideline Técnico

```
                    🎯 META FINAL: MVP FUNCIONAL NA BANCA
                    ─────────────────────────────────────
```

## ═══════════════ FASE 1 — FUNDAÇÃO ═══════════════

```
[   SEMANA 1   ]  Setup de ambiente + Firebase + Estrutura
─────────────────────────────────────────────────────────────
```

```
    DIAS 1-2                      DIAS 3-4                         DIA 5
┌──────────────────┐      ┌──────────────────────┐      ┌────────────────────┐
│  Flutter SDK      │ ──→  │  Estrutura pastas    │ ←── │  Firebase pronto   │
│  Android Studio   │      │  Tema + Rotas        │      │  Auth + Firestore  │
│  `flutter doctor` │      │  main.dart funcional │      │  Regras segurança  │
│  Git/GitHub       │      │  Provider setup      │      │  PR #1 mergeado    │
└──────────────────┘      └──────────────────────┘      └────────────────────┘
         │                         │                            │
         │                         │                            │
         ▼                         ▼                            ▼
    ✔ SDK instalado          ✔ App roda no                ✔ Firebase conectado
      + emulador               emulador                      + PR aprovado
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  CHECKPOINT: flutter run funciona sem erro. Firebase Auth conectado.       │
│  PR #1 aprovado e mergeado na develop.                                     │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════════ FASE 2 — AUTH + NAVEGAÇÃO ═══════════════

```
[   SEMANA 2   ]  Login, cadastro, logout, navegação entre telas
─────────────────────────────────────────────────────────────────
```

```
    DIAS 6-7                       DIAS 8-9                         DIA 10
┌──────────────────────┐    ┌──────────────────────┐      ┌────────────────────┐
│  LoginScreen         │    │  Guarda de rota      │      │  PR #2 mergeado    │
│  RegisterScreen      │    │  Sessão persistente  │      │  Testes fluxo      │
│  AuthProvider        │ ──→ │  BottomNavBar        │ ←── │  Correções         │
│  Error handling PT   │    │  Dashboard esqueleto │      │  Review em grupo   │
│  User no Firestore   │    │  ProfileScreen       │      │                    │
└──────────────────────┘    └──────────────────────┘      └────────────────────┘
         │                           │                            │
         ▼                           ▼                            ▼
    ✔ Cadastro + login           ✔ App lembra                 ✔ Criar conta →
      funcionando                  sessão                       dashboard →
                                                                 logout
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  CHECKPOINT: criar conta → dashboard → logout → login volta ao dashboard. │
│  Fechar app reabre logado. Mensagens de erro em PT-BR.                     │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════════ FASE 3 — MÓDULOS ═══════════════

```
[  SEMANAS 3-4  ]  Dashboard + Rotina (disciplinas, notas, faltas)
──────────────────────────────────────────────────────────────────
```

```
    DIAS 11-14                     DIAS 15-18                      DIAS 19-22
┌──────────────────────┐    ┌──────────────────────┐      ┌────────────────────┐
│  GridView cards      │    │  Discipline model     │      │  Cálculo média     │
│  ModuleCard widget   │    │  DisciplinesScreen    │      │  Previsão final    │
│  DashboardProvider   │ ──→ │  Formulário validação │ ←── │  Controle faltas   │
│  Resumo horas        │    │  Lançar notas         │      │  Alertas visuais   │
│  Progresso visual    │    │  Salvar Firestore     │      │  Testes + PR #3    │
└──────────────────────┘    └──────────────────────┘      └────────────────────┘
```

---

```
[   SEMANA 5-6   ]  Certificados (upload + progresso)
───────────────────────────────────────────────────────
```

```
    DIAS 23-26                     DIAS 27-30
┌──────────────────────┐    ┌──────────────────────────┐
│  Certificate model    │    │  ProgressRing widget     │
│  StorageService       │ ──→ │  Horas totais no Dash   │
│  FilePicker/Image     │    │  Testes upload/delete   │
│  Upload Firestore     │    │  Correções + PR #4      │
└──────────────────────┘    └──────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  CHECKPOINT: upload de PDF → salva no Storage → lista na tela →            │
│  dashboard mostra total de horas com gráfico.                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

```
[   SEMANA 7   ]  Pesquisa TCC (OpenAlex API)
──────────────────────────────────────────────
```

```
    DIAS 31-34                     DIAS 35-37
┌──────────────────────┐    ┌──────────────────────────┐
│  OpenAlexService      │    │  Paginação resultados   │
│  Decodificar abstract │ ──→ │  Filtro por ano         │
│  ResearchProvider     │    │  Testes busca real      │
│  ArticleCard widget   │    │  PR #5                  │
└──────────────────────┘    └──────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  CHECKPOINT: buscar artigo → lista com título, autores, resumo, ano, link. │
│  Loading + erro + vazio tratados.                                          │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

```
[   SEMANA 8   ]  Radar Eventos (lista + mapa)
───────────────────────────────────────────────
```

```
    DIAS 38-41                     DIAS 42-44
┌──────────────────────┐    ┌──────────────────────────┐
│  Event model          │    │  Popup info no marker    │
│  EventProvider        │ ──→ │  Filtro por data         │
│  EventsScreen lista   │    │  Link de inscrição       │
│  flutter_map markers  │    │  Testes + PR #6          │
└──────────────────────┘    └──────────────────────────┘
```

---

## ═══════════════ FASE 4 — QUALIDADE ═══════════════

```
[   SEMANA 9   ]  Estabilização + Testes + Preparação banca
─────────────────────────────────────────────────────────────
```

```
    DIAS 45-47                     DIAS 48-50
┌──────────────────────────┐    ┌──────────────────────────────┐
│  Testes fluxo completo    │    │  Dados de demo              │
│  Correção bugs críticos  │ ──→ │  Contas de teste            │
│  Empty/loading/error     │    │  Vídeo backup               │
│  Review UX final         │    │  Slides apresentação         │
│  Regras Firestore        │    │  3 ensaios cronometrados    │
└──────────────────────────┘    └──────────────────────────────┘
         │                               │
         ▼                               ▼
    ✔ App sem crashes               ✔ Time pronto para banca
```

---

```
🎉 ENTREGA FINAL 🎉
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│    ✔ Auth funcionando      ✔ Dashboard com dados     ✔ Rotina calculando   │
│    ✔ Certificados salvos   ✔ OpenAlex buscando       ✔ Radar exibindo      │
│                                                                             │
│    ✔ 3 ensaios realizados  ✔ Vídeo backup pronto    ✔ Slides prontos       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```
