# GUIA DE APRESENTAÇÃO — Banca GraduaHUB

**Versão:** 1.0  
**Público:** Equipe SENAI (preparação para a banca)  
**Objetivo:** Roteiro completo para a apresentação final — do roteiro às perguntas da banca.

---

## Índice

1. [Estrutura da Apresentação](#1-estrutura-da-apresentação)
2. [Roteiro de 7 Minutos](#2-roteiro-de-7-minutos)
3. [Divisão de Falas (4 pessoas)](#3-divisão-de-falas-4-pessoas)
4. [Checklist de Preparação](#4-checklist-de-preparação)
5. [Perguntas Que a Banca Pode Fazer](#5-perguntas-que-a-banca-pode-fazer)
6. [Plano B (se algo der errado)](#6-plano-b-se-algo-der-errado)
7. [Dicas de Apresentação](#7-dicas-de-apresentação)

---

## 1) Estrutura da Apresentação

| Parte | Duração | Quem |
|---|---|---|
| **1. Abertura** — o problema | 1 min | Pessoa A |
| **2. Solução** — o GraduaHUB | 1 min | Pessoa B |
| **3. Demo** — app funcionando | 3 min | Pessoa C |
| **4. Arquitetura** — como foi feito | 1 min | Pessoa D |
| **5. Desafios** — o que aprendemos | 0.5 min | Pessoa A |
| **6. Encerramento** | 0.5 min | Todos |

**Tempo total:** ~7 minutos (ideal: 5-8 min)

---

## 2) Roteiro de 7 Minutos

### Parte 1 — Abertura (1 min) — Pessoa A

> "Bom dia/boa tarde! Somos a equipe GraduaHUB. Nosso projeto nasceu de um problema real: **os alunos do ensino superior têm dificuldade em centralizar a vida acadêmica**. São vários apps, planilhas, prazos perdidos... A gente queria resolver isso em um único lugar."

**Slides:** Problema → foto de aluno confuso com vários apps

### Parte 2 — Solução (1 min) — Pessoa B

> "O GraduaHUB é um hub acadêmico com 4 módulos principais:
> - **Rotina:** controle de disciplinas, notas e faltas
> - **Certificados:** upload e validação de horas complementares
> - **Pesquisa TCC:** busca de artigos científicos na OpenAlex
> - **Radar:** mapa de eventos acadêmicos
> 
> Tudo isso em um app Flutter, multiplataforma."

**Slides:** Logo + 4 cards dos módulos

### Parte 3 — Demo (3 min) — Pessoa C

> "Vou mostrar o app funcionando. Criei uma conta de teste..."

**Roteiro da demo:**
1. Abrir app → mostrar login
2. Entrar com conta de teste (já preparada)
3. Navegar pelo Dashboard
4. Mostrar **Rotina:** disciplina com notas e faltas
5. Mostrar **Certificados:** upload de PDF
6. Mostrar **Pesquisa:** buscar "inteligência artificial"
7. Mostrar **Radar:** lista e mapa de eventos

> **Importante:** Treine a demo pelo menos 5x. Cada clique tem que ser natural.

### Parte 4 — Arquitetura (1 min) — Pessoa D

> "Por trás dos panos, usamos:
> - **Flutter** para o app (uma base de código para Android, iOS e Web)
> - **Firebase** para login, banco de dados e armazenamento
> - **Provider** para gerenciar o estado do app
> - **OpenAlex API** para artigos científicos
> - **OpenStreetMap** para o mapa de eventos
> 
> Tudo conectado de forma segura com regras do Firestore."

**Slides:** Diagrama de arquitetura (Flutter ⇄ Firebase ⇄ APIs)

### Parte 5 — Desafios (30s) — Pessoa A

> "O maior desafio foi aprender Flutter do zero em 10 semanas. A gente organizou em sprints, com daily meetings e revisões de código. No final, entregamos um MVP funcional e testado."

**Slides:** Timeline do projeto (sprints)

### Parte 6 — Encerramento (30s) — Todos

> **Pessoa A:** "Obrigado pela atenção!"
> **Todos:** "Estamos prontos para as perguntas!"

---

## 3) Divisão de Falas (4 pessoas)

| Membro | Fala Principal | Perguntas que RESPONDE |
|---|---|---|
| **Pessoa A** | Abertura + Desafios | Arquitetura geral, Firebase, decisões técnicas |
| **Pessoa B** | Solução + Módulos | UI/UX, Widgets, Navegação, Provider |
| **Pessoa C** | Demo + Funcionalidades | Rotina, Certificados, Formulários |
| **Pessoa D** | Arquitetura + Stack | API OpenAlex, Mapa, Testes, Git |

### Plano de perguntas que cada um deve saber:

**Pessoa A (Líder Técnico):**
- Por que escolheram Flutter?
- Como funciona a autenticação?
- Como protegeram os dados do usuário?
- Quais as regras de segurança do Firestore?

**Pessoa B (Front):**
- Como funciona o Provider?
- Quais widgets mais usaram?
- Como lidaram com loading e erro?
- Como é a estrutura de navegação?

**Pessoa C (Dados):**
- Como funciona o cálculo de média?
- Como é o fluxo de upload de certificado?
- Como validam as horas complementares?
- Como tratam dados offline?

**Pessoa D (API/Testes):**
- Como funciona a integração com OpenAlex?
- Como fizeram o mapa?
- Que testes implementaram?
- Como foi o workflow do Git?

---

## 4) Checklist de Preparação

### 1 Semana Antes
- [ ] App 100% funcional nos cenários principais
- [ ] Contas de teste criadas com dados reais
- [ ] Slides finalizados
- [ ] Roteiro de falas distribuído

### 3 Dias Antes
- [ ] 1º ensaio completo (cronometrado)
- [ ] Corrigir falhas do roteiro
- [ ] Testar app no projetor/monitor externo

### 1 Dia Antes
- [ ] 2º ensaio completo
- [ ] Vídeo de backup do app gravado
- [ ] Slides exportados em PDF (backup)
- [ ] APK do app salvo em pendrive + nuvem

### Dia da Banca
- [ ] 3º ensaio (manhã)
- [ ] Notebook carregado
- [ ] App testado 5 min antes
- [ ] Projetor funcionando
- [ ] Respiro fundo 😊

---

## 5) Perguntas Que a Banca Pode Fazer

### Técnicas

| Pergunta | O que esperam | Resposta esperada |
|---|---|---|
| "Por que Flutter e não React Native?" | Conhecimento de mercado | "Flutter tem performance nativa, hot reload, e uma base de código para Android, iOS e Web. O React Native também é bom, mas escolhemos Flutter pela integração com Firebase e pela curva de aprendizado." |
| "Como vocês garantiram a segurança dos dados?" | Regras Firestore | "Configuramos regras no Firestore para que cada usuário só acesse os próprios dados. Usuários só podem ler/escrever documentos onde o `userId` bate com o `auth.uid`." |
| "E se o usuário estiver offline?" | Tratamento de erro | "No momento, o app precisa de internet para funcionar. Mas planejamos adicionar cache offline usando o Firestore offline persistence." |
| "Como testaram o app?" | Qualidade | "Fizemos testes unitários nos modelos e serviços, testes de widget nas telas principais, e testes manuais de fluxo completo antes de cada PR." |

### Gerenciais

| Pergunta | Resposta |
|---|---|
| "Como dividiram as tarefas?" | "Usamos sprints semanais com daily meetings de 15 min. Cada pessoa tinha uma função clara e as tarefas eram distribuídas no GitHub Projects." |
| "Qual foi o maior desafio?" | "Aprender Flutter do zero. Mas seguimos um plano de estudos de 4 semanas antes de começar o projeto, o que ajudou muito." |
| "O que mudariam se fosse começar de novo?" | "Começaríamos os testes mais cedo e faríamos mais integrações parciais ao invés de tudo no final." |

### Para Cada Membro

Prepare 3 perguntas específicas para a área de cada um (veja seção 3 acima).

---

## 6) Plano B (se algo der errado)

| Problema | Solução |
|---|---|
| **App crashou** | "Deixa eu reiniciar... (5s)... Enquanto isso, explico como o módulo funciona." |
| **Internet caiu** | Usar vídeo de backup do app |
| **Projetor não funciona** | Slides no notebook + descrever o app verbalmente |
| **Notebook travou** | Ter APK no celular + pendrive com slides |
| **Esqueci a senha** | Contas de teste anotadas no slide |
| **Banca perguntou algo que não sei** | "Essa é uma boa pergunta. O que posso dizer é que... (responder o que sabe). O (colega) pode complementar se quiser." |

> **Kit de emergência:** Pendrive com APK + slides + vídeo. Cabo HDMI. Carregador. Água.

---

## 7) Dicas de Apresentação

### Durante a fala

- **Não leia os slides** — eles são seu apoio, não seu roteiro
- **Olhe para a banca** — não para o chão ou para a tela
- **Fale pausadamente** — nervosismo acelera a fala
- **Mostre entusiasmo** — você trabalhou duro nisso, tenha orgulho!
- **Use as mãos** — gestos naturais ajudam a comunicar

### Na demo

- **Dados reais** — nada de "hipoteticamente..."
- **Comece com o app já logado** — evite risco de falha no login
- **Tenha um roteiro de clique** — saiba exatamente o que clicar
- **Se travar, não entre em pânico** — "enquanto carrega, explico que..."

### Após a apresentação

- **Agradeça** sempre
- **Aceite críticas** com positividade — "ótimo ponto, vamos considerar"
- **Não discuta** com a banca
- **Saia com confiança** — vocês fizeram o melhor que puderam

---

> **Regra de ouro da apresentação:** A banca quer que você vá bem. Eles estão do seu lado. Mostre o que aprendeu, não o que você não sabe.
