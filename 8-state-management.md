# State Management

## StreamController & StreamBuilder
Salah satu kekurangan setState yang ada di StatefulWidget yaitu akan merebuild semua komponen didalam build method termasuk yang tidak ada kaitannya dengan state yang berubah. Tentunya ini akan sangat tidak efektif ketika screen yang dibuat sudah terdiri dari banyak widget tree. Di flutter ada salah satu kelas yang membantu kita untuk mengimplementasikan reactive programming yaitu StreamBuilder dan StreamController. StreamController berfungsi untuk menampung nilai, sedangkan StreamBuilder berfungsi untuk mengamati perubahan nilai di StreamController dan akan me-rebuild widget tree ketika terjadi perubahan state.

```dart
import 'dart:async';

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
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final _controller = StreamController<int>();

  int counter = 0;

  @override
  void initState() {
    super.initState();
  }

  @override
  void dispose() {
    _controller.close();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'You have pushed the button this many times:',
            ),
            StreamBuilder<int>(
              stream: _controller.stream,
              initialData: counter,
              builder: (context, snapshot) {
                return Text(
                  '${snapshot.data}',
                  style: Theme.of(context).textTheme.headline4,
                );
              },
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          counter += 1;
          _controller.add(counter);
        },
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

## BuildContext
Sebelum masuk ke pembahasan state management, ada baiknya kalau kita memahami terlebih dahulu tentang BuildContext yang ada di flutter. Singkatnya, BuildContext merupakan sebuah instance yang berisi informasi posisi widget dalam widget tree yang saat ini ditampilkan.

![image info](./images/widget-tree.png)

Pada gambar diatas, **Icon** merupakan **child widget** dari **Column** yang merupakan **child widget** dari **Row** . Dan **Row** sendiri merupakan **child widget** dari **Container** .

## Kapan state manager diperlukan ?

- Ketika ada kebutuhan sharing data antar screen
- Ketika codebase diperkirakan akan complex, sehingga antara layer UI dan logic aplikasi perlu dipisahkan