# Roadmap — Guideline Técnico

```mermaid
flowchart LR
    subgraph F1[Fase 1 — Fundação]
        direction TB
        A1[Flutter SDK] --> A2[Firebase] --> A3[Estrutura] --> A4[PR #1]
    end

    subgraph F2[Fase 2 — Auth + Nav]
        direction TB
        B1[Login] --> B2[Guarda rota] --> B3[Navegação] --> B4[PR #2]
    end

    subgraph F3[Fase 3 — Módulos]
        direction TB
        C1[Dashboard] --> C2[Rotina] --> C3[Certificados] --> C4[Pesquisa TCC] --> C5[Radar]
    end

    subgraph F4[Fase 4 — Qualidade]
        direction TB
        D1[Testes] --> D2[Correções] --> D3[Dados demo] --> D4[Banca]
    end

    F1 --> F2 --> F3 --> F4
```

---

## Fase 1 — Fundação (Dias 1-5)

```mermaid
flowchart LR
    subgraph Dia1[Dias 1-2]
        SDK[Flutter SDK] --> Doc[flutter doctor]
        Studio[Android Studio] --> Emulador[Emulador]
        Git[GitHub] --> Repo[Repositório]
    end

    subgraph Dia2[Dias 3-4]
        Estrutura[Pastas lib/] --> Tema[Tema + Rotas]
        Firebase[Firebase Console] --> FlutterFire[flutterfire configure]
        Provider[Provider setup] --> Main[main.dart]
    end

    subgraph Dia3[Dia 5]
        AuthS[AuthService] --> AuthP[AuthProvider]
        FSS[FirestoreService] --> Regras[Regras segurança]
        PR["PR #1 mergeado"] --> OK["✔ flutter run + Firebase OK"]
    end

    Dia1 --> Dia2 --> Dia3
```

### Entregas da Fase 1

- `flutter run` funcionando sem erros
- Firebase conectado (Auth, Firestore, Storage)
- Estrutura de pastas criada (`core/`, `data/`, `features/`, `providers/`)
- Tema global definido
- AuthService + FirestoreService + AuthProvider implementados
- PR #1 aprovado e mergeado na `develop`

---

## Fase 2 — Auth + Navegação (Dias 6-10)

```mermaid
flowchart LR
    subgraph Dias6_7[Dias 6-7]
        Login[LoginScreen] --> Register[RegisterScreen]
        AuthP2[AuthProvider] --> Erros[Erros PT-BR]
    end

    subgraph Dias8_9[Dias 8-9]
        Guarda[Guarda de rota] --> Sessao[Sessão persistente]
        BottomNav[BottomNavBar] --> Dash[Dashboard esqueleto]
    end

    subgraph Dia10[Dia 10]
        Testes[Testes fluxo] --> Correcao[Correções]
        Revisao[Review grupo] --> PR2["PR #2 mergeado"]
    end

    Dias6_7 --> Dias8_9 --> Dia10
```

### Entregas da Fase 2

- Criar conta → dashboard automatizado
- Login com email existente → dashboard
- Logout → volta para login
- Fechar e reabrir app → continua logado
- Mensagens de erro em português
- PR #2 mergeado

---

## Fase 3 — Módulos (Dias 11-44)

### Dashboard (Dias 11-14)
```mermaid
flowchart LR
    Grid[GridView cards] --> Card[ModuleCard widget]
    DashP[DashboardProvider] --> Resumo[Resumo horas + contagem]
    Progresso[Progresso visual] --> PR3["PR #3"]
```

### Rotina (Dias 15-22)
```mermaid
flowchart LR
    Model[Discipline model] --> Form[Formulário validação]
    Notas[Lançar notas] --> Media[Cálculo média ponderada]
    Previsao[Previsão nota final] --> Faltas[Controle faltas]
    Alertas[Alertas visuais] --> PR4["PR #4"]
```

### Certificados (Dias 23-30)
```mermaid
flowchart LR
    CertModel[Certificate model] --> Upload[Upload Storage]
    Lista[Lista certificados] --> Progress[Progress Ring]
    Total[Total horas no Dash] --> PR5["PR #5"]
```

### Pesquisa TCC (Dias 31-37)
```mermaid
flowchart LR
    OA[OpenAlex Service] --> Abstract[Decodificar abstract]
    Card2[ArticleCard widget] --> Paginacao[Paginação]
    Filtro[Filtro ano] --> PR6["PR #6"]
```

### Radar Eventos (Dias 38-44)
```mermaid
flowchart LR
    Event[Event model] --> Lista2[Lista eventos]
    Mapa[flutter_map markers] --> Popup[Popup info]
    Filtro2[Filtro data] --> Link[Link inscrição]
    Testes2[Testes] --> PR7["PR #7"]
```

---

## Fase 4 — Qualidade + Banca (Dias 45-50)

```mermaid
flowchart LR
    subgraph Dias45_47[Dias 45-47]
        TestesFim[Testes fluxo completo] --> Bugs[Correção bugs críticos]
        UX[Empty / Loading / Error] --> RevisaoUX[Review UX final]
    end

    subgraph Dias48_49[Dias 48-49]
        Demo[Dados de demo] --> Contas[Contas de teste]
        Video[Vídeo backup] --> Slides[Slides apresentação]
    end

    subgraph Dia50[Dia 50]
        E1[Ensaio 1] --> E2[Ensaio 2]
        E2 --> E3[Ensaio 3]
        E3 --> Backup[Backup final]
    end

    Dias45_47 --> Dias48_49 --> Dia50
```

### Checklist Final da Banca

- **Auth:** login, cadastro, logout, sessão persistente
- **Dashboard:** cards dos módulos, resumo horas, contagem disciplinas
- **Rotina:** CRUD disciplinas, cálculo média, previsão final, faltas
- **Certificados:** upload, lista, progresso visual
- **Pesquisa TCC:** busca OpenAlex, cards com dados
- **Radar:** lista eventos, mapa com markers
- **Qualidade:** loading em tudo, erro tratado, empty states
- **Apresentação:** 3 ensaios, vídeo backup, slides prontos
