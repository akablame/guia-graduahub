# Roadmap — Plano de Execução

```mermaid
gantt
    title Cronograma Macro — 10 Semanas
    dateFormat  YYYY-MM-DD
    axisFormat  Semana %W

    section Sprints
    Sprint 0 — Fundação              :s0, 2024-01-01, 5d
    Sprint 1 — Auth + Navegação      :s1, after s0, 5d
    Sprint 2 — Dashboard             :s2, after s1, 4d
    Sprint 3 — Rotina                :s3, after s2, 8d
    Sprint 4 — Certificados          :s4, after s3, 8d
    Sprint 5 — Pesquisa TCC          :s5, after s4, 7d
    Sprint 6 — Radar Eventos         :s6, after s5, 7d
    Sprint 7 — Qualidade + Banca     :s7, after s6, 6d
```

---

## Sprints Detalhadas

### Sprint 0 — Fundação (Dias 1-5)

```mermaid
flowchart LR
    subgraph Todos[Dias 1-2]
        SDK[Flutter SDK + Android Studio] --> Doctor[flutter doctor OK]
        Git[GitHub repo] --> Create[flutter create]
    end

    subgraph Time[Dias 3-4]
        PessoaA["Pessoa A<br>pastas + routes + main"] --> PessoaB["Pessoa B<br>tema + componentes"]
        PessoaC["Pessoa C<br>Firebase + Firestore"] --> PessoaD["Pessoa D<br>board + docs"]
    end

    subgraph Fim[Dia 5]
        AuthService[AuthService + AuthProvider] --> FirestoreS[FirestoreService]
        Regras[Regras segurança] --> PR1["PR #1 mergeado"]
    end

    Todos --> Time --> Fim
```

**Checkpoint:** `flutter run` sem erro ✅ | Firebase conectado ✅ | PR #1 mergeado ✅

---

### Sprint 1 — Auth + Navegação (Dias 6-10)

```mermaid
flowchart LR
    subgraph Dias6_7[Dias 6-7]
        Login[LoginScreen] --> Register[RegisterScreen]
        AuthP[AuthProvider erros PT] --> UserFS[User no Firestore]
    end

    subgraph Dias8_9[Dias 8-9]
        Guarda[Guarda de rota] --> Sessao[Sessão persistente]
        BottomNav[BottomNavigationBar] --> Dash[Dashboard esqueleto]
        Profile[ProfileScreen] --> Sair[Botão sair]
    end

    subgraph Dia10[Dia 10]
        Testes[Testes fluxo] --> Correcao[Correções]
        Review[Review grupo] --> PR2["PR #2 mergeado"]
    end

    Dias6_7 --> Dias8_9 --> Dia10
```

**Checkpoint:** Login/Cadastro ✅ | Sessão persistente ✅ | Navegação ✅ | PR #2 ✅

---

### Sprint 2 — Dashboard (Dias 11-14)

```mermaid
flowchart LR
    subgraph Dias11_12[Dias 11-12]
        Grid[GridView cards] --> ModuleCard[ModuleCard widget]
        DashP[DashboardProvider] --> NavegacaoCards[Navegação dos cards]
    end

    subgraph Dias13_14[Dias 13-14]
        Resumo[Resumo horas] --> Contagem[Contagem disciplinas]
        Progresso[Progresso visual] --> PR3["PR #3"]
    end

    Dias11_12 --> Dias13_14
```

**Checkpoint:** Dashboard com cards ✅ | Resumo horas ✅ | Contagem ✅ | PR #3 ✅

---

### Sprint 3 — Rotina (Dias 15-22)

```mermaid
flowchart LR
    subgraph Dias15_17[Dias 15-17]
        ModelDisc[Discipline model] --> ListaDisc[Lista disciplinas]
        FormDisc[Formulário validação] --> Salvamento[Salvar Firestore]
    end

    subgraph Dias18_20[Dias 18-20]
        Notas[Lançar notas] --> Media[Cálculo média]
        Previsao[Previsão nota final] --> Faltas[Controle faltas]
        Alertas[Alertas visuais] --> Calculos[Cálculos funcionando]
    end

    subgraph Dias21_22[Dias 21-22]
        TestesRotina[Testes fluxo] --> CorrecaoRotina[Correções]
        ReviewRotina[Review] --> PR4["PR #4"]
    end

    Dias15_17 --> Dias18_20 --> Dias21_22
```

**Checkpoint:** CRUD disciplinas ✅ | Cálculo média ✅ | Previsão final ✅ | Faltas ✅ | PR #4 ✅

---

### Sprint 4 — Certificados (Dias 23-30)

