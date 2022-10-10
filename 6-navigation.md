# Navigation
Ada 2 cara dalam menggunakan navigasi bawaan di flutter, yaitu dengan menggunakan MaterialPageRoute dan dengan menggunakan named route. Kali ini akan kita bahas terlebih dahulu dengan menggunakan MaterialPageRoute. Contoh :

```dart
ElevatedButton(
    onPressed: () {
        Navigator.of(context).push(
            MaterialPageRoute(
                builder: (context) => const DetailScreen(),
            ),
        );
    }
)
```

Langsung saja untuk mencoba navigasi bisa ikuti langkah-langkah dibawah

1. Struktur folder project

```
lib
├── detail_screen.dart
├── home_screen.dart
└── main.dart
```

2. Buatlah file main.dart, isi dengan kode dibawah
```dart
// main.dart
import 'package:flutter/material.dart';
import 'package:training/home_screen.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const HomeScreen(),
    );
  }
}

```

3. Buatlah halaman detail
```dart
// detail_screen.dart
import 'package:flutter/material.dart';

class DetailScreen extends StatelessWidget {
  const DetailScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Detail'),
      ),
    );
  }
}

```

4. Buatlah halaman home yang menampilkan satu buah tombol di tengah
```dart
// home_screen.dart
import 'package:flutter/material.dart';
import 'package:training/detail_screen.dart';

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
          onPressed: () => Navigator.of(context).push(
            MaterialPageRoute(
              builder: (builder) => const DetailScreen(),
            ),
          ),
          child: const Text('Go to detail'),
        ),
      ),
    );
  }
}

```
