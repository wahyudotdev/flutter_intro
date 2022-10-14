# Navigasi dengan GoRouter

Diawal kita sudah mengenal mengenai cara navigasi di flutter menggunakan Navigator bawaan. Namun kekurangannya adalah sulitnya menghandle deeplink yang disertai parameter ketika kita menggunakan navigator bawaan dari flutter. Untuk mengatasi masalah tersebut, ada sebuah library yang mampu menghandle masalah umum navigasi yaitu GoRouter. 

## Navigasi dasar
#### 1. Buka project training dari module sebelumnya, lalu tambahkan go_router di pubspec.yaml
```yaml
dependencies:
  go_router: ^5.0.5
```

#### 2. Buatlah file baru dengan nama **router.dart**

```dart
// router.dart
import 'package:go_router/go_router.dart';
import 'package:training/detail_screen.dart';
import 'package:training/home_screen.dart';

final router = GoRouter(
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => const HomeScreen(),
    ),
    GoRoute(
      path: '/detail',
      builder: (context, state) => const DetailScreen(),
    )
  ],
);

```

#### 3. Modifikasi **main.dart** seperti dibawah
```dart
// main.dart
import 'package:flutter/material.dart';
import 'package:training/router.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      routerDelegate: router.routerDelegate,
      routeInformationParser: router.routeInformationParser,
      routeInformationProvider: router.routeInformationProvider,
    );
  }
}

```

#### 4. Lalu modifikasi juga callback onClick button di HomeScreen seperti berikut dan jalankan aplikasi Anda
```dart
// home_screen.dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Home'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () => GoRouter.of(context).push('/detail'),
          child: const Text('Go to detail'),
        ),
      ),
    );
  }
}

```
Seperti yang terlihat di kode HomeScreen bahwa kita bisa mengakses halaman detail dengan nama rutenya. Atau bisa juga kita tulis dengan syntax yang lebih pendek dengan memanfaatkan extension function gorouter
```dart
context.push('/detail')
```

Dibawah ini beberapa method yang dapat anda gunakan :
- push : pergi ke halaman tujuan dan menambahkan halaman sekarang ke backstack
- pop : untuk kembali ke halaman sebelumnya yang ada di backstack
- go : pergi ke halaman tujuan tanpa menambahkan halaman sekarang ke backstack


## Navigasi dengan membawa data
#### 1. Tambahkan property **data** dengan tipe String pada **detail_screen.dart** menjadi seperti dibawah :
```dart
// detail_screen.dart
import 'package:flutter/material.dart';

class DetailScreen extends StatelessWidget {
  const DetailScreen({super.key, required this.data});
  final String data;
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(data),
      ),
    );
  }
}

```

#### 2. Buka file router.dart dan modifikasi rute detail menjadi seperti dibawah
```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';
import 'package:training/detail_screen.dart';
import 'package:training/home_screen.dart';

final router = GoRouter(
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => const HomeScreen(),
    ),
    GoRoute(
      path: '/detail',
      builder: (context, state) {
        final data = state.extra;
        if (data is String) {
          return DetailScreen(data: data);
        }
        return Container();
      },
    )
  ],
);

```

#### 3. Buka file home_screen.dart, ubahlah menjadi StatefulWidget lalu wrap ElevatedButton dengan Column dan tambahkan TextField beserta TextEditingControllernya, kurang lebih menjadi seperti dibawah ini dan jalankan aplikasi Anda
```dart

// home_screen.dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  final controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Home'),
      ),
      body: Center(
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: [
            TextField(
              controller: controller,
            ),
            ElevatedButton(
              onPressed: () => context.push('/detail', extra: controller.text),
              child: const Text('Go to detail'),
            ),
          ],
        ),
      ),
    );
  }
}

```