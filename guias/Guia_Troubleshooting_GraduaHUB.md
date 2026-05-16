# GUIA DE TROUBLESHOOTING — GraduaHUB

**Versão:** 1.0  
**Público:** Equipe SENAI (iniciantes em Flutter)  
**Objetivo:** Erros comuns e soluções passo a passo — quando algo der errado, olhe aqui primeiro.

---

## Índice

1. [Erros do Flutter Doctor](#1-erros-do-flutter-doctor)
2. [Erros de Compilação](#2-erros-de-compilação)
3. [Erros do Firebase](#3-erros-do-firebase)
4. [Erros do Pub Get](#4-erros-do-pub-get)
5. [Erros de Emulador/Dispositivo](#5-erros-de-emuladordispositivo)
6. [Erros em Tempo de Execução](#6-erros-em-tempo-de-execução)
7. [Erros do Git](#7-erros-do-git)

---

## 1) Erros do Flutter Doctor

### `[✗] Android toolchain - unable to locate Android SDK`

**Causa:** Android SDK não instalado ou não configurado.

**Solução:**
```bash
# 1. Abrir Android Studio
# 2. File > Settings > Appearance & Behavior > System Settings > Android SDK
# 3. Anotar o caminho do "Android SDK Location"
# 4. Configurar variável de ambiente:
#    Windows: setx ANDROID_HOME "C:\Users\SeuNome\AppData\Local\Android\Sdk"
# 5. Fechar e reabrir terminal
# 6. Rodar flutter doctor novamente
```

### `[!] Android Studio (not installed)` mesmo tendo instalado

**Causa:** Flutter não encontrou o Android Studio.

**Solução:**
```bash
# Forçar o caminho:
flutter config --android-studio-dir="C:\Program Files\Android\Android Studio"
```

### `[!] Chrome not installed` (para web)

**Causa:** Chrome não encontrado.

**Solução:** Instalar o Google Chrome ou ignorar (não é obrigatório para Android).

---

## 2) Erros de Compilação

### `The method 'X' isn't defined for the class 'Y'`

**Causa:** Você chamou um método que não existe na classe.

**Solução:**
- Verificar se o nome do método está escrito corretamente
- Verificar se a classe tem esse método (olhar a definição)
- Verificar se você importou o arquivo certo

### `Undefined name 'X'`

**Causa:** Variável ou classe não encontrada.

**Solução:**
```dart
// Verificar:
// 1. O nome está correto?
// 2. A variável foi declarada?
// 3. O import do arquivo foi adicionado?
import 'package:graduahub/data/models/discipline_model.dart';
```

### `Target of URI doesn't exist: 'package:...'`

**Causa:** Import de um pacote que não está no pubspec.yaml.

**Solução:**
```yaml
# 1. Adicionar no pubspec.yaml
dependencies:
  pacote_faltando: ^versao

# 2. Rodar
flutter pub get
```

### Erro de null safety

```dart
// ERRO: Parameter 'nome' can't be null
void saudar(String nome) { ... }

// SOLUÇÃO: Adicionar 'required' ou valor padrão
void saudar({required String nome}) { ... }
// OU
void saudar(String? nome) { ... }
```

---

## 3) Erros do Firebase

### `FirebaseException: [core/no-app] No Firebase App '[DEFAULT]'`

**Causa:** Firebase não foi inicializado.

**Solução:**
```dart
// Verificar main.dart:
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(const GraduaHubApp());
}

// Verificar se firebase_options.dart existe
// Se não existir, rodar:
flutterfire configure --project=graduahub-dev
```

### `FirebaseAuthException: [email-already-in-use]`

**Causa:** Email já cadastrado.

**Solução:** Já tratado no AuthProvider com mensagem em português.

### `FirebaseAuthException: [invalid-credential]`

**Causa:** Email ou senha incorretos.

**Solução:** Já tratado no AuthProvider.

### `FirebaseException: [permission-denied]`

**Causa:** Regras do Firestore bloqueando a operação.

**Solução:**
```javascript
// Verificar regras no console Firebase
// Usuário só pode acessar PRÓPRIOS dados
match /users/{userId} {
  allow read, write: if request.auth.uid == userId;
}
```

### Erro de Storage

```
FirebaseException: [storage/object-not-found]
```

**Causa:** Arquivo não encontrado no Storage.

**Solução:**
```dart
// Verificar se o path está correto
final ref = _storage.ref().child('certificates/$userId/$filename');
```

---

## 4) Erros do Pub Get

### `Because [pacote] doesn't support null safety`

**Causa:** Pacote antigo sem suporte a null safety.

**Solução:**
```bash
# Forçar null safety:
flutter pub get --enable-experiment=non-nullable
# OU atualizar para versão mais recente:
flutter pub upgrade [pacote]
```

### `Error on line [X] of pubspec.yaml`

**Causa:** Erro de sintaxe no pubspec.yaml (provavelmente indentação).

**Solução:**
```yaml
# YAML usa ESPAÇOS (não tabs), e indentação é 2 espaços
dependencies:  # <-- sem espaço antes
  flutter:     # <-- 2 espaços antes
    sdk: flutter  # <-- 4 espaços antes
```

### `Warning: The package [pacote] has no SDK`

**Causa:** Versão do pacote incompatível com seu SDK.

**Solução:** Verificar se a versão do Flutter é compatível. Atualizar o Flutter:
```bash
flutter upgrade
```

---

## 5) Erros de Emulador/Dispositivo

### `No connected devices`

**Causa:** Nenhum dispositivo conectado.

**Solução:**
```bash
# Ver dispositivos disponíveis
flutter devices

# Abrir emulador pelo Android Studio
# Tools > Device Manager > Start

# Conectar celular físico
# 1. Ativar "Opções do Desenvolvedor" no celular
# 2. Ativar "Depuração USB"
# 3. Conectar USB
# 4. Aceitar permissão no celular
```

### Emulador lento

**Solução:**
```bash
# Usar emulador x86_64 (mais rápido)
# Usar dispositivo físico se possível
# No Android Studio: criar emulador com Google Play Services
# Reduzir resolução do emulador (1280x720)
```

### `Gradle build failed`

**Causa:** Erro genérico do Gradle.

**Solução:**
```bash
# 1. Limpar cache
flutter clean
flutter pub get
cd android && gradlew clean && cd ..

# 2. Verificar versão do Gradle em android/gradle-wrapper.properties

# 3. Se persistir, deletar pasta .gradle:
rm -rf ~/.gradle/caches/
```

---

## 6) Erros em Tempo de Execução

### Tela branca (app abre mas não mostra nada)

**Causa:** Erro silencioso no build do widget.

**Solução:**
```dart
// Ativar modo debug no Flutter
// O erro vai aparecer no console do terminal

// Verificar main.dart: tem Firebase.initializeApp()?
// Verificar se todos os providers estão registrados em MultiProvider
```

### `setState() called after dispose()`

**Causa:** Você tentou atualizar um widget que já foi removido da tela.

**Solução:**
```dart
// Verificar se tem setState() em async
// Sempre verificar mounted antes:
if (mounted) {
  setState(() { ... });
}
```

### Objeto null inesperado

```dart
// ERRO TÍPICO:
final nome = user.name!;  // Vai crashar se for null

// SOLUÇÃO:
final nome = user.name ?? 'Sem nome';
```

### ProviderNotFoundException

**Causa:** Você tentou usar um provider que não foi registrado.

**Solução:**
```dart
// Verificar se o provider está no MultiProvider em app.dart:
MultiProvider(
  providers: [
    ChangeNotifierProvider(create: (_) => AuthProvider()),
    ChangeNotifierProvider(create: (_) => RoutineProvider()),
    // ...
  ],
  child: const GraduaHubApp(),
)
```

---

## 7) Erros do Git

### `failed to push some refs to`

**Causa:** A branch remota tem commits que você não tem.

**Solução:**
```bash
# Puxar as mudanças e tentar de novo
git pull origin develop
git push origin develop
```

### `Merge conflict in [arquivo]`

**Causa:** Duas pessoas mexeram no mesmo arquivo.

**Solução:**   
```bash
# 1. Abrir o arquivo com conflito
# 2. Procurar por: <<<<<<< HEAD ======= >>>>>>>
# 3. Escolher versão ou juntar as duas
# 4. git add arquivo
# 5. git commit
```

### `Your branch is ahead of 'origin/develop' by 1 commit`

**Causa:** Você tem commits locais que não foram enviados.

**Solução:**
```bash
git push origin develop
```

### `Changes not staged for commit`

**Causa:** Arquivos modificados mas não adicionados.

**Solução:**
```bash
# Adicionar arquivos específicos
git add arquivo.dart

# OU adicionar tudo
git add .
```

---

> **Regra de ouro do troubleshooting:** Leia o erro. O Flutter é muito bom em te dizer exatamente o que está errado e em qual linha. Não entre em pânico — 90% dos erros são imports faltando ou null safety.
