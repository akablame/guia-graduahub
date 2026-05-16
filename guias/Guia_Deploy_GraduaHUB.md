# GUIA DE DEPLOY — GraduaHUB

**Versão:** 1.0  
**Público:** Equipe SENAI  
**Objetivo:** Guia para gerar o APK de apresentação e publicar o app.

---

## Índice

1. [APK de Depuração (Debug)](#1-apk-de-depuração-debug)
2. [APK de Apresentação (Release)](#2-apk-de-apresentação-release)
3. [Web – Firebase Hosting](#3-web--firebase-hosting)
4. [App Bundle (Play Store)](#4-app-bundle-play-store)
5. [Checklist Pré-Deploy](#5-checklist-pré-deploy)

---

## 1) APK de Depuração (Debug)

Para testar rápido no celular físico:

```bash
flutter build apk --debug

# APK gerado em:
# build/app/outputs/flutter-apk/app-debug.apk
```

Transferir para o celular por USB, WhatsApp, Drive, etc.

---

## 2) APK de Apresentação (Release)

### Gerar Keystore (uma vez)

```bash
keytool -genkey -v -keystore C:\Users\SeuNome\upload-keystore.jks ^
  -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 ^
  -alias upload
```

Anote a senha! Você vai precisar.

### Configurar key.properties

Criar `android/key.properties`:

```properties
storePassword=senha_que_você_definiu
keyPassword=senha_que_você_definiu
keyAlias=upload
storeFile=C:/Users/SeuNome/upload-keystore.jks
```

### Build

```bash
flutter build apk --release

# APK em:
# build/app/outputs/flutter-apk/app-release.apk
```

### Build Split (APK menor por arquitetura)

```bash
flutter build apk --release --split-per-abi
# Gera:
# - app-arm64-v8a-release.apk (recomendado)
# - app-armeabi-v7a-release.apk
# - app-x86_64-release.apk
```

---

## 3) Web – Firebase Hosting

```bash
# Build para web
flutter build web

# Instalar Firebase CLI (se não tiver)
npm install -g firebase-tools

# Login no Firebase
firebase login

# Inicializar hosting no projeto
firebase init hosting

# Escolher:
# - Firebase project: graduahub-dev
# - Public directory: build/web
# - Single-page app: Yes
# - Automatic builds: No

# Deploy
firebase deploy --only hosting

# URL: https://graduahub-dev.web.app
```

---

## 4) App Bundle (Play Store)

Para publicar na Play Store (se quiserem):

```bash
flutter build appbundle --release

# Bundle em:
# build/app/outputs/bundle/release/app-release.aab
```

Depois:
1. Acessar `play.google.com/console`
2. Criar conta de desenvolvedor (US$25 única vez)
3. Criar novo app
4. Enviar bundle
5. Preencher ficha da loja

---

## 5) Checklist Pré-Deploy

- [ ] `flutter analyze` sem erros
- [ ] `flutter test` passando
- [ ] Testar em dispositivo físico (não só emulador)
- [ ] Testar em Android e iOS (se possível)
- [ ] Dados demo populados nas contas de teste
- [ ] APK gerado e testado
- [ ] APK salvo em pendrive + nuvem
- [ ] Web deploy feito (Firebase Hosting)
- [ ] Vídeo de backup gravado

---

> **Regra de ouro do deploy:** Teste o APK em um celular que NUNCA viu o projeto antes. Se funcionou de primeira, está pronto.
