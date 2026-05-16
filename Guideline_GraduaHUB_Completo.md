# GUIDELINE GRADUAHUB — Documento Mestre

**Versão:** 2.0  
**Público:** Equipe SENAI (zero experiência em Flutter)  
**Objetivo:** Guia técnico passo a passo, do zero até o MVP funcionando na banca.

---

## Índice

1. [Stack e Justificativas](#1-stack-e-justificativas)
2. [Estrutura do Projeto Flutter](#2-estrutura-do-projeto-flutter)
3. [Setup do Ambiente (passo a passo real)](#3-setup-do-ambiente)
4. [Conexão com Firebase](#4-conexão-com-firebase)
5. [Padrões de Código Obrigatórios](#5-padrões-de-código-obrigatórios)
6. [Implementação dos Módulos](#6-implementação-dos-módulos)
7. [Tratamento de Erros e Loading](#7-tratamento-de-erros-e-loading)
8. [Regras de Segurança Firestore](#8-regras-de-segurança-firestore)
9. [Build e Deploy](#9-build-e-deploy)
10. [Checklist da Banca](#10-checklist-da-banca)

---

## 1) Stack e Justificativas

| Tecnologia | Função | Por quê? |
|---|---|---|
| **Flutter** | App Mobile + Web | Único código para Android, iOS e Web. Hot Reload acelera desenvolvimento. |
| **Firebase Auth** | Login/Cadastro | Pronto, gratuito, 10k usuários/mês no plano Spark. |
| **Cloud Firestore** | Banco de dados | Tempo real, escalável, integração nativa com Flutter. |
| **Firebase Storage** | Upload de certificados | 5GB grátis, integração direta com Flutter. |
| **Provider** | Gerenciamento de estado | Mais simples que Bloc/Riverpod para iniciantes. |
| **google_mlkit_text_recognition** | OCR | Offline, gratuito, lê texto de imagens. |
| **flutter_map** | Mapa | OpenStreetMap gratuito, sem API key. |
| **OpenAlex API** | Pesquisa TCC | Catálogo científico aberto, sem chave de API. |

---

## 2) Estrutura do Projeto Flutter

```
graduahub/
├── lib/
│   ├── main.dart                    # Entry point, runApp, inicialização Firebase
│   ├── app.dart                     # MaterialApp, tema, rotas
│   │
│   ├── core/
│   │   ├── theme.dart               # Cores, tipografia, estilos globais
│   │   ├── routes.dart              # Rotas nomeadas (login, dashboard, etc.)
│   │   ├── constants.dart           # Strings, URLs, chaves
│   │   └── utils/
│   │       ├── validators.dart      # Validadores de formulário
│   │       └── helpers.dart         # Formatação data/hora, etc.
│   │
│   ├── data/
│   │   ├── models/
│   │   │   ├── user_model.dart
│   │   │   ├── discipline_model.dart
│   │   │   ├── certificate_model.dart
│   │   │   └── event_model.dart
│   │   └── services/
│   │       ├── auth_service.dart      # Firebase Auth wrapper
│   │       ├── firestore_service.dart # CRUD genérico Firestore
│   │       ├── storage_service.dart   # Upload Firebase Storage
│   │       └── openalex_service.dart  # HTTP requests OpenAlex
│   │
│   ├── providers/
│   │   ├── auth_provider.dart
│   │   ├── routine_provider.dart
│   │   ├── certificate_provider.dart
│   │   └── event_provider.dart
│   │
│   └── features/
│       ├── auth/
│       │   ├── login_screen.dart
│       │   └── register_screen.dart
│       ├── dashboard/
│       │   └── dashboard_screen.dart
│       ├── routine/
│       │   ├── disciplines_screen.dart
│       │   ├── discipline_form_screen.dart
│       │   └── widgets/
│       │       ├── grade_card.dart
│       │       └── absence_chart.dart
│       ├── certificates/
│       │   ├── certificates_screen.dart
│       │   ├── certificate_upload_screen.dart
│       │   └── widgets/
│       │       └── progress_ring.dart
│       ├── research/
│       │   ├── research_screen.dart
│       │   └── widgets/
│       │       └── article_card.dart
│       └── events/
│           ├── events_screen.dart
│           ├── event_map_screen.dart
│           └── widgets/
│               └── event_card.dart
│
├── assets/
│   ├── images/     # Logos, ilustrações
│   └── fonts/      # Fontes locais (se necessário)
│
├── android/
├── ios/
├── web/
├── pubspec.yaml
└── firebase_options.dart  # Gerado automaticamente pelo FlutterFire CLI
```

---

## 3) Setup do Ambiente (passo a passo real)

### 3.1 Instalar Flutter

```bash
# 1. Acesse https://docs.flutter.dev/get-started/install/windows
# 2. Baixe o SDK em C:\dev\flutter
# 3. Adicione ao PATH do Windows:
#    C:\dev\flutter\bin
#    C:\dev\flutter\bin\cache\dart-sdk\bin

# 4. Verifique a instalação:
flutter doctor

# 5. Se aparecerem X's, corrija cada um:
#    - Android Studio: instalar Android Studio + Android SDK
#    - Android SDK: File > Settings > Appearance & Behavior > System Settings > Android SDK
#    - Chrome: instalar Chrome para debug web
```

### 3.2 Criar o Projeto

```bash
flutter create --org com.graduahub --project-name graduahub .
```

### 3.3 Adicionar Dependências (pubspec.yaml)

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^3.12.0
  firebase_auth: ^5.5.0
  cloud_firestore: ^5.6.0
  firebase_storage: ^12.4.0
  provider: ^6.1.0
  google_mlkit_text_recognition: ^0.14.0
  flutter_map: ^7.0.0
  latlong2: ^0.9.0
  http: ^1.2.0
  image_picker: ^1.1.0
  file_picker: ^8.0.0
  intl: ^0.19.0
  google_fonts: ^6.2.0
```

```bash
# Instalar dependências
flutter pub get
```

### 3.4 Configurar Firebase (Passo a Passo)

```bash
# 1. Instalar FlutterFire CLI
dart pub global activate flutterfire_cli

# 2. Acessar https://console.firebase.google.com
#    - Criar novo projeto (nome: graduahub-dev)
#    - Desabilitar Google Analytics (simplifica)

# 3. No console Firebase:
#    - Authentication > Sign-in method > Ativar Email/Senha
#    - Firestore Database > Criar banco > Modo de teste
#    - Storage > Configurar > Modo de teste

# 4. Conectar Flutter ao Firebase (pelo terminal)
flutterfire configure --project=graduahub-dev

# Isso gera firebase_options.dart automaticamente
```

### 3.5 Arquivo main.dart (inicialização)

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';
import 'app.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);
  runApp(const GraduaHubApp());
}
```

---

## 4) Conexão com Firebase

### 4.1 Auth Service (auth_service.dart)

```dart
import 'package:firebase_auth/firebase_auth.dart';

class AuthService {
  final FirebaseAuth _auth = FirebaseAuth.instance;

  User? get currentUser => _auth.currentUser;
  Stream<User?> get authStateChanges => _auth.authStateChanges();

  Future<UserCredential> signUp(String email, String password) async {
    return await _auth.createUserWithEmailAndPassword(
      email: email,
      password: password,
    );
  }

  Future<UserCredential> signIn(String email, String password) async {
    return await _auth.signInWithEmailAndPassword(
      email: email,
      password: password,
    );
  }

  Future<void> signOut() async {
    await _auth.signOut();
  }
}
```

### 4.2 Firestore Service (firestore_service.dart)

```dart
import 'package:cloud_firestore/cloud_firestore.dart';

class FirestoreService {
  final FirebaseFirestore _db = FirebaseFirestore.instance;

  // Create / Update
  Future<void> setData({
    required String collection,
    required String docId,
    required Map<String, dynamic> data,
  }) async {
    await _db.collection(collection).doc(docId).set(data, SetOptions(merge: true));
  }

  // Read (uma vez)
  Future<Map<String, dynamic>?> getDoc({
    required String collection,
    required String docId,
  }) async {
    final doc = await _db.collection(collection).doc(docId).get();
    return doc.data();
  }

  // Read (tempo real)
  Stream<DocumentSnapshot> streamDoc({
    required String collection,
    required String docId,
  }) {
    return _db.collection(collection).doc(docId).snapshots();
  }

  // Query com filtro
  Stream<QuerySnapshot> streamQuery({
    required String collection,
    required String field,
    required dynamic value,
  }) {
    return _db.collection(collection).where(field, isEqualTo: value).snapshots();
  }

  // Delete
  Future<void> deleteDoc({
    required String collection,
    required String docId,
  }) async {
    await _db.collection(collection).doc(docId).delete();
  }
}
```

### 4.3 Provider de Autenticação (auth_provider.dart)

```dart
import 'package:flutter/material.dart';
import '../data/services/auth_service.dart';
import '../data/services/firestore_service.dart';

class AuthProvider extends ChangeNotifier {
  final AuthService _authService = AuthService();
  final FirestoreService _firestoreService = FirestoreService();

  bool _isLoading = false;
  String? _error;

  bool get isLoading => _isLoading;
  String? get error => _error;
  bool get isLoggedIn => _authService.currentUser != null;
  String? get userId => _authService.currentUser?.uid;

  AuthProvider() {
    _authService.authStateChanges.listen((User? user) {
      notifyListeners();
    });
  }

  Future<bool> login(String email, String password) async {
    _isLoading = true;
    _error = null;
    notifyListeners();

    try {
      await _authService.signIn(email, password);
      _isLoading = false;
      notifyListeners();
      return true;
    } on FirebaseAuthException catch (e) {
      _error = _mapAuthError(e.code);
      _isLoading = false;
      notifyListeners();
      return false;
    }
  }

  Future<bool> register(String email, String password, String name) async {
    _isLoading = true;
    _error = null;
    notifyListeners();

    try {
      final cred = await _authService.signUp(email, password);
      await _firestoreService.setData(
        collection: 'users',
        docId: cred.user!.uid,
        data: {
          'name': name,
          'email': email,
          'createdAt': FieldValue.serverTimestamp(),
        },
      );
      _isLoading = false;
      notifyListeners();
      return true;
    } on FirebaseAuthException catch (e) {
      _error = _mapAuthError(e.code);
      _isLoading = false;
      notifyListeners();
      return false;
    }
  }

  Future<void> logout() async {
    await _authService.signOut();
  }

  String _mapAuthError(String code) {
    switch (code) {
      case 'email-already-in-use': return 'Este email já está cadastrado.';
      case 'invalid-email': return 'Email inválido.';
      case 'weak-password': return 'Senha muito fraca (mínimo 6 caracteres).';
      case 'user-not-found': return 'Usuário não encontrado.';
      case 'wrong-password': return 'Senha incorreta.';
      default: return 'Erro ao autenticar. Tente novamente.';
    }
  }
}
```

---

## 5) Padrões de Código Obrigatórios

### 5.1 Tela Padrão com Provider

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../providers/auth_provider.dart';

class LoginScreen extends StatelessWidget {
  const LoginScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Consumer<AuthProvider>(
        builder: (context, auth, _) {
          if (auth.isLoading) {
            return const Center(child: CircularProgressIndicator());
          }
          // Seu formulário aqui
          return Center(
            child: Text(auth.error ?? ''),
          );
        },
      ),
    );
  }
}
```

### 5.2 Regras de Nomenclatura

| Item | Regra | Exemplo |
|---|---|---|
| Arquivos | snake_case | `login_screen.dart` |
| Classes | PascalCase | `LoginScreen` |
| Variáveis/const | camelCase | `userName` |
| Constantes | UPPER_SNAKE | `kMaxHours` |
| Providers | camelCase + Provider | `authProvider` |
| Telas | Nome + Screen | `DashboardScreen` |
| Widgets | Nome descritivo | `ProgressRing`, `ArticleCard` |

### 5.3 Estrutura de Provider + Consumer

```dart
// NO PROVIDER (sempre):
class MeuProvider extends ChangeNotifier {
  bool _loading = false;
  String? _error;

  bool get loading => _loading;
  String? get error => _error;

  Future<void> minhaFuncao() async {
    _loading = true; _error = null; notifyListeners();
    try {
      // ... lógica ...
    } catch (e) {
      _error = e.toString();
    }
    _loading = false; notifyListeners();
  }
}

// NA TELA (sempre):
Consumer<MeuProvider>(
  builder: (_, provider, __) {
    if (provider.loading) return const CircularProgressIndicator();
    if (provider.error != null) return Text(provider.error!);
    return // ... seu widget ...
  },
)
```

---

## 6) Implementação dos Módulos

### 6.1 Módulo Auth

**Arquivos:**
- `features/auth/login_screen.dart`
- `features/auth/register_screen.dart`
- `providers/auth_provider.dart` (já feito acima)

**Fluxo:**
1. App abre → `main.dart` → `app.dart` → verifica `authProvider.isLoggedIn`
2. Se não logado → `LoginScreen`
3. Se logado → `DashboardScreen`
4. Botão "Sair" no Dashboard → `authProvider.logout()`

**Roteamento (routes.dart):**
```dart
import 'package:flutter/material.dart';
import 'features/auth/login_screen.dart';
import 'features/dashboard/dashboard_screen.dart';

class AppRoutes {
  static const String login = '/login';
  static const String dashboard = '/dashboard';

  static Map<String, WidgetBuilder> routes = {
    login: (_) => const LoginScreen(),
    dashboard: (_) => const DashboardScreen(),
  };
}
```

### 6.2 Módulo Dashboard

**Função:** Mostrar cards de atalho para cada módulo + resumo do progresso.

**Widget Tree:**
```
DashboardScreen
├── AppBar (título + botão logout)
├── GridView
│   ├── ModuleCard("Rotina", icon, cor)
│   ├── ModuleCard("Certificados", icon, cor)
│   ├── ModuleCard("Pesquisa TCC", icon, cor)
│   └── ModuleCard("Eventos", icon, cor)
└── ProgressSummary (horas complementares)
```

### 6.3 Módulo Rotina (Disciplinas + Notas + Faltas)

**Modelo (discipline_model.dart):**
```dart
class Discipline {
  final String id;
  final String name;
  final String professor;
  final double maxAbsences;
  final double currentAbsences;
  final List<Grade> grades; // [{weight: 2, score: 8.5}, ...]

  Discipline({
    required this.id,
    required this.name,
    required this.professor,
    this.maxAbsences = 20,
    this.currentAbsences = 0,
    this.grades = const [],
  });

  double get weightedAverage {
    if (grades.isEmpty) return 0;
    double totalWeight = 0;
    double totalScore = 0;
    for (final g in grades) {
      totalWeight += g.weight;
      totalScore += g.weight * g.score;
    }
    return totalScore / totalWeight;
  }

  double get remainingAbsences => maxAbsences - currentAbsences;

  double get neededForFinal {
    // (5.0 - weightedAverage) * totalWeight / finalWeight
    final needed = (5.0 - weightedAverage) * 10 / 4;
    return needed.clamp(0, 10);
  }

  Map<String, dynamic> toMap() => {
    'name': name,
    'professor': professor,
    'maxAbsences': maxAbsences,
    'currentAbsences': currentAbsences,
    'grades': grades.map((g) => {'weight': g.weight, 'score': g.score}).toList(),
  };
}

class Grade {
  final double weight;
  final double score;
  Grade({required this.weight, required this.score});
}
```

### 6.4 Módulo Certificados

**Fluxo:**
1. `CertificateUploadScreen` → botão "Adicionar Certificado"
2. `FilePicker` ou `ImagePicker` → seleciona PDF/imagem
3. Upload para Firebase Storage → pega URL
4. Salva no Firestore: `certificates/{certId}`
5. Dashboard exibe total de horas do usuário

**Upload (storage_service.dart):**
```dart
import 'package:firebase_storage/firebase_storage.dart';
import 'dart:io';

class StorageService {
  final FirebaseStorage _storage = FirebaseStorage.instance;

  Future<String> uploadFile({
    required String path,
    required String userId,
  }) async {
    final file = File(path);
    final filename = '$userId/${DateTime.now().millisecondsSinceEpoch}';
    final ref = _storage.ref().child('certificates/$filename');
    await ref.putFile(file);
    return await ref.getDownloadURL();
  }
}
```

### 6.5 Módulo Pesquisa TCC (OpenAlex)

**API Call (openalex_service.dart):**
```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class OpenAlexService {
  Future<List<Map<String, dynamic>>> searchArticles(String query) async {
    final url = Uri.https('api.openalex.org', '/works', {
      'search': query,
      'filter': 'language:pt',
      'per_page': '20',
    });

    final response = await http.get(url);
    if (response.statusCode != 200) {
      throw Exception('Erro na API OpenAlex');
    }

    final data = jsonDecode(response.body);
    final results = data['results'] as List;

    return results.map((r) => {
      'title': r['title'] ?? 'Sem título',
      'authors': (r['authorships'] as List?)
              ?.map((a) => a['author']['display_name'])
              .take(3)
              .join(', ') ?? 'Autores não disponíveis',
      'abstract': r['abstract_inverted_index'] != null
          ? _decodeAbstract(r['abstract_inverted_index'])
          : 'Resumo não disponível',
      'url': r['doi'] ?? r['primary_location']?['landing_page_url'] ?? '',
      'year': r['publication_year'] ?? '',
    }).toList();
  }

  String _decodeAbstract(Map abstract) {
    // OpenAlex retorna abstract em formato invertido
    final words = <String>[];
    abstract.forEach((word, positions) {
      for (final pos in positions as List) {
        words.add('$pos::$word');
      }
    });
    words.sort((a, b) {
      final aPos = int.parse(a.split('::')[0]);
      final bPos = int.parse(b.split('::')[0]);
      return aPos.compareTo(bPos);
    });
    return words.map((w) => w.split('::')[1]).join(' ');
  }
}
```

### 6.6 Módulo Radar de Eventos

**Mapa (event_map_screen.dart):**
```dart
import 'package:flutter/material.dart';
import 'package:flutter_map/flutter_map.dart';
import 'package:latlong2/latlong.dart';

class EventMapScreen extends StatelessWidget {
  final List<Map<String, dynamic>> events;

  const EventMapScreen({super.key, required this.events});

  @override
  Widget build(BuildContext context) {
    return FlutterMap(
      options: const MapOptions(
        initialCenter: LatLng(-23.5505, -46.6333), // Centro de SP
        initialZoom: 12,
      ),
      children: [
        TileLayer(
          urlTemplate: 'https://tile.openstreetmap.org/{z}/{x}/{y}.png',
        ),
        MarkerLayer(
          markers: events.map((event) {
            return Marker(
              point: LatLng(event['lat'], event['lng']),
              width: 40,
              height: 40,
              child: const Icon(Icons.location_on, color: Colors.red, size: 36),
            );
          }).toList(),
        ),
      ],
    );
  }
}
```

---

## 7) Tratamento de Erros e Loading

Toda tela precisa de 3 estados:

```dart
// 1. LOADING
if (provider.loading) {
  return const Center(child: CircularProgressIndicator());
}

// 2. ERRO
if (provider.error != null) {
  return Center(
    child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        const Icon(Icons.error_outline, size: 48, color: Colors.red),
        const SizedBox(height: 16),
        Text(provider.error!, textAlign: TextAlign.center),
        const SizedBox(height: 16),
        ElevatedButton(
          onPressed: () => provider.recarregar(),
          child: const Text('Tentar novamente'),
        ),
      ],
    ),
  );
}

// 3. VAZIO
if (provider.lista.isEmpty) {
  return Center(
    child: Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        const Icon(Icons.inbox_outlined, size: 48, color: Colors.grey),
        const SizedBox(height: 16),
        const Text('Nenhum item encontrado'),
      ],
    ),
  );
}

// 4. DADOS
return ListView.builder(
  itemCount: provider.lista.length,
  itemBuilder: (_, index) => ItemCard(provider.lista[index]),
);
```

---

## 8) Regras de Segurança Firestore

```javascript
// Firestore Rules
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    // Usuário só pode ler/escrever PRÓPRIOS dados
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }

    match /certificates/{certId} {
      allow read: if request.auth != null && resource.data.userId == request.auth.uid;
      allow create: if request.auth != null && request.resource.data.userId == request.auth.uid;
      allow update, delete: if request.auth != null && resource.data.userId == request.auth.uid;
    }

    match /grades/{gradeId} {
      allow read: if request.auth != null && resource.data.userId == request.auth.uid;
      allow create: if request.auth != null && request.resource.data.userId == request.auth.uid;
      allow update, delete: if request.auth != null && resource.data.userId == request.auth.uid;
    }

    // Eventos são públicos (leitura para todos logados)
    match /events/{eventId} {
      allow read: if request.auth != null;
    }

    // Regra para Storage
    match /certificates/{fileName} {
      allow read: if request.auth != null;
      allow write: if request.auth != null
        && fileName.startsWith(request.auth.uid);
    }
  }
}
```

---

## 9) Build e Deploy

### 9.1 APK de Depuração

```bash
# Para testar no celular físico
flutter build apk --debug

# APK estará em: build/app/outputs/flutter-apk/app-debug.apk
```

### 9.2 APK de Apresentação (Release)

```bash
# 1. Gerar keystore (só precisa fazer uma vez)
keytool -genkey -v -keystore C:\Users\SeuNome\upload-keystore.jks ^
  -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 ^
  -alias upload

# 2. Criar android/key.properties com:
#    storePassword=senha
#    keyPassword=senha
#    keyAlias=upload
#    storeFile=C:/Users/SeuNome/upload-keystore.jks

# 3. Build
flutter build apk --release

# APK estará em: build/app/outputs/flutter-apk/app-release.apk
```

### 9.3 Web (Firebase Hosting)

```bash
# Build para web
flutter build web

# Instalar Firebase CLI
npm install -g firebase-tools

# Inicializar hosting
firebase init hosting

# Deploy
firebase deploy --only hosting
```

---

## 10) Checklist da Banca

### Funcionalidades (obrigatório funcionar)

- [ ] **Cadastro:** criar conta com email + senha + nome
- [ ] **Login:** entrar com email + senha
- [ ] **Logout:** sair da conta, voltar para tela de login
- [ ] **Persistência:** fechar e abrir app continua logado
- [ ] **Dashboard:** exibir cards dos módulos
- [ ] **Rotina:** adicionar disciplina, lançar nota, ver média
- [ ] **Rotina:** ver faltas restantes
- [ ] **Certificado:** fazer upload de PDF
- [ ] **Certificado:** ver progresso de horas no dashboard
- [ ] **Pesquisa:** buscar artigo no OpenAlex e ver resultados
- [ ] **Eventos:** ver lista de eventos do Firestore
- [ ] **Eventos:** ver mapa com pins dos eventos

### Qualidade

- [ ] Sem crash ao navegar entre telas
- [ ] Loading visível em operações lentas
- [ ] Mensagem de erro amigável quando algo falha
- [ ] Estado vazio quando não há dados
- [ ] Design consistente (cores, fontes, espaçamento)

### Apresentação

- [ ] Contas de teste criadas com dados reais
- [ ] Roteiro de demo de 5-8 minutos
- [ ] Video de backup do fluxo completo
- [ ] Cada membro sabe explicar uma parte técnica

---

> **Regra de ouro:** funcionalidade simples funcionando > funcionalidade complexa quebrada. Entreguem o básico PERFEITO.
