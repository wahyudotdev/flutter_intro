# Stateless dan Stateful Widget

Widget merupakan hirarki kelas tertinggi di flutter, sama seperti View di android atau UIView di SwiftUI. Widget ini dibagi lagi menjadi 2 subclass utama yaitu StatelessWidget dan StatefulWidget

## Apa itu state ?
State di flutter hanyalah sebuah local variable (properti) didalam suatu kelas. Nantinya widget akan di render ulang ketika local variable ini berubah

## Stateless Widget
Merupakan widget yang tidak memiliki local state sehingga hanya akan dirender ulang ketika parent widgetnya berubah. Contoh widget bawaan flutter yang merupakan StatelessWidget adalah ElevatedButton dan Text. 

```dart
import 'package:flutter/material.dart';

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
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatelessWidget {
  final String title;
  const MyHomePage({super.key, required this.title});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Text(title),
    );
  }
}

```
Task :
- Cobalah wrap widget Text dengan widget Center lalu save dan lihat hasilnya
- Cobalah untuk mengubah properti style pada Text widget (color, fontSize, fontWeight)

Beberapa stateless widget bawaan yang dapat anda coba :
- ElevatedButton
- TextButton
- AppBar
- FloatingActionButton
- GestureDetector

## StatefulWidget
Merupakan widget yang memiliki local state untuk mengubah UI yang ditampilkan. Cara untuk mengubah UI di StatefulWidget yaitu dengan mengganti nilai local state menggunakan method setState dimanapun didalam StatefulWidget. Apabila local state hanya diubah nilainya tanpa menggunakan setState maka UI tidak akan berubah.

```dart
import 'package:flutter/material.dart';

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
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  final String title;
  const MyHomePage({super.key, required this.title});

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int counter = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Text('Counter $counter'),
      ),
      floatingActionButton: FloatingActionButton(
        child: const Icon(Icons.add),
        onPressed: () {
          setState(() {
            counter += 1;
          });
        },
      ),
    );
  }
}

```

Stateful widget juga memiliki lifecycle sebagai berikut :
- initState : akan terpanggil sebelum widget dirender
- onDestroy : akan terpanggil setelah widget dihapus dari widget tree secara permanen