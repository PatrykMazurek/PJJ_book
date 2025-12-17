# Typy generyczne

Typy generyczne - wprowadzone od wersji Java 5.0, mechanizm umożliwiający tworzenie klas, interfejsów, metod opierających się na różnych typach danych bez utraty bezpieczeństwa typów i konieczności rzutowania. W uproszczeniu można powiedzieć, że typy generyczne są “szablonami”. Dzięki typom generycznym możemy uniknąć niepotrzebnego rzutowania. Ponadto przy ich pomocy kompilator jest w stanie sprawdzić poprawność typów na etapie kompilacji, oznacza to więcej błędów wykrytych w jej trakcie.

Poniższe dwa przykłady przedstawią sytuacje bez typów generycznych i z typami generycznymi.

bez typów generycznych&#x20;

```java
List list = new ArrayList();
list.add("hej");
String s = (String) list.get(0); // rzutowanie
```

Z typami generycznymi&#x20;

```java
List<String> list = new ArrayList<>();
list.add("hej");
String s = list.get(0); // bez rzutowania
```

### Budowanie klas i metod generycznych

#### Konwencje nazewnictwa

W kodzie możesz spotkasz się z jednoliterowymi oznaczeniami. Każda z poniższych wymienionych liter jest tylko umowną formą zapisu danego typu:

* T – Type (ogólny typ)
* E – Element (używane głównie w Kolekcjach, np. `List<E>`)
* K – Key (klucz w mapach)
* V – Value (wartość w mapach)
* N – Number (liczby)

**Budowa klas generycznych**

```java
public class Box<T> {
    private T value;

    public void set(T value) { this.value = value; }
    public T get() { return value; }
}
```

Przykład użycia

```java
Box<String> b1 = new Box<>();
b1.set("abc");
String x = b1.get();

Box<Integer> b2 = new Box<>();
b2.set(123);
int y = b2.get();
```

Przykład dla klasy zawierającej kilka typów generycznych

```java
public class Pair<K, V> {
    private final K key;
    private final V value;

    public Pair(K key, V value) {
        this.key = key; this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }
}
```

**Budowa metod generycznych**&#x20;

Czasami nie wymagane jest generowanie nowych klas generycznych a wystarczy stworzyć metody generyczne.&#x20;

```java
public static <T> T first(List<T> list) {
    return list.get(0);
}
```

Sposób użycia&#x20;

```java
String a = first(List.of("x", "y"));
Integer b = first(List.of(1, 2, 3));
```

**Ograniczenie typów (bounds)**

Czasami metody czy klasy wymagają ograniczenia do np. liczb (całkowitych czy zmiennoprzecinkowych. Wtedy mamy możliwość zastosować słówko `extends` i dziedziczyć np. po obiektach `Number`.&#x20;

```java
public static <T extends Number> double sum(T a, T b) {
    return a.doubleValue() + b.doubleValue();
}
```

lub obiekty, które implementują wybrany interfejs&#x20;

```java
public class X<T extends Number & Comparable<T>> { }
```

### **Zadania**

1. Napisz klasę `Box<T>`, która przechowuje jedną wartość typu T. Klasa powinna zawierać następujące  metody `set(T value)`, `T get()`, `boolean isEmpty()` (puste, gdy wartość to null), `void clear()` ustawiając wartość null. Przetestuj stworzone rozwiązanie dla kilku wybranych typów.
2. Bazując na zadaniu z zadania 1 stwórz klasę, która będzie przechowywać kilka elementów typu numerycznego. W klasie skorzystaj z listy do przechowywania nowych elementów.
3.  Stwórz następującą metodę:

    `public static void swap(List list, int i, int j)`

    Zadaniem metody będzie zamiana elementów z indeksu i na element z indeksu j. jeżeli któraś z podanych liczb wykroczy poza zakres listy wywołaj wyjątek `IndexOutOfBoundsException` . Przetestuj stworzoną metodę tak aby mogła działać dla listy z różnymi typami np. `list<String>`, `list<Integer>`&#x20;
