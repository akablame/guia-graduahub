# Roadmap — Plano de Estudos

```
TRILHA DE APRENDIZADO: DO ZERO AO FLUTTER FUNCIONAL
─────────────────────────────────────────────────────
```

## ═══════════ SEMANA 1 — DART + FLUTTER BASE ═══════════

```
Nível atual: ❌ nunca programou / sabe lógica básica
Meta:        ✔ criar app Flutter com 3 telas navegáveis
```

```
    SEG          TER          QUA          QUI          SEX          SÁB
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│  Dart I   │ │  Dart II  │ │ Flutter I │ │ Flutter  │ │  Listas  │ │ Reforço  │
│ variáveis │ │  classes  │ │ primeiro │ │  II      │ │   +      │ │ +        │
│ funções   │ │  listas   │ │  app     │ │ navegação│ │ Layout   │ │ Revisão  │
│ null-safe │ │  mapas    │ │ widgets  │ │ forms    │ │ Grids    │ │          │
└────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘
     │            │            │            │            │            │
     ▼            ▼            ▼            ▼            ▼            ▼
  10 ex     Classes      App roda    3 telas     Lista de      Tudo
  resolv    Aluno com    no          + forms     20 cards      funcionando
  em Dart   media       emulador    validados   customizados  sem duvidas
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 MARCO: App com 3 telas navegáveis + formulário com validação rodando   │
│            no emulador Android.                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════ SEMANA 2 — FIREBASE + PROVIDER ═══════════

```
Nível atual: ✔ faz telas estáticas em Flutter
Meta:        ✔ app com login real + dados salvos na nuvem
```

```
    SEG          TER          QUA          QUI          SEX          SÁB
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│ Provider  │ │ Firebase │ │ Firestore│ │ Firebase │ │  HTTP +  │ │ Reforço  │
│          │ │   Auth   │ │   CRUD   │ │ Storage  │ │ OpenAlex │ │ +        │
│ Change   │ │ login/   │ │ models   │ │ upload   │ │   API    │ │ Revisão  │
│ Notifier │ │ cadastro │ │ streams  │ │ image    │ │  JSON    │ │          │
│ Consumer │ │          │ │          │ │ picker   │ │          │ │          │
└────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘
     │            │            │            │            │            │
     ▼            ▼            ▼            ▼            ▼            ▼
   ToDo de   App com     Lista em    Upload     Busca      Domínio
   exemplo   login       tempo       de foto    artigos    de tudo
   rodando   funcional   real        exibindo   OpenAlex   estudado
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 MARCO: 2 apps rodando (1) ToDo com Provider (2) Login + CRUD          │
│            Firestore. Cada membro entrega individualmente.                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════ SEMANA 3 — MINI PROJETOS OBRIGATÓRIOS ═══════════

```
Nível atual: ✔ sabe conectar Flutter + Firebase
Meta:        ✔ entregar 2 mini projetos completos (em dupla)
```

```
    SEG          TER          QUA          QUI          SEX          SÁB
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│  Mini    │ │  Mini    │ │  Mini    │ │  Mini    │ │ Revisão  │ │ Entrega  │
│ Projeto  │ │ Projeto  │ │ Projeto  │ │ Projeto  │ │   +      │ │   dos    │
│  1 dia 1 │ │  1 dia 2 │ │  2 dia 1 │ │  2 dia 2 │ │ Correções│ │ projetos │
└────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘
     │            │            │            │            │            │
     ▼            ▼            ▼            ▼            ▼            ▼
   ToDo      ToDo       CRUD       CRUD +     PR     Ambos
   completo  com        produtos   upload     aberto   mergeados
   + login   Firestore  completo   de foto    + review na develop
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 MARCO: 2 mini projetos completos no GitHub. Cada membro sabe fazer    │
│            CRUD completo + Auth + upload de arquivo. PR aprovado.          │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Mini Projeto 1 — ToDo List**
- Login Firebase Auth
- CRUD no Firestore
- Marcar concluída
- Filtrar: todas/pendentes/concluídas
- Provider + loading + erro + vazio

**Mini Projeto 2 — CRUD + Upload**
- Cadastro de produto com foto
- Upload para Firebase Storage
- Lista com StreamBuilder
- Editar/Excluir com confirmação

---

## ═══════════ SEMANA 4 — AVANÇADO + INTEGRAÇÕES ═══════════

```
Nível atual: ✔ mini projetos completos
Meta:        ✔ domínio de tópicos avançados para o GraduaHUB
```

```
    SEG           TER            QUA            QUI            SEX
┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐
│ Navegação  │ │  Maps      │ │   OCR      │ │ Animações  │ │  Revisão   │
│ avançada   │ │            │ │            │ │            │ │   Geral    │
│ BottomNav  │ │ flutter_map│ │ ML Kit     │ │ Animated   │ │            │
│ Indexed    │ │ markers    │ │ text       │ │ Container  │ │ Juntar     │
│ Stack      │ │ geolocator │ │ recognition│ │ Hero       │ │ tudo       │
└────┬───────┘ └────┬───────┘ └────┬───────┘ └────┬───────┘ └────┬───────┘
     │              │              │              │              │
     ▼              ▼              ▼              ▼              ▼
   4 abas       Mapa com      OCR lendo      Transições     Pronto
   com        pins reais     texto de       suaves         para
   telas                     imagem         entre telas    o projeto
   independentes
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🏁 MARCO FINAL DOS ESTUDOS: Time apto a desenvolver o GraduaHUB.         │
│  Cada membro consegue:                                                     │
│    • Criar tela Flutter com formulário                                     │
│    • Navegar entre telas                                                   │
│    • Salvar/ler dados no Firestore                                         │
│    • Implementar login com Firebase Auth                                   │
│    • Subir feature via branch + PR                                         │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## ═══════════ SEMANAS 5-8 — ESTUDO PARALELO ÀS SPRINTS ═══════════

```
Nível atual: ✔ base completa para desenvolver
Estratégia: estudar APENAS o necessário para a próxima tarefa
```

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│  SPRINT 1 (Auth + Nav)     → Provider, Firebase Auth, Navigator             │
│  SPRINT 2 (Dashboard)      → GridView, Cards, StreamBuilder                │
│  SPRINT 3 (Rotina)         → Forms, cálculos, validação                    │
│  SPRINT 4 (Certificados)   → ImagePicker, Storage, File                    │
│  SPRINT 5 (Pesquisa)       → HTTP, JSON, ListView                          │
│  SPRINT 6 (Radar)          → flutter_map, geolocator, markers              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📊 SUMÁRIO DE PROGRESSO

```
SEMANA 1 ─████████░░░░░░░░░░ 40%  Dart + Flutter base
SEMANA 2 ─████████████░░░░░░ 60%  Firebase + Provider
SEMANA 3 ─█████████████████░ 90%  Mini projetos
SEMANA 4 ─██████████████████ 100% Tópicos avançados

         ├───────────┬───────────┬───────────┬───────────┤
        Semana 1    Semana 2    Semana 3    Semana 4

  ✔ = pronto para desenvolver o GraduaHUB
```

---

## ⚠️ REGRA DE OURO

```
Se mais de 30% do time não conseguir fazer um exercício:
    → REPETIR o dia seguinte com mais prática
    → NÃO AVANÇAR sem base sólida

Cada membro PRECISA conseguir fazer tudo sozinho:
    ❌ "Fulano fez a parte dele, eu só copiei"
    ✔ "Eu fiz minha tela do zero e entendi cada linha"
```
