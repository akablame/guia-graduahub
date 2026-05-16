# PLANO DE EXECUÇÃO GRADUAHUB — Sprints e Tarefas

**Duração total:** 10 semanas (50 dias úteis)  
**Equipe:** 4-6 pessoas (iniciantes em Flutter)  
**Meta:** MVP funcional apresentável na banca

---

## Índice

1. [Timeline Macro](#1-timeline-macro)
2. [Alocação da Equipe](#2-alocação-da-equipe)
3. [Sprint 0 — Fundação (Dias 1-5)](#3-sprint-0)
4. [Sprint 1 — Auth + Navegação (Dias 6-10)](#4-sprint-1)
5. [Sprint 2 — Dashboard (Dias 11-14)](#5-sprint-2)
6. [Sprint 3 — Rotina (Dias 15-22)](#6-sprint-3)
7. [Sprint 4 — Certificados (Dias 23-30)](#7-sprint-4)
8. [Sprint 5 — Pesquisa TCC (Dias 31-37)](#8-sprint-5)
9. [Sprint 6 — Radar Eventos (Dias 38-44)](#9-sprint-6)
10. [Sprint 7 — Polimento + Banca (Dias 45-50)](#10-sprint-7)
11. [Anexos](#11-anexos)

---

## 1) Timeline Macro

```
     SEMANA 1     SEMANA 2     SEMANA 3     SEMANA 4     SEMANA 5
    ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
    │  Sprint 0 │ │  Sprint 1 │ │  Sprint 2 │ │  Sprint 3 │ │  Sprint 3 │
    │ Fundação  │ │ Auth+Nav  │ │ Dashboard │ │  Rotina   │ │  Rotina   │
    └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘

     SEMANA 6     SEMANA 7     SEMANA 8     SEMANA 9     SEMANA 10
    ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
    │  Sprint 4 │ │  Sprint 5 │ │  Sprint 6 │ │  Sprint 7 │ │  Banca    │
    │ Certifica │ │ Pesquisa  │ │  Radar    │ │ Polimento │ │  Defesa   │
    └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘
```

---

## 2) Alocação da Equipe

### Papéis (para 4 pessoas)

| Membro | Papel Principal | Responsabilidades |
|---|---|---|
| **Pessoa A** | Líder Técnico + Auth | Configura Firebase, Provider, Auth, revisa PRs |
| **Pessoa B** | Dev Front (Telas) | Dashboard, Rotina, layout geral |
| **Pessoa C** | Dev Backend (Dados) | Firestore, Storage, modelos, serviços |
| **Pessoa D** | QA + Documentação | Testes, checklist, slides, evidências |

### Papéis (para 6 pessoas)

| Membro | Papel |
|---|---|
| Pessoa A | Líder Técnico |
| Pessoa B | Auth + Provider |
| Pessoa C | Dashboard + Rotina |
| Pessoa D | Certificados + Storage |
| Pessoa E | Pesquisa + API |
| Pessoa F | Radar + Mapa + QA |

---

## 3) Sprint 0 — Fundação (Dias 1-5)

**Objetivo:** Ambiente pronto e equipe consegue rodar `flutter run`

### Tarefas Detalhadas

| Dia | Tarefa | Responsável | Horas | Depende de |
|---|---|---|---|---|
| 1 | Instalar Flutter SDK + configurar PATH | A, B, C, D (todos) | 2h | — |
| 1 | Instalar Android Studio + SDK + emulador | A, B, C, D (todos) | 3h | — |
| 1 | `flutter doctor` tudo verde | A (verifica) | 0.5h | Instalação |
| 2 | Criar repositório GitHub (main + develop + feature/*) | A | 0.5h | — |
| 2 | `flutter create graduahub` + `flutter pub get` | A | 0.5h | Git repo |
| 2 | Executar `flutter run` no emulador | A, B, C, D | 1h | Flutter SDK |
| 2 | Criar projeto Firebase console (graduahub-dev) | A | 1h | — |
| 2 | Executar `flutterfire configure` | A | 1h | Firebase project |
| 2 | Adicionar dependências iniciais no pubspec.yaml | A | 0.5h | Projeto criado |
| 3 | Criar estrutura de pastas (core, data, features, providers) | A | 1h | — |
| 3 | Criar tema básico (cores, tipografia, espaçamentos) | B | 2h | — |
| 3 | Criar routes.dart com rotas nomeadas | A | 1h | — |
| 3 | Implementar main.dart com inicialização Firebase | A | 1h | Firebase config |
| 4 | Criar AuthService (Firebase Auth wrapper) | A | 2h | Firebase config |
| 4 | Criar FirestoreService (CRUD genérico) | C | 2h | Firebase config |
| 4 | Criar AuthProvider (ChangeNotifier) | A | 1.5h | AuthService |
| 4 | Criar LoginScreen + RegisterScreen esqueleto | B | 3h | Provider |
| 5 | Configurar regras de segurança Firestore (seção 8 do Guideline) | C | 1h | — |
| 5 | Testar fluxo login/cadastro no emulador | D | 2h | Telas prontas |
| 5 | Corrigir bugs encontrados | A, B | 2h | Testes |
| 5 | Subir PR de fundação + revisão | Todos | 1h | Tudo acima |

### Entregáveis da Sprint 0

- [ ] Repositório GitHub com branches main, develop, feature/*
- [ ] `flutter run` funcionando sem erros
- [ ] Firebase conectado (Auth, Firestore, Storage)
- [ ] Estrutura de pastas criada
- [ ] Tema global definido
- [ ] AuthService + FirestoreService + AuthProvider implementados
- [ ] LoginScreen e RegisterScreen criadas
- [ ] PR revisado e mergeado na develop

---

## 4) Sprint 1 — Auth + Navegação (Dias 6-10)

**Objetivo:** Usuário consegue criar conta, entrar e sair; telas principais navegáveis

### Tarefas Detalhadas

| Dia | Tarefa | Responsável | Horas | Depende de |
|---|---|---|---|---|
| 6 | Finalizar LoginScreen (form, validação, loading, erro) | B | 3h | Sprint 0 |
| 6 | Finalizar RegisterScreen (com nome + email + senha) | B | 3h | Sprint 0 |
| 6 | Implementar `user` collection no Firestore (criar ao registrar) | C | 2h | Sprint 0 |
| 7 | Implementar guarda de rota (se não logado → login) | A | 2h | AuthProvider |
| 7 | Criar BottomNavigationBar com 4 abas | B | 3h | — |
| 7 | Criar DashboardScreen (esqueleto com cards placeholder) | B | 2h | — |
| 7 | Criar ProfileScreen (exibir nome/email, botão sair) | B | 2h | — |
| 8 | Implementar fluxo de logout (limpar estado, voltar login) | A | 1h | AuthProvider |
| 8 | Testar sessão persistente (fechar e reabrir app) | D | 1h | Auth |
| 8 | Tratar erros de auth com mensagens amigáveis em PT-BR | B | 2h | — |
| 9 | Testar fluxo completo: cadastrar → logar → dashboard → sair | D | 2h | Tudo acima |
| 9 | Corrigir bugs (navegação, estado, persistência) | A, B | 3h | Testes |
| 9 | Melhorar validação de formulários (email válido, senha >= 6) | B | 1h | — |
| 10 | Revisão de código em grupo + ajustes finos | Todos | 2h | — |
| 10 | Subir PR + merge na develop | A | 1h | Revisão |

### Critério de Aceite

1. Usuário cria conta → vai para Dashboard
2. Usuário faz login com conta existente → vai para Dashboard
3. Usuário faz logout → volta para Login
4. Fechar e reabrir app → continua logado
5. Erro ao cadastrar com email duplicado → mensagem "Este email já está cadastrado"
6. Erro ao logar com senha errada → mensagem "Senha incorreta"

---

## 5) Sprint 2 — Dashboard (Dias 11-14)

**Objetivo:** Dashboard funcional com informações reais do usuário e atalhos

### Tarefas Detalhadas

| Dia | Tarefa | Responsável | Horas | Depende de |
|---|---|---|---|---|
| 11 | Refatorar DashboardScreen com GridView de ModuleCards | B | 3h | Sprint 1 |
| 11 | Criar ModuleCard widget (ícone, título, descrição, gradiente) | B | 2h | — |
| 11 | Configurar navegação dos cards para cada módulo | A | 1.5h | ModuleCard |
| 12 | Criar placeholder de cada módulo (tela "Em construção") | B | 2h | — |
| 12 | Criar DashboardProvider com dados agregados do Firestore | C | 3h | FirestoreService |
| 12 | Exibir nome do usuário no topo do Dashboard | B | 1h | AuthProvider |
| 13 | Exibir resumo de horas complementares no Dashboard | C | 3h | Certificate model |
| 13 | Exibir contagem de disciplinas cadastradas | C | 2h | Discipline model |
| 13 | Adicionar indicador de progresso visual (LinearProgressIndicator) | B | 1.5h | — |
| 14 | Testar Dashboard em 3 perfis diferentes | D | 2h | Tudo acima |
| 14 | Corrigir bugs de carregamento e atualização | A, B | 3h | Testes |
| 14 | Subir PR + merge | Todos | 1h | Revisão |

---

## 6) Sprint 3 — Rotina (Dias 15-22)

**Objetivo:** CRUD de disciplinas com cálculo de média e faltas (8 dias — módulo mais denso)

### Dia 15 — Modelo e Serviço

| Tarefa | Resp. | Horas |
|---|---|---|
| Criar Discipline model (nome, professor, carga horária, limite faltas, notas parciais) | C | 2h |
| Implementar toMap() e fromMap() do Discipline | C | 1h |
| Criar RoutineProvider (ChangeNotifier com lista de disciplinas) | A | 2.5h |
| Criar Firestore coleção `grades` com regras de segurança | C | 1h |

### Dia 16 — Tela de Lista de Disciplinas

| Tarefa | Resp. | Horas |
|---|---|---|
| Criar DisciplinesScreen com Consumer<RoutineProvider> | B | 3h |
| Exibir disciplinas em ListView com Card | B | 2h |
| Estado vazio: "Nenhuma disciplina cadastrada" com ilustração | B | 1h |

### Dia 17 — Formulário de Disciplina

| Tarefa | Resp. | Horas |
|---|---|---|
| Criar DisciplineFormScreen (nome, professor, carga horária, limite faltas) | B | 3h |
| Validar campos obrigatórios | B | 1h |
| Implementar salvar no Firestore via Provider | A | 1h |

### Dia 18 — Lançamento de Notas

| Tarefa | Resp. | Horas |
|---|---|---|
| Criar tela de lançamento de notas dentro da disciplina | B | 3h |
| Adicionar/remover notas parciais (dinâmico) | B | 2h |
| Salvar notas no Firestore | C | 1h |

### Dia 19 — Cálculo de Média + Previsão Final

| Tarefa | Resp. | Horas |
|---|---|---|
| Implementar cálculo de média ponderada no model | A | 1.5h |
| Implementar cálculo de nota necessária na final | A | 1.5h |
| Exibir resultados na tela da disciplina | B | 2h |
| Testar com cenários reais (aprovado, recuperação, reprovado) | D | 1h |

### Dia 20 — Controle de Faltas

| Tarefa | Resp. | Horas |
|---|---|---|
| Adicionar campo de faltas no formulário | B | 1h |
| Implementar cálculo de faltas restantes | A | 1h |
| Alerta visual se faltas > 75% do limite | B | 1.5h |
| Exibir barra de progresso de faltas | B | 1.5h |

### Dia 21 — Testes + Correções

| Tarefa | Resp. | Horas |
|---|---|---|
| Testar fluxo completo: criar disciplina → lançar notas → ver média | D | 3h |
| Testar edge cases: sem notas, nota 0, nota 10 | D | 1h |
| Testar exclusão de disciplina | D | 1h |
| Corrigir bugs encontrados | A, B, C | 3h |

### Dia 22 — Revisão + PR

| Tarefa | Resp. | Horas |
|---|---|---|
| Code review em grupo | Todos | 2h |
| Ajustes finos de UX | B | 2h |
| Subir PR + merge na develop | A | 1h |

### Critério de Aceite do Módulo Rotina

- [ ] Criar disciplina com nome, professor, carga horária
- [ ] Lançar notas parciais com pesos diferentes
- [ ] Ver média ponderada calculada automaticamente
- [ ] Ver quantos pontos precisa na final para passar
- [ ] Registrar faltas e ver saldo restante
- [ ] Excluir disciplina
- [ ] Dados persistem no Firestore (fechar e abrir app)

---

## 7) Sprint 4 — Certificados (Dias 23-30)

**Objetivo:** Upload de certificado (PDF/imagem) e controle de horas complementares

### Tarefas

| Dia | Tarefa | Resp. | Horas |
|---|---|---|---|
| 23 | Criar Certificate model (id, userId, storageUrl, validatedHours, category, uploadDate) | C | 1.5h |
| 23 | Criar CertificateProvider com métodos upload, list, delete | A | 3h |
| 23 | Criar StorageService com uploadFile() | C | 2h |
| 24 | Criar CertificatesScreen com ListView de certificados | B | 3h |
| 24 | Exibir cada certificado como Card (nome, horas, data) | B | 2h |
| 25 | Criar CertificateUploadScreen com FilePicker/ImagePicker | B | 3h |
| 25 | Implementar upload para Firebase Storage + salvamento Firestore | C | 3h |
| 26 | Adicionar formulário de validação manual (horas, categoria) | B | 2.5h |
| 26 | Implementar cálculo total de horas no DashboardProvider | C | 2h |
| 27 | Criar ProgressRing widget (gráfico circular de progresso) | B | 3h |
| 27 | Exibir ProgressRing no Dashboard com meta configurável | B | 2h |
| 28 | Testar upload de PDF e imagem | D | 2h |
| 28 | Testar cálculo de horas totais | D | 1h |
| 28 | Testar exclusão de certificado (diminuir total) | D | 1h |
| 29 | Corrigir bugs de upload (progresso, timeout, erro de rede) | A, C | 4h |
| 30 | Revisão + PR + merge | Todos | 3h |

### Critério de Aceite

- [ ] Selecionar PDF/imagem do celular
- [ ] Upload para Firebase Storage com indicador de progresso
- [ ] Salvar metadados no Firestore
- [ ] Ver certificado na lista
- [ ] Dashboard mostra total de horas com gráfico
- [ ] Excluir certificado remove do Storage e atualiza total

---

## 8) Sprint 5 — Pesquisa TCC (Dias 31-37)

**Objetivo:** Buscar artigos científicos na API OpenAlex

### Tarefas

| Dia | Tarefa | Resp. | Horas |
|---|---|---|---|
| 31 | Criar OpenAlexService com searchArticles(query) | C | 3h |
| 31 | Implementar decodificação do abstract invertido | A | 2h |
| 32 | Criar ResearchProvider com resultados, loading, erro | A | 2h |
| 32 | Criar ResearchScreen com campo de busca + botão | B | 2h |
| 33 | Criar ArticleCard widget (título, autores, resumo, link) | B | 3h |
| 33 | Exibir resultados em ListView | B | 1.5h |
| 34 | Implementar paginação (carregar mais resultados) | A, B | 3h |
| 34 | Tratar estado vazio "Nenhum resultado encontrado" | B | 1h |
| 35 | Testar busca com termos reais (português) | D | 2h |
| 35 | Testar edge cases: busca vazia, sem internet, caracteres especiais | D | 2h |
| 36 | Adicionar filtro por ano (opcional) | B | 2h |
| 36 | Corrigir bugs de parsing e exibição | A, C | 3h |
| 37 | Revisão + PR + merge | Todos | 3h |

### Critério de Aceite

- [ ] Digitar termo de busca → resultados aparecem
- [ ] Cada resultado mostra título, autores (até 3), resumo, ano
- [ ] Botão "Abrir artigo" leva ao link do DOI/publicação
- [ ] Loading enquanto busca
- [ ] Mensagem de erro se falhar
- [ ] Mensagem "Nenhum resultado" se vazio

---

## 9) Sprint 6 — Radar Eventos (Dias 38-44)

**Objetivo:** Lista + mapa de eventos acadêmicos salvos no Firestore

### Tarefas

| Dia | Tarefa | Resp. | Horas |
|---|---|---|---|
| 38 | Criar Event model (title, description, link, lat, lng, date) | C | 1.5h |
| 38 | Criar EventProvider com stream de eventos do Firestore | A | 2h |
| 38 | Popular Firestore com 5-10 eventos de exemplo (dados mockados) | C | 1h |
| 39 | Criar EventsScreen com TabBar: Lista | Mapa | B | 3h |
| 39 | Criar EventCard widget (título, data, link) | B | 2h |
| 40 | Implementar EventMapScreen com flutter_map + markers | B | 4h |
| 41 | Adicionar filtro por data (próximos 7 dias, 30 dias, todos) | A, B | 3h |
| 41 | Ao clicar no marker, mostrar info do evento (popup) | B | 2h |
| 42 | Testar mapa com markers, zoom, rotação | D | 2h |
| 42 | Testar filtros de data | D | 1h |
| 42 | Testar link de inscrição do evento | D | 1h |
| 43 | Adicionar botão "Abrir link" no card/popup | B | 1h |
| 43 | Corrigir bugs de layout e navegação | A, B | 3h |
| 44 | Revisão + PR + merge | Todos | 3h |

### Critério de Aceite

- [ ] Lista de eventos carregada do Firestore
- [ ] Mapa com pins nos locais dos eventos
- [ ] Clicar no pin → info do evento
- [ ] Filtro por data funcionando
- [ ] Link de inscrição abre navegador

---

## 10) Sprint 7 — Polimento + Banca (Dias 45-50)

**Objetivo:** App estável, testado e pronto para apresentação

### Dia 45 — Testes de Fluxo Completo

| Tarefa | Resp. | Horas |
|---|---|---|
| Rodar checklist completo de todas as funcionalidades | D | 4h |
| Listar bugs por severidade (crítico, alto, médio, baixo) | D | 1h |

### Dia 46 — Correção de Bugs Críticos

| Tarefa | Resp. | Horas |
|---|---|---|
| Corrigir bugs críticos (crash, fluxo quebrado) | A, B, C | 4h |
| Corrigir bugs altos (dados errados, navegação incorreta) | A, B, C | 2h |

### Dia 47 — UX e Design

| Tarefa | Resp. | Horas |
|---|---|---|
| Adicionar states de loading em todas as telas | B | 2h |
| Adicionar mensagens de erro amigáveis | B | 1.5h |
| Adicionar empty states (ilustração + texto) | B | 1.5h |
| Revisar contraste, fontes, espaçamento | B | 2h |

### Dia 48 — Preparação de Dados de Demo

| Tarefa | Resp. | Horas |
|---|---|---|
| Criar 3 contas de teste (email: aluno1@teste.com, etc.) | D | 0.5h |
| Popular dados de exemplo (disciplinas, notas, certificados) | D | 2h |
| Verificar todos os módulos com dados reais | D | 1.5h |

### Dia 49 — Documentação e Evidências

| Tarefa | Resp. | Horas |
|---|---|---|
| Gravar vídeo do fluxo completo (plano B para banca) | D | 1h |
| Criar slides de apresentação (problema, solução, arquitetura, demo) | D | 4h |
| Separar falas de cada membro | Todos | 1h |

### Dia 50 — Ensaio Geral

| Tarefa | Resp. | Horas |
|---|---|---|
| Ensaio 1: fluxo completo cronometrado | Todos | 1h |
| Ensaio 2: com perguntas da banca simuladas | Todos | 1h |
| Ensaio 3: última revisão + ajustes finos | Todos | 1h |
| Backup: vídeo do app funcionando em pendrive + nuvem | D | 0.5h |

---

## 11) Anexos

### A. Template de Daily

```
Nome: [Seu nome]
O que fiz ontem: [resumo]
O que vou fazer hoje: [tarefa específica]
Bloqueios: [algo impedindo?]
```

### B. Template de PR

```
## O que foi feito
[descrição das mudanças]

## Prints / Vídeo
[link]

## Checklist
- [ ] Funciona no emulador
- [ ] Sem erro de compilação
- [ ] Fluxo testado manualmente
- [ ] Código segue padrões do projeto

## Revisores
@colega1 @colega2
```

### C. Critério de Priorização (se faltar tempo)

```
1º Auth + Dashboard       ← obrigatório, sem isso não tem app
2º Rotina                 ← obrigatório, módulo mais útil para banca
3º Certificados v1        ← obrigatório, diferencial do projeto
4º Pesquisa TCC           ← importante, mostra integração com API
5º Radar v1               ← desejável, legal mas complexo
6º OCR, Scraper, etc.     ← bônus, só se sobrar tempo
```

### D. Ferramentas Recomendadas

| Ferramenta | Para quê |
|---|---|
| GitHub Projects | Board de tarefas (Kanban) |
| Trello | Alternativa simples ao GitHub Projects |
| Discord | Daily + dúvidas (canais de texto/voz) |
| Google Drive | Documentos compartilhados |
| Canva | Slides da apresentação |
| OBS Studio | Gravação do vídeo backup |
| Figma | Wireframes (se quiserem) |
