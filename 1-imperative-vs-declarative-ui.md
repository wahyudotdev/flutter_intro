# Imperative vs Declarative UI

### Imperative UI
- Diubah isinya ketika state berubah. 
- Biasanya menggunakan bahasa markup untuk membuat kerangka UI.

Contoh pada native android :
- Kode UI
```xml
<TextView
   android:id="@+id/textView"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="@string/app_name"/>

```
- Kode logic aplikasi
```kotlin
val textView = findViewById<TextView>(R.id.textView)
textView.text = “Hello mom”

```


### Declarative UI
- Dirender ulang ketika state berubah. 
- Biasanya menggunakan satu bahasa pemrograman baik untuk UI maupun logic.
Contoh :
```dart
class Item extends StatelessWidget {
 final String title;
 const Item({super.key, required this.title});

 @override
 Widget build(BuildContext context) {
   return Text(title);
 }
}

```