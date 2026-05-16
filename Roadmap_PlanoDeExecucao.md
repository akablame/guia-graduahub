# Roadmap — Plano de Execução

```
LINHA DO TEMPO: 10 SEMANAS → MVP NA BANCA
───────────────────────────────────────────
```

## ════════════════ VISÃO GERAL ════════════════

```
    Sprint 0     Sprint 1     Sprint 2     Sprint 3     Sprint 4
   Semana 1     Semana 2     Semana 3     Semana 4     Semana 5
 ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
 │ Fundação  │ │ Auth +   │ │ Dashboard │ │  Rotina  │ │  Rotina  │
 │          │ │  Nav     │ │           │ │          │ │ (cont.)  │
 └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘
      │            │            │            │            │
      ▼            ▼            ▼            ▼            ▼
  Firebase     Login/      Cards       Disciplinas   Cálculo
  pronto       Cadastro    módulos     +             notas/
  + App roda   funcional   + resumo    formulário    faltas

    Sprint 5     Sprint 6     Sprint 7     Sprint 8
   Semana 6     Semana 7     Semana 8     Semanas 9-10
 ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐
 │ Certifica │ │ Pesquisa  │ │  Radar   │ │  Qualidade   │
 │  dos     │ │   TCC    │ │  Eventos │ │  + Banca     │
 └────┬─────┘ └────┬─────┘ └────┬─────┘ └──────┬───────┘
      │            │            │              │
      ▼            ▼            ▼              ▼
  Upload      OpenAlex     Mapa +        Testes +
  +           +            Lista         Slides +
  Progresso   ArticleCard  eventos       Ensaio
```

---

## ══════════════ DIAS 1-5 — SPRINT 0: FUNDAÇÃO ══════════════

```
OBJETIVO: Ambiente pronto, `flutter run` funciona, Firebase conectado

 Responsável       Dia 1           Dia 2          Dia 3          Dia 4          Dia 5
───────────────────────────────────────────────────────────────────────────────────────────────
 Pessoa A (Líder)  │               │              │              │              │
                    Instalar       Criar repo     Criar          Implementar   Revisar PR
                    Flutter SDK    GitHub +       pastas +       AuthService    + mergear
                    + configurar   flutter create main.dart +    +
                    PATH           + Firebase     routes.dart    AuthProvider
                                   + pubspec

 Pessoa B (Front)   Instalar       flutter run    Criar tema    LoginScreen   Ajudar
                    Android        no emulador    (cores,        +             correções
                    Studio + SDK                   fontes)       RegisterScreen

 Pessoa C (Dados)   Instalar       flutterfire    ─              Firestore     Regras
                    Flutter        configure                      Service       Firestore
                                                                               + testes

 Pessoa D (QA/Doc)  Instalar tudo  Testar         Organizar      Testar        Checklist
                                  flutter run     docs + board   login/cad     + PR
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA: flutter run ✅ | Firebase conectado ✅ | PR #1 mergeado ✅   │
│  Board criado ✅ | Regras de branch configuradas ✅                         │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ══════════════ DIAS 6-10 — SPRINT 1: AUTH + NAV ══════════════

```
  DIA 6         DIA 7          DIA 8          DIA 9          DIA 10
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│ Finalizar│ │ Guarda   │ │ Logout   │ │ Testes   │ │ Review   │
│ Login +  │ │ de rota  │ │ completo │ │ fluxo    │ │ +        │
│ Register │ │ Bottom   │ │ Persis-  │ │ completo │ │ PR #2    │
│ Telas    │ │ NavBar   │ │ tência   │ │ +        │ │ + merge  │
└──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA: Login/Cadastro ✅ | Sessão persistente ✅ |                   │
│  Navegação entre telas ✅ | Mensagens de erro PT ✅                         │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ══════════════ DIAS 11-14 — SPRINT 2: DASHBOARD ══════════════

```
  DIA 11        DIA 12         DIA 13          DIA 14
┌──────────┐ ┌──────────┐ ┌────────────┐ ┌────────────┐
│ GridView │ │ Dashboard│ │ Resumo     │ │ Testes     │
│ Module   │ │ Provider │ │ horas +    │ │ +          │
│ Card     │ │ +        │ │ contagem   │ │ PR #3      │
│ widget   │ │ placehold│ │ disciplinas│ │ + merge    │
└──────────┘ └──────────┘ └────────────┘ └────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA: Dashboard com cards dos módulos ✅ |                           │
│  Resumo de horas complementares ✅ | Contagem de disciplinas ✅             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ════════════════ DIAS 15-22 — SPRINT 3: ROTINA ════════════════

```
  DIAS 15-16     DIAS 17-18      DIAS 19-20      DIAS 21-22
┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐
│ Model +    │ │ Lançar     │ │ Cálculo    │ │ Testes +   │
│ Provider + │ │ notas +    │ │ média +    │ │ Correções  │
│ Tela lista │ │ formulário │ │ previsão   │ │ + PR #4    │
│ disciplinas│ │ faltas     │ │ final      │ │ + merge    │
└────────────┘ └────────────┘ └────────────┘ └────────────┘

    │              │              │              │
    ▼              ▼              ▼              ▼
  Disciplina    Notas         "Precisa de     Fluxo completo
  salva no      lançadas       X na final     testado com
  Firestore     com peso       para passar"   dados reais
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA: CRUD disciplinas ✅ | Cálculo média ✅ |                      │
│  Previsão nota final ✅ | Controle faltas ✅ | Alertas visuais ✅           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════════ DIAS 23-30 — SPRINT 4: CERTIFICADOS ═══════════════

```
  DIAS 23-24      DIAS 25-26       DIAS 27-28       DIAS 29-30
┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐
│ Model +    │ │ Upload     │ │ Progress   │ │ Testes +   │
│ Provider + │ │ Storage +  │ │ Ring +     │ │ Correções  │
│ Tela lista │ │ Firestore  │ │ Total no   │ │ + PR #5    │
│ certificad │ │ Validação  │ │ Dashboard  │ │ + merge    │
└────────────┘ └────────────┘ └────────────┘ └────────────┘

    │              │              │              │
    ▼              ▼              ▼              ▼
  Lista         PDF salvo      Gráfico       Upload +
  de           no Storage     mostrando     exclusão
  certificados + Firestore    progresso     funcionando
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA: Upload PDF/imagem ✅ | Lista de certificados ✅ |             │
│  Dashboard com progresso visual ✅ | Exclusão funcional ✅                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════════ DIAS 31-37 — SPRINT 5: PESQUISA TCC ═══════════════

```
  DIAS 31-32      DIAS 33-34       DIAS 35-37
┌────────────┐ ┌────────────┐ ┌──────────────┐
│ OpenAlex   │ │ ArticleCard│ │ Paginação    │
│ Service +  │ │ + ListView │ │ + Filtro ano │
│ Provider   │ │ + Estado   │ │ + Testes     │
│ Decodificar│ │ vazio/erro │ │ + PR #6      │
│ abstract   │ │            │ │ + merge      │
└────────────┘ └────────────┘ └──────────────┘

    │              │              │
    ▼              ▼              ▼
  API           Resultados      Busca com
  respondendo   exibidos        termos reais
  com dados     em cards        funcionando
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA: Busca OpenAlex ✅ | Cards com título/autor/resumo/ano/link ✅│
│  Loading + erro + vazio ✅ | Paginação funcionando ✅                      │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════════ DIAS 38-44 — SPRINT 6: RADAR EVENTOS ═══════════════

```
  DIAS 38-39      DIAS 40-41       DIAS 42-44
┌────────────┐ ┌────────────┐ ┌──────────────┐
│ Event      │ │ Mapa com   │ │ Popup info   │
│ model +    │ │ flutter_map│ │ + Filtro     │
│ Provider + │ │ + markers  │ │ + Link       │
│ Lista +    │ │ + zoom     │ │ + Testes     │
│ dados mock │ │            │ │ + PR #7      │
└────────────┘ └────────────┘ └──────────────┘

    │              │              │
    ▼              ▼              ▼
  Eventos        Mapa com       Clicar no
  no             pins nas       pin mostra
  Firestore      coordenadas    info do evento
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA: Lista de eventos ✅ | Mapa com markers ✅ |                    │
│  Popup com info ✅ | Filtro por data ✅ | Link de inscrição ✅              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ════════════════ DIAS 45-50 — SPRINT 7: QUALIDADE + BANCA ════════════════

```
  DIAS 45-46        DIAS 47-48         DIAS 49-50
┌────────────────┐ ┌────────────────┐ ┌──────────────────┐
│ Testes fluxo   │ │ Dados demo     │ │ Ensaio 1, 2, 3   │
│ completo       │ │ Contas teste   │ │ Slides prontos   │
│ Corrigir bugs  │ │ Vídeo backup   │ │ Backup em nuvem  │
│ críticos       │ │ Slides         │ │ Tudo verificado  │
└────────────────┘ └────────────────┘ └──────────────────┘

    │                  │                  │
    ▼                  ▼                  ▼
  App sem           Dados reais         Time pronto
  crashes           para mostrar        para banca
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 ENTREGA FINAL:                                                        │
│                                                                             │
│  📱 App: Auth ✅ Dashboard ✅ Rotina ✅ Certificados ✅                     │
│          Pesquisa ✅ Radar ✅                                               │
│                                                                             │
│  📋 Documentação: Prints ✅ Vídeo backup ✅ Slides ✅                       │
│                                                                             │
│  🎤 Time: 3 ensaios realizados ✅ Falas definidas ✅                       │
│          Perguntas da banca preparadas ✅                                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ⚠️ PLANO DE CONTINGÊNCIA (SE FALTAR TEMPO)

```
Prioridade absoluta (não pular):
  1º Auth + Dashboard     ← base de tudo
  2º Rotina               ← módulo mais útil
  3º Certificados v1      ← diferencial do projeto

Pode reduzir escopo:
  4º Pesquisa TCC         ← versão sem paginação
  5º Radar v1             ← só lista, sem mapa

Corta por último:
  6º OCR automático       ← versão manual já funciona
  7º Scraper Python       ← dados mockados resolvem
```