```mermaid
flowchart LR
    subgraph Dias23_25[Dias 23-25]
        CertModel[Certificate model] --> StorageS[StorageService]
        CertProvider[CertificateProvider] --> Upload[Upload FilePicker]
    end

    subgraph Dias26_28[Dias 26-28]
        FirestoreCert[Salvar Firestore] --> ListaCert[Lista certificados]
        ProgressRing[ProgressRing widget] --> TotalHoras[Total no Dashboard]
    end

    subgraph Dias29_30[Dias 29-30]
        TestesCert[Testes upload/delete] --> CorrecaoCert[Correções]
        PR5["PR #5"]
    end

    Dias23_25 --> Dias26_28 --> Dias29_30
```

**Checkpoint:** Upload PDF/imagem ✅ | Lista certificados ✅ | Progresso visual ✅ | PR #5 ✅

---

### Sprint 5 — Pesquisa TCC (Dias 31-37)

```mermaid
flowchart LR
    subgraph Dias31_33[Dias 31-33]
        OAS[OpenAlexService] --> Abstract[Decodificar abstract]
        ResearchP[ResearchProvider] --> Busca[Campo de busca]
    end

    subgraph Dias34_36[Dias 34-36]
        ArticleCard[ArticleCard widget] --> ListaOA[Lista resultados]
        Paginacao[Paginação] --> FiltroAno[Filtro ano]
    end

    subgraph Dia37[Dia 37]
        TestesOA[Testes busca real] --> PR6["PR #6"]
    end

    Dias31_33 --> Dias34_36 --> Dia37
```

**Checkpoint:** Busca OpenAlex ✅ | Cards com dados ✅ | Loading/erro/vazio ✅ | PR #6 ✅

---

### Sprint 6 — Radar Eventos (Dias 38-44)

```mermaid
flowchart LR
    subgraph Dias38_40[Dias 38-40]
        EventModel[Event model] --> EventProvider[EventProvider]
        DadosMock[Dados mock Firestore] --> ListaEvent[Lista eventos]
    end

    subgraph Dias41_43[Dias 41-43]
        Mapa[flutter_map + markers] --> Popup[Popup info]
        FiltroData[Filtro por data] --> LinkEvent[Link inscrição]
    end

    subgraph Dia44[Dia 44]
        TestesEvent[Testes mapa/lista] --> PR7["PR #7"]
    end

    Dias38_40 --> Dias41_43 --> Dia44
```

**Checkpoint:** Lista eventos ✅ | Mapa com markers ✅ | Popup ✅ | Filtro data ✅ | PR #7 ✅

---

### Sprint 7 — Qualidade + Banca (Dias 45-50)

```mermaid
flowchart LR
    subgraph Dias45_47[Dias 45-47]
        TestesFim[Testes fluxo completo] --> Bugs[Bugs críticos]
        UX[UX + loading + erro] --> RegrasFS[Regras Firestore]
    end

    subgraph Dias48_49[Dias 48-49]
        Demo[Dados de demo] --> Contas[3 contas teste]
        Video[Vídeo backup] --> Slides[Slides]
    end

    subgraph Dia50[Dia 50]
        Ensaio1[Ensaio 1] --> Ensaio2[Ensaio 2]
        Ensaio2 --> Ensaio3[Ensaio 3]
        Ensaio3 --> Banca["🎯 Banca!"]
    end

    Dias45_47 --> Dias48_49 --> Dia50
```

**Checkpoint Final:**

- Auth ✅ | Dashboard ✅ | Rotina ✅ | Certificados ✅ | Pesquisa ✅ | Radar ✅
- 3 ensaios realizados ✅ | Vídeo backup ✅ | Slides prontos ✅

---

## Plano de Contingência

```mermaid
flowchart TD
    subgraph Prioridade1[NÃO PULAR]
        P1a["1º Auth + Dashboard"] --> P1b["2º Rotina"]
        P1b --> P1c["3º Certificados v1"]
    end

    subgraph Prioridade2[REDUZIR ESCOPO]
        P2a["4º Pesquisa TCC (sem paginação)"] --> P2b["5º Radar (só lista)"]
    end

    subgraph Prioridade3[CORTAR]
        P3a["OCR automático"] --> P3b["Scraper Python"]
        P3b --> P3c["Notificações push"]
    end

    Prioridade1 --> Prioridade2 --> Prioridade3
```

---

## Distribuição por Pessoa (Equipe de 4)

```mermaid
flowchart LR
    subgraph Pessoas
        A["Pessoa A<br>Líder Técnico"] --> Auth[Auth + Provider + Firebase]
        B["Pessoa B<br>Dev Front"] --> Telas[Telas + Dashboard + Rotina]
        C["Pessoa C<br>Dev Dados"] --> Dados[Modelos + Services + Storage]
        D["Pessoa D<br>QA/Doc"] --> Testes[Testes + Docs + Slides]
    end
```
