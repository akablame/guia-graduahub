# PLANO DE ESTUDOS GRADUAHUB — Trilha para Iniciantes

**Duração:** 4 semanas de capacitação intensiva + 4 semanas de estudo paralelo ao desenvolvimento  
**Carga:** 2h/dia útil (mínimo) | 3h/dia (ideal) | 4h sábado  
**Pré-requisito:** Lógica de programação básica (if, for, while — se não tiver, estude 1 semana antes)

---

## Índice

1. [Como usar este plano](#1-como-usar-este-plano)
2. [Semana 1 — Dart + Flutter Essencial](#2-semana-1)
3. [Semana 2 — Firebase + State Management](#3-semana-2)
4. [Semana 3 — Mini Projetos Obrigatórios](#4-semana-3)
5. [Semana 4 — Avançado + Integrações](#5-semana-4)
6. [Semanas 5-8 — Estudo Paralelo ao Desenvolvimento](#6-semanas-5-8)
7. [Recursos Oficiais (links)](#7-recursos-oficiais)
8. [Erros Comuns e Soluções](#8-erros-comuns-e-soluções)

---

## 1) Como usar este plano

- **Dia 1-5 (Semana 1):** Seguir a ordem de exercícios **exatamente como listada**
- **Dia 6-10 (Semana 2):** Praticar com os mini projetos
- **Meta:** ao final de 4 semanas, cada membro do time deve ser capaz de criar uma tela com formulário, salvar no Firestore e exibir em lista
- **Parar e revisar:** se mais de 30% do time não conseguir fazer um exercício, repetir no dia seguinte

---

## 2) Semana 1 — Dart + Flutter Essencial

### Dia 1 — Dart: Variáveis, Tipos, Funções

**O que estudar:**
1. [Dart Tour (Páginas 1-10):](https://dart.dev/language) variáveis, tipos, `final` vs `const`
2. [Funções em Dart:](https://dart.dev/language/functions) parâmetros nomeados, `=>` arrow syntax
3. [Null Safety:](https://dart.dev/null-safety) `?`, `!`, `late`

**Exercícios para fazer (no DartPad — https://dartpad.dev):**

```dart
// 1. Declare uma variável String com seu nome e um int com sua idade
String nome = 'João';
int idade = 20;

// 2. Crie uma função que recebe dois números e retorna a média
double calcularMedia(double a, double b) => (a + b) / 2;

// 3. Crie uma função que recebe um nome nullable e retorna "Olá, nome" ou "Olá, visitante"
String saudacao(String? nome) => 'Olá, ${nome ?? "visitante"}';

// 4. Crie uma função que recebe uma lista de números e retorna a soma
int somarLista(List<int> numeros) => numeros.fold(0, (a, b) => a + b);
```

**Entregável:** 10 exercícios de lógica em Dart resolvidos.

---

### Dia 2 — Dart: Listas, Mapas, Classes

**O que estudar:**
1. [Coleções em Dart:](https://dart.dev/language/collections) `List`, `Set`, `Map`
2. [Classes:](https://dart.dev/language/classes) construtores, `this`, `named parameters`
3. [Records e Patterns (básico)](https://dart.dev/language/records)

**Exercícios:**

```dart
// 1. Crie uma classe Aluno com nome, idade, lista de notas
class Aluno {
  final String nome;
  final int idade;
  final List<double> notas;
  
  Aluno({required this.nome, required this.idade, required this.notas});
  
  double get media => notas.isEmpty 
    ? 0 
    : notas.reduce((a, b) => a + b) / notas.length;
}

// 2. Crie uma lista de alunos e filtre os aprovados (média >= 7)
List<Aluno> aprovados(List<Aluno> turma) {
  return turma.where((a) => a.media >= 7).toList();
}

// 3. Crie um Map<String, double> para armazenar preços de produtos
//    e uma função que retorna o total do carrinho
double calcularTotal(Map<String, double> precos, List<String> itens) {
  return itens.fold(0, (total, item) => total + (precos[item] ?? 0));
}
```

**Entregável:** Sistema de cadastro de alunos com cálculo de média em Dart puro.

---

### Dia 3 — Flutter: Primeiro App + Widgets

**O que estudar:**
1. [Flutter Get Started:](https://docs.flutter.dev/get-started/install) instalação + primeiro app
2. [Widgets fundamentais:](https://docs.flutter.dev/ui/widgets) `Text`, `Container`, `Row`, `Column`, `Stack`
3. [StatefulWidget vs StatelessWidget](https://docs.flutter.dev/ui/widgets-intro)

**Prática:**

```bash
# Criar projeto de teste
flutter create meu_primeiro_app
cd meu_primeiro_app
flutter run
```

**Código para testar:**

```dart
import 'package:flutter/material.dart';

void main() => runApp(const MeuApp());

class MeuApp extends StatelessWidget {
  const MeuApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('Meu Primeiro App')),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: const [
              Text('Olá, GraduaHUB!', style: TextStyle(fontSize: 24)),
              SizedBox(height: 16),
              Icon(Icons.school, size: 64, color: Colors.purple),
            ],
          ),
        ),
      ),
    );
  }
}
```

**Exercícios:**
1. Recriar o layout acima com diferentes widgets
2. Adicionar um `Image` da internet
3. Criar um `Container` decorado (borda, sombra, gradiente)

**Entregável:** App rodando no emulador com layout customizado.

---

### Dia 4 — Flutter: Navegação + Formulários

**O que estudar:**
1. [Navigator:](https://docs.flutter.dev/ui/navigation) `push`, `pop`, `pushNamed`
2. [Formulários:](https://docs.flutter.dev/cookbook/forms/validation) `TextEditingController`, `Form`, `GlobalKey`, `validator`
3. [SnackBar e diálogos](https://docs.flutter.dev/cookbook/design/snackbars)

**Código para testar:**

```dart
// Navegação entre telas
Navigator.push(
  context,
  MaterialPageRoute(builder: (_) => const SegundaTela()),
);

// Formulário com validação
final _formKey = GlobalKey<FormState>();
final _nomeController = TextEditingController();

Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        controller: _nomeController,
        validator: (value) => value!.isEmpty ? 'Campo obrigatório' : null,
        decoration: const InputDecoration(labelText: 'Nome'),
      ),
      ElevatedButton(
        onPressed: () {
          if (_formKey.currentState!.validate()) {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(content: Text('Olá, ${_nomeController.text}!')),
            );
          }
        },
        child: const Text('Enviar'),
      ),
    ],
  ),
);
```

**Exercícios:**
1. Criar 3 telas com navegação (Login → Cadastro → Home)
2. Criar formulário de cadastro com 4 campos e validação
3. Passar dados entre telas via construtor

**Entregável:** App com 3 telas navegáveis e formulário validado.

---

### Dia 5 — Flutter: Listas + Layout Responsivo

**O que estudar:**
1. [ListView.builder:](https://docs.flutter.dev/cookbook/lists/long-lists) listas dinâmicas
2. [GridView:](https://docs.flutter.dev/cookbook/lists/grid-lists) grade de cards
3. [LayoutBuilder e MediaQuery:](https://docs.flutter.dev/ui/layout/responsive) responsividade

**Exercícios:**
1. Criar uma lista de 20 itens com `ListView.builder`
2. Criar cards customizados para cada item (com `Card` widget)
3. Adaptar layout entre celular e tablet

```dart
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return Card(
      child: ListTile(
        leading: const Icon(Icons.star),
        title: Text(items[index].nome),
        subtitle: Text(items[index].descricao),
        trailing: Text('${items[index].valor}'),
      ),
    );
  },
);
```

**Entregável:** Tela com lista dinâmica de cards estilizados.

---

## 3) Semana 2 — Firebase + State Management

### Dia 6 — State Management com Provider

**O que estudar:**
1. [Provider package:](https://pub.dev/packages/provider) `ChangeNotifier`, `Consumer`, `Provider.of`
2. [Conceito:](https://docs.flutter.dev/data-and-backend/state-mgmt/simple) por que usar state management?

**Código para testar:**

```dart
// 1. provider/contador_provider.dart
class ContadorProvider extends ChangeNotifier {
  int _count = 0;
  int get count => _count;

  void incrementar() {
    _count++;
    notifyListeners();
  }
}

// 2. No main.dart (antes do runApp):
runApp(
  ChangeNotifierProvider(
    create: (_) => ContadorProvider(),
    child: const MeuApp(),
  ),
);

// 3. Na tela:
Consumer<ContadorProvider>(
  builder: (context, provider, _) {
    return Text('Contagem: ${provider.count}');
  },
);
```

**Exercícios:**
1. Criar um contador com Provider (incrementar/decrementar)
2. Criar um ToDo list com Provider (adicionar/remover itens)
3. Adicionar persistência local com `shared_preferences`

**Entregável:** ToDo list funcional com Provider.

---

### Dia 7 — Firebase Auth

**O que estudar:**
1. [Firebase Auth Flutter:](https://firebase.flutter.dev/docs/auth/overview/) configuração + métodos
2. [Email/Password auth:](https://firebase.flutter.dev/docs/auth/usage) createUser, signIn, signOut
3. [Stream de auth state:](https://firebase.flutter.dev/docs/auth/usage#listen-to-authentication-state) `authStateChanges()`

**Prática (copiar para projeto de teste):**

```bash
# No projeto de teste
flutter pub add firebase_core firebase_auth

# Configurar Firebase (ver Guideline seção 3.4)
```

```dart
// services/auth_service.dart (copiar do Guideline seção 4.1)

// providers/auth_provider.dart (copiar do Guideline seção 4.3)

// Telas: login_screen.dart e register_screen.dart
```

**Exercícios:**
1. Implementar tela de login com email/senha
2. Implementar tela de cadastro com validação
3. Mostrar/esconder telas baseado no estado de autenticação
4. Tratar erros específicos (email já existe, senha fraca, etc.)

**Entregável:** App com login/cadastro funcional conectado ao Firebase.

---

### Dia 8 — Firestore CRUD

**O que estudar:**
1. [Firestore Flutter:](https://firebase.flutter.dev/docs/firestore/usage) `add`, `set`, `get`, `snapshots`
2. [Modelos Dart:](https://firebase.flutter.dev/docs/firestore/usage#data-types) `toMap()`, `fromMap()`
3. [Streams:](https://dart.dev/language/async#stream) `StreamBuilder` + Firestore

**Prática:**

```dart
// model/tarefa_model.dart
class Tarefa {
  final String id;
  final String titulo;
  final bool concluida;

  Tarefa({required this.id, required this.titulo, this.concluida = false});

  Map<String, dynamic> toMap() => {'titulo': titulo, 'concluida': concluida};

  factory Tarefa.fromMap(String id, Map<String, dynamic> map) => Tarefa(
    id: id,
    titulo: map['titulo'] ?? '',
    concluida: map['concluida'] ?? false,
  );
}

// CRUD
Future<void> adicionarTarefa(Tarefa tarefa) async {
  await FirebaseFirestore.instance.collection('tarefas').add(tarefa.toMap());
}

Stream<List<Tarefa>> listarTarefas(String userId) {
  return FirebaseFirestore.instance
    .collection('tarefas')
    .where('userId', isEqualTo: userId)
    .snapshots()
    .map((snap) => snap.docs
      .map((doc) => Tarefa.fromMap(doc.id, doc.data()))
      .toList());
}
```

**Exercícios:**
1. CRUD completo de tarefas no Firestore
2. Lista em tempo real com `StreamBuilder`
3. Filtro por usuário logado

**Entregável:** ToDo list persistente no Firestore.

---

### Dia 9 — Firebase Storage + Image Picker

**O que estudar:**
1. [Firebase Storage Flutter:](https://firebase.flutter.dev/docs/storage/usage) upload, download URL
2. [Image Picker:](https://pub.dev/packages/image_picker) câmera + galeria
3. [File Picker:](https://pub.dev/packages/file_picker) PDF selecionado

**Prática:**

```dart
import 'package:image_picker/image_picker.dart';

final picker = ImagePicker();
final file = await picker.pickImage(source: ImageSource.gallery);

if (file != null) {
  final storageRef = FirebaseStorage.instance
    .ref()
    .child('uploads/${DateTime.now().millisecondsSinceEpoch}.jpg');
  await storageRef.putFile(File(file.path));
  final url = await storageRef.getDownloadURL();
  print('URL do arquivo: $url');
}
```

**Exercícios:**
1. Selecionar imagem da galeria e fazer upload
2. Exibir imagem após upload
3. Salvar URL no Firestore

**Entregável:** App que tira foto, faz upload e mostra na tela.

---

### Dia 10 — HTTP + API externa (OpenAlex)

**O que estudar:**
1. [http package:](https://pub.dev/packages/http) GET requests
2. [JSON decoding:](https://dart.dev/language/json) `jsonDecode`, `jsonEncode`
3. [Tratamento de erro de rede:](https://docs.flutter.dev/cookbook/networking/fetch-data) try/catch + timeout

**Prática:**

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<List<dynamic>> buscarArtigos(String query) async {
  final url = Uri.parse('https://api.openalex.org/works?search=$query&per_page=10');
  final response = await http.get(url);
  if (response.statusCode == 200) {
    final data = jsonDecode(response.body);
    return data['results'];
  } else {
    throw Exception('Falha ao carregar: ${response.statusCode}');
  }
}
```

**Exercícios:**
1. Fazer requisição GET para OpenAlex
2. Exibir resultados em uma lista
3. Tratar loading, erro e lista vazia

**Entregável:** App de busca de artigos consumindo API real.

---

## 4) Semana 3 — Mini Projetos Obrigatórios

### Mini Projeto 1: ToDo List Completo (2 dias)

**Funcionalidades:**
- Login com Firebase Auth
- CRUD de tarefas no Firestore
- Marcar como concluída
- Filtrar: todas, pendentes, concluídas
- Provider para estado

**Não pode faltar:**
- [ ] Tela de login
- [ ] Lista de tarefas em tempo real
- [ ] Adicionar tarefa com formulário
- [ ] Loading e erro tratados
- [ ] Logout funcional

### Mini Projeto 2: Cadastro + Upload (2 dias)

**Funcionalidades:**
- Formulário de cadastro de produto/pessoa
- Upload de foto
- Lista com dados + foto
- Editar e excluir

**Não pode faltar:**
- [ ] Validação de formulário
- [ ] Upload para Firebase Storage
- [ ] Lista com StreamBuilder
- [ ] Excluir com confirmação

---

## 5) Semana 4 — Avançado + Integrações

| Dia | Tema | O que fazer |
|---|---|---|
| 1 | Navegação avançada | BottomNavigationBar + IndexedStack |
| 2 | Maps | flutter_map + marcadores + localização |
| 3 | OCR | google_mlkit_text_recognition |
| 4 | Animações | AnimatedContainer, Hero, transitions |
| 5 | Tema global | Tema escuro/claro, Google Fonts |
| 6 | Revisão geral | Juntar tudo + corrigir bugs |

---

## 6) Semanas 5-8 — Estudo Paralelo ao Desenvolvimento

Durante as sprints, estudar **apenas o que for necessário** para a próxima tarefa:

| Sprint | Estudo necessário |
|---|---|
| Auth + Shell | Provider, Firebase Auth, Navigator |
| Dashboard | GridView, Cards, StreamBuilder |
| Rotina | Forms, cálculos, validação |
| Certificados | ImagePicker, Storage, File |
| Pesquisa | HTTP, JSON, ListView |
| Radar | flutter_map, geolocator, marcadores |

---

## 7) Recursos Oficiais (links)

### Dart
- [Dart Language Tour](https://dart.dev/language) — documentação oficial completa
- [DartPad](https://dartpad.dev) — praticar Dart direto no navegador
- [Dart Codelabs](https://dart.dev/codelabs) — tutoriais interativos oficiais

### Flutter
- [Flutter Get Started](https://docs.flutter.dev/get-started/install) — instalação
- [Flutter Codelabs](https://docs.flutter.dev/codelabs) — tutoriais oficiais
- [Widget of the Week (YouTube)](https://www.youtube.com/playlist?list=PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG) — playlist curta sobre cada widget
- [Layout tutorial](https://docs.flutter.dev/ui/layout/tutorial) — como organizar widgets

### Firebase
- [FlutterFire Overview](https://firebase.flutter.dev/docs/overview) — docs oficiais
- [Firebase Auth](https://firebase.flutter.dev/docs/auth/overview)
- [Cloud Firestore](https://firebase.flutter.dev/docs/firestore/usage)
- [Firebase Storage](https://firebase.flutter.dev/docs/storage/usage)

### YouTube (canais gratuitos)
- [Flutter com Migs](https://www.youtube.com/@fluttercommigs) — português
- [Flutter Mapp](https://www.youtube.com/@FlutterMapp) — tutoriais rápidos
- [NetNinja Flutter Course](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jLYyp2Aoh6hcWuxFDX6PBJ) — inglês, muito bom

---

## 8) Erros Comuns e Soluções

| Erro | Causa | Solução |
|---|---|---|
| `flutter: [ERROR] No Firebase App '[DEFAULT]'` | Firebase não inicializado | Chamar `Firebase.initializeApp()` no `main.dart` |
| `Null check operator used on a null value` | Usar `!` em variável null | Usar `??` ou `?.` |
| `setState() called after dispose()` | Atualizar widget descartado | Usar `mounted` check ou Provider |
| `The method 'toMap' isn't defined` | Modelo sem método | Criar `Map<String, dynamic> toMap()` |
| `type 'List<dynamic>' is not a subtype` | Parse JSON errado | Especificar tipo: `data['results'] as List` |
| `PERMISSION_DENIED` | Regras Firestore bloqueando | Atualizar regras no Console Firebase |
| `FirebaseException: [cloud_firestore/not-found]` | Documento não existe | Verificar ID do documento |
