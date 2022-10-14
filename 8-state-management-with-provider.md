# State Management dengan Provider

## BuildContext
Sebelum masuk ke pembahasan state management, ada baiknya kalau kita memahami terlebih dahulu tentang BuildContext yang ada di flutter. Singkatnya, BuildContext merupakan sebuah instance yang berisi informasi posisi widget dalam widget tree yang saat ini ditampilkan.

![image info](./images/widget-tree.png)

Pada gambar diatas, **Icon** merupakan **child widget** dari **Column** yang merupakan **child widget** dari **Row** . Dan **Row** sendiri merupakan **child widget** dari **Container** .

## Kapan state manager diperlukan ?

- Ketika ada kebutuhan sharing data antar screen
- Ketika codebase diperkirakan akan complex, sehingga antara layer UI dan logic aplikasi perlu dipisahkan