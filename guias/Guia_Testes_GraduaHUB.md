# GUIA DE TESTES — GraduaHUB

**Versão:** 1.0  
**Público:** Equipe SENAI (iniciantes em teste de software)  
**Objetivo:** Ensinar a testar o app Flutter com confiança — unit tests, widget tests e uma pitada de integration test.

---

## Índice

1. [Por que testar?](#1-por-que-testar)
2. [Tipos de Teste no Flutter](#2-tipos-de-teste-no-flutter)
3. [Setup do Ambiente de Teste](#3-setup-do-ambiente-de-teste)
4. [Testes de Unidade (Unit Tests)](#4-testes-de-unidade-unit-tests)
5. [Testes de Widget (Widget Tests)](#5-testes-de-widget-widget-tests)
6. [Mockando Dependências](#6-mockando-dependências)
7. [Testes de Integração](#7-testes-de-integração)
8. [Cobertura de Testes](#8-cobertura-de-testes)
9. [Checklist de Testes por Módulo](#9-checklist-de-testes-por-módulo)
10. [GitHub Actions (CI)](#10-github-actions-ci)

---

## 1) Por que testar?

| Razão | Explicação |
|---|---|
| **Confiança** | Saber que uma funcionalidade não quebrou ao mexer em outra parte |
| **Documentação viva** | Testes mostram como o código DEVE se comportar |
| **Menos retrabalho** | Bug detectado cedo custa 10x menos que em produção |
| **Nota na banca** | Testes são diferencial na apresentação |

> **Regra:** Se você deu `flutter run` e testou manualmente, já fez "teste". Agora vamos automatizar isso.

---

## 2) Tipos de Teste no Flutter

```
          ┌────────────────────────────┐
          │     Integration Test       │  Lento, mas testa o app real
          ├────────────────────────────┤
          │      Widget Test           │  Médio, testa componentes
          ├────────────────────────────┤
          │       Unit Test            │  Rápido, testa lógica pura
          └────────────────────────────┘
```

| Tipo | O que testa | Velocidade | Quando usar |
|---|---|---|---|
| **Unit** | Modelos, serviços, providers | 🔥 ms | Toda lógica de negócio |
| **Widget** | Telas, formulários, componentes | ⚡ segundos | Comportamento visual |
| **Integration** | Fluxo completo | 🐢 minutos | Fluxos críticos (login) |

---

## 3) Setup do Ambiente de Teste

O Flutter já vem com `flutter_test` nativo. Não precisa instalar nada extra para começar.

```bash
# Rodar todos os testes
flutter test

# Rodar um arquivo específico
flutter test test/models/discipline_model_test.dart

# Rodar com cobertura
flutter test --coverage
# Gera coverage/lcov.info
```

### Dependências para mock (pubspec.yaml dev_dependencies)

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
  mockito: ^5.4.0
  build_runner: ^2.4.0
  mocktail: ^1.0.0  # Alternativa mais simples que mockito
```

```bash
# Se usar mockito, gerar mocks:
dart run build_runner build
```

---

## 4) Testes de Unidade (Unit Tests)

Testam lógica PURA — sem UI, sem Firebase real.

### Testando o Discipline Model

**Arquivo:** `test/models/discipline_model_test.dart`

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:graduahub/data/models/discipline_model.dart';

void main() {
  group('Discipline Model', () {
    test('weightedAverage retorna 0 quando sem notas', () {
      final d = Discipline(
        id: '1', name: 'Matemática', professor: 'João',
      );
      expect(d.weightedAverage, 0);
    });

    test('weightedAverage calcula média ponderada correta', () {
      final d = Discipline(
        id: '1', name: 'Matemática', professor: 'João',
        grades: [
          Grade(weight: 2, score: 8.0),
          Grade(weight: 3, score: 6.0),
        ],
      );
      // (2*8 + 3*6) / (2+3) = (16+18)/5 = 6.8
      expect(d.weightedAverage, 6.8);
    });

    test('remainingAbsences calcula saldo corretamente', () {
      final d = Discipline(
        id: '1', name: 'Matemática', professor: 'João',
        maxAbsences: 20, currentAbsences: 8,
      );
      expect(d.remainingAbsences, 12);
    });

    test('toMap() e fromMap() são consistentes', () {
      final d = Discipline(
        id: '1', name: 'Matemática', professor: 'João',
        maxAbsences: 20, currentAbsences: 5,
        grades: [Grade(weight: 2, score: 7.5)],
      );
      final map = d.toMap();
      final restored = Discipline.fromMap('1', map);
      expect(restored.name, d.name);
      expect(restored.weightedAverage, d.weightedAverage);
    });
  });
}
```

### Testando o AuthService (com mock)

**Arquivo:** `test/services/auth_service_test.dart`

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:mocktail/mocktail.dart';
import 'package:firebase_auth/firebase_auth.dart';
import 'package:graduahub/data/services/auth_service.dart';

class MockFirebaseAuth extends Mock implements FirebaseAuth {}
class MockUserCredential extends Mock implements UserCredential {}
class MockUser extends Mock implements User {}

void main() {
  late MockFirebaseAuth mockAuth;
  late AuthService authService;

  setUp(() {
    mockAuth = MockFirebaseAuth();
    authService = AuthService(auth: mockAuth); // precisa aceitar auth injetado
  });

  test('signUp retorna UserCredential', () async {
    when(() => mockAuth.createUserWithEmailAndPassword(
      email: any(named: 'email'),
      password: any(named: 'password'),
    )).thenAnswer((_) async => MockUserCredential());

    final result = await authService.signUp('teste@teste.com', '123456');
    expect(result, isA<UserCredential>());
  });
}
```

---

## 5) Testes de Widget (Widget Tests)

Testam a UI — formulários, estados loading/erro, navegação.

### Testando LoginScreen

**Arquivo:** `test/features/auth/login_screen_test.dart`

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'package:graduahub/providers/auth_provider.dart';
import 'package:graduahub/features/auth/login_screen.dart';

void main() {
  testWidgets('LoginScreen exibe campos de email e senha', (tester) async {
    await tester.pumpWidget(
      ChangeNotifierProvider<AuthProvider>(
        create: (_) => AuthProvider(),
        child: const MaterialApp(home: LoginScreen()),
      ),
    );

    // Verificar campos existem
    expect(find.byType(TextField), findsNWidgets(2));
    expect(find.text('Entrar'), findsOneWidget);

    // Digitar email
    await tester.enterText(find.byType(TextField).at(0), 'teste@teste.com');
    await tester.enterText(find.byType(TextField).at(1), '123456');

    // Clicar entrar
    await tester.tap(find.text('Entrar'));
    await tester.pump();

    // Verificar loading aparece
    expect(find.byType(CircularProgressIndicator), findsWidgets);
  });
}
```

### Testando estado vazio

```dart
testWidgets('DisciplinesScreen mostra empty state', (tester) async {
  await tester.pumpWidget(
    ChangeNotifierProvider<RoutineProvider>(
      create: (_) => RoutineProvider(),
      child: const MaterialApp(home: DisciplinesScreen()),
    ),
  );

  expect(find.text('Nenhuma disciplina cadastrada'), findsOneWidget);
});
```

### Padrão: Loading → Dados

Sempre teste os 3 estados:

```dart
// 1. Loading
expect(find.byType(CircularProgressIndicator), findsOneWidget);

// 2. Erro
expect(find.textContaining('Erro'), findsOneWidget);
expect(find.text('Tentar novamente'), findsOneWidget);

// 3. Dados
expect(find.byType(DisciplineCard), findsWidgets);
```

---

## 6) Mockando Dependências

### Com mocktail (mais simples)

```dart
import 'package:mocktail/mocktail.dart';

class MockFirestoreService extends Mock implements FirestoreService {}

void main() {
  late MockFirestoreService mockFirestore;

  setUp(() {
    mockFirestore = MockFirestoreService();
  });

  test('RoutineProvider busca disciplinas', () async {
    when(() => mockFirestore.streamQuery(
      collection: any(named: 'collection'),
      field: any(named: 'field'),
      value: any(named: 'value'),
    )).thenAnswer((_) => const Stream.empty());

    final provider = RoutineProvider(firestore: mockFirestore);
    // ... assert
  });
}
```

### Injeção de dependência nos providers

Para facilitar testes, os providers devem aceitar dependências injetadas:

```dart
class RoutineProvider extends ChangeNotifier {
  final FirestoreService _firestore;

  // Construtor padrão (produção)
  RoutineProvider() : _firestore = FirestoreService();

  // Construtor named para testes
  RoutineProvider.test({required FirestoreService firestore})
      : _firestore = firestore;
}
```

---

## 7) Testes de Integração

Testam o app REAL rodando em dispositivo/emulador.

### Setup

```bash
# Adicionar ao pubspec.yaml
dev_dependencies:
  integration_test:
    sdk: flutter
```

**Arquivo:** `integration_test/app_test.dart`

```dart
import 'package:flutter_test/flutter_test.dart';
import 'package:integration_test/integration_test.dart';
import 'package:graduahub/main.dart';

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('Fluxo completo: cadastrar → logar → ver dashboard', (tester) async {
    await tester.pumpWidget(const GraduaHubApp());
    await tester.pumpAndSettle();

    // Clicar em "Criar conta"
    await tester.tap(find.text('Criar conta'));
    await tester.pumpAndSettle();

    // Preencher formulário
    final email = 'teste_${DateTime.now().millisecondsSinceEpoch}@teste.com';
    await tester.enterText(find.byType(TextField).at(0), 'João');
    await tester.enterText(find.byType(TextField).at(1), email);
    await tester.enterText(find.byType(TextField).at(2), '123456');

    await tester.tap(find.text('Cadastrar'));
    await tester.pumpAndSettle();

    // Verificar que foi para Dashboard
    expect(find.text('Dashboard'), findsWidgets);
  });
}
```

---

## 8) Cobertura de Testes

```bash
flutter test --coverage
# Instalar extensão VSCode: Coverage Gutters
# Ou usar:
genhtml coverage/lcov.info -o coverage/html/
# Abrir coverage/html/index.html no navegador
```

### Meta para o projeto

| Módulo | Cobertura Mínima |
|---|---|
| **Models** (Discipline, etc.) | 100% |
| **Services** (Auth, Firestore) | 80% |
| **Providers** | 70% |
| **Telas críticas** (Login, Dashboard) | 60% |
| **Geral do projeto** | **70%+** |

---

## 9) Checklist de Testes por Módulo

### Auth
- [ ] Unit: signUp retorna UserCredential
- [ ] Unit: signIn com email errado lança exceção
- [ ] Unit: signOut não lança erro
- [ ] Widget: LoginScreen mostra loading ao logar
- [ ] Widget: LoginScreen mostra erro de senha incorreta
- [ ] Widget: RegisterScreen valida campos obrigatórios

### Discipline Model
- [ ] Unit: weightedAverage com notas vazias = 0
- [ ] Unit: weightedAverage cálculo correto
- [ ] Unit: remainingAbsences
- [ ] Unit: toMap/fromMap consistência
- [ ] Unit: neededForFinal dentro do range [0,10]

### Dashboard
- [ ] Widget: mostra nome do usuário
- [ ] Widget: mostra 4 ModuleCards
- [ ] Widget: empty state quando sem dados

### Certificados
- [ ] Widget: lista certificados do Firestore
- [ ] Widget: empty state "Nenhum certificado"
- [ ] Widget: loading indicator durante upload

### Pesquisa
- [ ] Unit: OpenAlexService parse correto
- [ ] Widget: campo de busca existe
- [ ] Widget: resultados aparecem em lista
- [ ] Widget: empty state "Nenhum resultado"

### Radar
- [ ] Widget: lista de eventos
- [ ] Widget: mapa com markers

---

## 10) GitHub Actions (CI)

**Arquivo:** `.github/workflows/test.yml`

```yaml
name: Testes
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.x'
      - run: flutter pub get
      - run: flutter test --coverage
      - uses: codecov/codecov-action@v3
```

---

> **Regra de ouro dos testes:** Teste o comportamento, não a implementação. Se você refatorar, os testes devem continuar passando sem precisar mudar nada.
