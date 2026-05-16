# Roadmap — Plano de Estudos

```mermaid
gantt
    title Trilha de Aprendizado — 4 Semanas
    dateFormat  YYYY-MM-DD
    axisFormat  %d/%m

    section Semana 1
    Dart I — Variáveis, funções, null safety      :s1a, 2024-01-01, 1d
    Dart II — Classes, listas, mapas              :s1b, after s1a, 1d
    Flutter I — Primeiro app, widgets             :s1c, after s1b, 1d
    Flutter II — Navegação, forms                 :s1d, after s1c, 1d
    Listas + Layout + Grid                        :s1e, after s1d, 1d
    Reforço / Revisão                             :s1f, after s1e, 1d

    section Semana 2
    Provider — ChangeNotifier, Consumer           :s2a, after s1f, 1d
    Firebase Auth — login, cadastro               :s2b, after s2a, 1d
    Firestore CRUD — models, streams              :s2c, after s2b, 1d
    Firebase Storage — upload, image picker       :s2d, after s2c, 1d
    HTTP + OpenAlex API                           :s2e, after s2d, 1d
    Reforço / Revisão                             :s2f, after s2e, 1d

    section Semana 3
    Mini Projeto 1 — ToDo completo                :s3a, after s2f, 2d
    Mini Projeto 2 — CRUD + Upload                :s3b, after s3a, 2d
    Revisão + Correções + PR                      :s3c, after s3b, 1d
    Entrega dos projetos                          :s3d, after s3c, 1d

    section Semana 4
    Navegação avançada — BottomNav, IndexedStack  :s4a, after s3d, 1d
    Maps — flutter_map, markers                   :s4b, after s4a, 1d
    OCR — ML Kit text recognition                 :s4c, after s4b, 1d
    Animações — AnimatedContainer, Hero           :s4d, after s4c, 1d
    Revisão geral — juntar tudo                   :s4e, after s4d, 1d
```

---

## Semana 1 — Dart + Flutter Base

```mermaid
flowchart LR
    subgraph Seg[Dia 1 — Dart I]
        Variaveis[Variáveis] --> Funcoes[Funções]
        Funcoes --> NullSafety[Null safety]
        NullSafety --> Ex10["10 exercícios"]
    end

    subgraph Ter[Dia 2 — Dart II]
        Classes[Classes] --> Listas[Listas]
        Listas --> Mapas[Mapas]
        Mapas --> ExAluno[Classe Aluno com média]
    end

    subgraph Qua[Dia 3 — Flutter I]
        Criar[flutter create] --> Widgets[Widgets básicos]
        Widgets --> AppRodando[App rodando no emulador]
    end

    subgraph Qui[Dia 4 — Flutter II]
        Navegacao[Navegação push/pop] --> Forms[Formulários]
        Forms --> Validacao[Validação]
        Validacao --> App3Telas[App com 3 telas]
    end

    subgraph Sex[Dia 5 — Listas]
        ListView[ListView.builder] --> CardCustom[Card customizado]
        CardCustom --> Grid[GridView]
        Grid --> Lista20[20 cards na tela]
    end

    Seg --> Ter --> Qua --> Qui --> Sex
```

**Marco da Semana 1:** App com 3 telas navegáveis + formulário com validação rodando no emulador.

---

## Semana 2 — Firebase + Provider

```mermaid
flowchart LR
    subgraph Seg[Dia 6 — Provider]
        Change[ChangeNotifier] --> Consumer[Consumer]
        Consumer --> ToDo[ToDo de exemplo]
    end

    subgraph Ter[Dia 7 — Firebase Auth]
        Config[Config Firebase] --> Login[Login]
        Login --> Cadastro[Cadastro]
        Cadastro --> AuthApp[App com login real]
    end

    subgraph Qua[Dia 8 — Firestore]
        Model[Model + toMap] --> CRUD[CRUD completo]
        CRUD --> Stream[Stream em tempo real]
    end

    subgraph Qui[Dia 9 — Storage]
        Picker[Image Picker] --> Upload[Upload Storage]
        Upload --> Exibir[Exibir na tela]
    end

    subgraph Sex[Dia 10 — API]
        HTTP[http.get] --> JSON[jsonDecode]
        JSON --> ListaAPI[Lista de resultados]
    end

    Seg --> Ter --> Qua --> Qui --> Sex
```

**Marco da Semana 2:** 2 apps rodando — (1) ToDo com Provider (2) Login + CRUD Firestore. Cada membro entrega individualmente.

---

## Semana 3 — Mini Projetos Obrigatórios

### Mini Projeto 1 — ToDo List (2 dias)

```mermaid
flowchart LR
    LoginMP[Login Firebase] --> CRUDMP[CRUD Firestore]
    CRUDMP --> Concluir[Concluir tarefa]
    Concluir --> Filtrar[Filtrar pendentes]
    Filtrar --> ProviderMP[Provider + Loading + Erro]
```

### Mini Projeto 2 — CRUD + Upload (2 dias)

```mermaid
flowchart LR
    FormProd[Formulário produto] --> Foto[Upload foto]
    Foto --> ListaProd[StreamBuilder lista]
    ListaProd --> Editar[Editar / Excluir]
    Editar --> Confirmar[Confirmação exclusão]
```

**Marco da Semana 3:** 2 mini projetos completos no GitHub. Cada membro sabe fazer CRUD completo + Auth + upload.

---

## Semana 4 — Avançado + Integrações

```mermaid
flowchart LR
    subgraph Seg[Dia 1 — Navegação]
        Bottom[BottomNavigationBar] --> Stack[IndexedStack]
    end

    subgraph Ter[Dia 2 — Maps]
        FMap[flutter_map] --> Markers[Markers]
    end

    subgraph Qua[Dia 3 — OCR]
        MLKit[ML Kit] --> TextRecognition[Text recognition]
    end

    subgraph Qui[Dia 4 — Animações]
        Anim[AnimatedContainer] --> Hero[Hero]
    end

    subgraph Sex[Dia 5 — Revisão]
        Revisao[Revisão geral] --> Junta[Juntar tudo]
    end

    Seg --> Ter --> Qua --> Qui --> Sex
```

---

## Progresso da Trilha

```mermaid
gantt
    title Progresso Geral
    dateFormat  YYYY-MM-DD
    axisFormat  Semana %W

    section Capacitação
    Semana 1 — Dart + Flutter base     :done, p1, 2024-01-01, 7d
    Semana 2 — Firebase + Provider     :done, p2, after p1, 7d
    Semana 3 — Mini projetos           :done, p3, after p2, 7d
    Semana 4 — Tópicos avançados       :done, p4, after p3, 7d
```

---

## Meta Final dos Estudos

Cada membro deve conseguir, **sozinho**:

- Criar uma tela Flutter com formulário
- Navegar entre telas
- Salvar e ler dados no Firestore
- Implementar login com Firebase Auth
- Subir uma feature via branch + PR

> Se mais de 30% do time não conseguir, **repetir a semana** antes de avançar.
