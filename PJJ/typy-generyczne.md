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



**Budowa metod generycznych**&#x20;





### **Zadania**

1. Napisz klasę `Box<T>`, która przechowuje jedną wartość typu T. Klasa powinna zawierać następujące  metody `set(T value)`, `T get()`, `boolean isEmpty()` (puste, gdy wartość to null), `void clear()` ustawiając wartość null. Przetestuj stworzone rozwiązanie dla kilku wybranych typów.
2. Bazując na zadaniu z zadania 1 stwórz klasę, która będzie przechowywać kilka elementów typu numerycznego. W klasie skorzystaj z listy do przechowywania nowych elementów.
3.  Stwórz następującą metodę:

    `public static void swap(List list, int i, int j)`

    Zadaniem metody będzie zamiana elementów z indeksu i na element z indeksu j. jeżeli któraś z podanych liczb wykroczy poza zakres listy wywołaj wyjątek `IndexOutOfBoundsException` . Przetestuj stworzoną metodę tak aby mogła działać dla listy z różnymi typami np. `list<String>`, `list<Integer>`&#x20;
