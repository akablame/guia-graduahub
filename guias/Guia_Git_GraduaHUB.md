# GUIA GIT & GITHUB — GraduaHUB

**Versão:** 1.0  
**Público:** Equipe SENAI (iniciantes em Git)  
**Objetivo:** Fluxo de trabalho com Git/GitHub para o projeto — sem medo de errar.

---

## Índice

1. [Conceitos Básicos](#1-conceitos-básicos)
2. [Estrutura de Branches](#2-estrutura-de-branches)
3. [Fluxo do Dia a Dia](#3-fluxo-do-dia-a-dia)
4. [Fazendo um Pull Request](#4-fazendo-um-pull-request)
5. [Revisão de Código (Code Review)](#5-revisão-de-código-code-review)
6. [Resolvendo Conflitos](#6-resolvendo-conflitos)
7. [Boas Práticas de Commit](#7-boas-práticas-de-commit)
8. [Comandos Úteis](#8-comandos-úteis)
9. [Checklist Antes do PR](#9-checklist-antes-do-pr)

---

## 1) Conceitos Básicos

```
Git = sistema de versionamento (controle de histórico)
GitHub = nuvem onde o código fica (repositório remoto)
Repository (repo) = pasta do projeto no GitHub
Branch = ramificação do código (linha do tempo paralela)
Commit = checkpoint salvo (como um "save point" de jogo)
Pull Request (PR) = pedido para juntar seu código ao principal
Merge = juntar branches
```

---

## 2) Estrutura de Branches

```
main
  └── develop
        ├── feature/auth
        ├── feature/dashboard
        ├── feature/rotina
        ├── feature/certificados
        ├── feature/pesquisa
        └── feature/radar
```

| Branch | Finalidade |
|---|---|
| **main** | Código final, só entra depois de testado e revisado |
| **develop** | Branch de integração, onde as features são juntadas |
| **feature/nome** | Sua branch de trabalho (uma por funcionalidade) |

### Regras

1. **Nunca** commitar direto na `main` ou `develop`
2. Sempre criar uma `feature/nomedafuncionalidade`
3. PR sempre apontando para `develop`
4. `develop` → `main` só na banca (ou em marcos importantes)

---

## 3) Fluxo do Dia a Dia

### Início do dia

```bash
# 1. Atualizar sua branch develop
git checkout develop
git pull origin develop

# 2. Criar branch para sua tarefa
git checkout -b feature/nome-da-tarefa
```

### Durante o desenvolvimento

```bash
# Ver o que mudou
git status

# Adicionar arquivos específicos
git add lib/features/routine/disciplines_screen.dart

# OU adicionar tudo de uma vez
git add .

# Commitar
git commit -m "Adiciona tela de listagem de disciplinas"

# Enviar para o GitHub
git push origin feature/nome-da-tarefa
```

### Fim da tarefa (PR)

```bash
# 1. Atualizar sua branch com a develop
git checkout develop
git pull origin develop
git checkout feature/nome-da-tarefa
git merge develop

# 2. Resolver conflitos se houver (veja seção 6)

# 3. Push final
git push origin feature/nome-da-tarefa

# 4. Abrir Pull Request no GitHub
```

---

## 4) Fazendo um Pull Request

### Pelo site do GitHub

1. Acessar `github.com/akablame/guia-graduahub`
2. Clicar em **Pull Requests > New Pull Request**
3. Base: `develop` → Compare: `feature/nome-da-tarefa`
4. Preencher template:

```markdown
## O que foi feito
Descreva de forma simples o que você implementou.

## Prints / Vídeo
Cole evidências do funcionamento.

## Checklist
- [ ] Funciona no emulador
- [ ] Sem erro de compilação
- [ ] Testei manualmente o fluxo
- [ ] Código segue padrões do projeto

## Revisores
@colega1 @colega2
```

5. Clicar em **Create Pull Request**
6. Marcar pelo menos 2 colegas como revisores

---

## 5) Revisão de Código (Code Review)

### O que olhar ao revisar

| Item | O que verificar |
|---|---|
| **Lógica** | O código faz o que deveria? Tem erro óbvio? |
| **Padrões** | Segue a estrutura do projeto? Nomes corretos? |
| **Loading/Erro** | Tem tratamento de loading e erro? |
| **Hard coded** | Tem string solta no código? Deveria ser constante? |
| **Segurança** | Dados sensíveis expostos? Regras Firestore? |

### Como revisar

```bash
# 1. Baixar o PR localmente
git checkout develop
git pull origin develop
git checkout -b review/nome-da-feature
git pull origin feature/nome-da-tarefa

# 2. Testar
flutter run

# 3. Aprovar ou pedir mudanças no GitHub
```

### Etiqueta do Code Review

- Seja **respeitoso**: "O que acha de...?" em vez de "Está errado"
- Seja **específico**: aponte a linha e sugira uma solução
- **Explique o porquê**: não só "mude isso", mas "mude isso porque..."
- **Aprove rápido** quando estiver bom: não atrase o coleguinha

---

## 6) Resolvendo Conflitos

Conflitos acontecem quando duas pessoas mexem no mesmo arquivo.

### Pelo terminal

```bash
# Quando der conflito no merge:
git merge develop
# → CONFLICT: lib/features/routine/disciplines_screen.dart

# Abrir o arquivo e procurar por:
<<<<<<< HEAD
seu código
=======
código da develop
>>>>>>> develop

# Escolher qual versão manter (ou juntar as duas)
# Depois de resolver:
git add arquivo_resolvido.dart
git commit -m "Resolve conflito em disciplines_screen"
```

### Pelo VSCode

1. Abrir arquivo com conflito
2. Clicar em **Accept Current Change** (seu) / **Accept Incoming Change** (develop) / **Accept Both Changes**
3. Salvar, `git add` e `git commit`

> **Dica:** Para evitar conflitos, sempre dê `git pull origin develop` antes de começar a codar.

---

## 7) Boas Práticas de Commit

### Mensagens de commit

```
Tipo: mensagem curta e clara

Tipos comuns:
- feat: nova funcionalidade
- fix: correção de bug
- refactor: refatoração sem mudar comportamento
- style: formatação, espaçamento
- test: adição ou alteração de testes
- docs: documentação
- chore: setup, dependências, configuração
```

### Exemplos

```bash
git commit -m "feat: adiciona tela de login com validação"
git commit -m "fix: corrige cálculo de média com notas vazias"
git commit -m "refactor: extrai ModuleCard para widget separado"
git commit -m "test: adiciona testes para DisciplineModel"
git commit -m "docs: atualiza README com instruções de setup"
```

### Frequência

- Commits **pequenos e frequentes** > commits gigantes
- Cada commit deve ser **uma mudança lógica completa**
- Se o commit tiver "e" na descrição ("fiz X e Y"), divida em dois

---

## 8) Comandos Úteis

```bash
# Ver histórico
git log --oneline --graph --all

# Ver o que mudou antes de commitar
git diff

# Desfazer mudanças não commitadas
git checkout -- arquivo.dart

# Desfazer último commit (mantendo mudanças)
git reset --soft HEAD~1

# Desfazer último commit PERDENDO mudanças
git reset --hard HEAD~1

# Atualizar branch com develop sem fazer merge commit
git rebase develop

# Ver quem fez o quê em um arquivo
git blame arquivo.dart
```

---

## 9) Checklist Antes do PR

- [ ] `flutter analyze` sem erros
- [ ] `flutter test` passando
- [ ] Testei manualmente o fluxo completo
- [ ] Código segue a estrutura de pastas do projeto
- [ ] Nomes de variáveis e arquivos em snake_case
- [ ] Sem imports não utilizados
- [ ] Sem `print()` esquecidos
- [ ] Tratamento de loading e erro nas telas
- [ ] Mensagens em português
- [ ] PR descrito com o que foi feito e evidências

---

> **Regra de ouro do Git:** Se tiver dúvida, `git status` mostra tudo. Se travou, `git log` mostra onde estava. Se deu merda, `git reset --hard` resolve (mas perde as mudanças locais).
