# Interfejsy Funkcyjne i Lambda

### Wyrażenia Lambda&#x20;

**Wyrażenie lambda** reprezentuje implementację **interfejsu funkcyjnego.**&#x20;

**Skłądnia lambdy**

### (parametry) -> ciało

**Przykład jedno parametrowy**&#x20;

```
x -> x * x
```

**Przykład dwu parametrowy**&#x20;

```
(a, b) -> a + b
```

**Z bloiem kodu (wielo linijkowy.**

```
(a, b) -> {
    return a + b;
}
```

### Interfejsy Funkcyjne

Interfejs funkcyjny to interfejs, który posiada dokładnie jedną metodę abstrakcyjną. Może posiadać dowolną liczbę metod domyślnych i statycznych. Adnotacja `@FunctionalInterface` jest opcjonalny ale po dodaniu drugiej metody abstrakcyjnej pojawi się błąd kompilacji.&#x20;

**Cztery podstawę interfejsy funkcyjne**

| Interfejsy      | Metody abstrakcyjne | Co wykonuje                     | Przykład użycia              |
| --------------- | ------------------- | ------------------------------- | ---------------------------- |
| Predicate\<T>   | `boolean test(T t)` | Sprawdza warunek (Filtr)        | `x -> x > 18`                |
| Consumer\<T>    | `void accept(T t)`  | Konsumuje dane (Drukarka)       | `x -> System.out.println(x)` |
| Supplier\<T>    | `T get()`           | Dostarcza dane (Fabryka)        | `() -> LocalDate.now()`      |
| Function\<T, R> | `R apply(T t)`      | Przetwarza dane (Transformator) | `s -> s.length()`            |
|                 |                     |                                 |                              |

**Interfejs Predicate** - interfejs, który przyjmuje dowolny obiekt na wejściu i zwraca tylko wertość logiczną TRUE lub FALSE.

```java
@FunctionalInterface
public interface Predicate<T> {

    boolean test(T t);
    
    ...
}
```

Przykład użycia

```java
import java.util.function.Predicate;

public class Start {

    public static void main(String[] args) {

        Predicate<String> testPredicate = name -> name.length() > 3;
        if (testPredicate.test("dowolny tekst do sprawdzenia"){
            System.out.println("właściwa długość tekstu");
        }else{
            System.out.println("niewłaściwa długość tekstu");
        }
    }
}
```

**Interfejs Consumer** -interfejs, który przyjmuje jedne argument, przetwarza go ale nic nie zwraca

```java
@FunctionalInterface
public interface Consumer<T> {

    void accept(T t);
    
    ...
}
```

Sposób wywołania

```java
import java.util.function.Consumer;

public class Main{
    public static void main(String[] args) {

        Consumer<Integer> item = id -> System.out.println(id);
        item.accept(10);
    }
}    
```

**Interfejs Supplier -** Interfejs Supplier nie przyjmuje żadnego argumentu, ale zwraca obiekt ustalonego typu

```java
@FunctionalInterface
public interface Supplier<T> {

    T get();
    
    ...
}
```

Sposób wywołania

```java
import java.util.function.Supplier;

public class Main{     
    public static void main(String[] args) {
    
        Supplier<String> item = () -> "This is description for MovieItem";
        String description = item.getDescription();
        System.out.println(description);
    }  
} 
```

**Interfejs Function** - interfejs, który może przyjąć dowolny obiekt na wejściu, przetworzyć i zwrócić również dowolny obiekt.&#x20;

```java
@FunctionalInterface
public interface Function<T, R> {

    R apply(T t);

    ...
}
```

Sposób wywołania

```java
import java.util.function.Function;

public class Main{

    public static void main(String[] args) {

        Function<Integer, String> functionApplier = value -> String.valueOf(value);
        System.out.println(function.apply(27));
    }
}
```

{% embed url="https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html" %}

**Sortowanie**

Przeanalizujmy poniższe przykłady sortowania, w tym celu została stworzona następująca lista

```java
List<String> strList = new ArrayList<String>();
strList.add("A");
strList.add("C");
strList.add("B");
strList.add("Z");
strList.add("E");
```

W przypadku listy z obiektami np. String, int, duble możemy wykorzystać mechanizm sortowania z biblioteki `Collections`.

```java
Collections.sort(strList);
for(String str: strList) System.out.print(" "+str);
```

Przy bardziej złożonych obiektach, stworzonych przez nas  np. klasa Student

```java
class Student {
    String imie;
    int wiek;
    // ... konstruktor, gettery, settery
}
```

Możemy sortować po określonym parametrze, dla przykładu zaostał stworzona lista studentów

```java
List<Student> studentList= new ArrayList<Student>();
strList.add(new Student("Jan", 23));
strList.add(new Student("Tomek", 24));
strList.add(new Student("Marta", 21));
strList.add(new Student("Ewelina", 22));
strList.add(new Student("Marek", 23));
```

Obiekt listy posiada wbudowaną metodę sortowania ale wymaga podania w jaki sposób sortować np. chcemy posortować po wieku studenta:

```java
studentList.sort((s1, s2) -> s1.getWiek() - s2.getWiek());
```

_Zasada działąnia._ Jeśli wynik jest ujemny -> `s1` jest mniejszy (idzie w lewo). Jeśli dodatni -> `s1` jest większy (idzie w prawo).

W innym przypadku możemy posortować po alfabetycznie po imieniu.

```java
studentList.sort((s1, s2) -> s1.getImie().compareTo(s2.getImie()));
```



### Zadania

1. Zadanie "Kalkulator": Stwórz interfejs funkcyjny `IntegerMath`, który wykonuje operację na dwóch liczbach. Użyj go, aby stworzyć lambdy dla: dodawania, odejmowania i potęgowania (`Math.pow`).
2. Zadanie "Generator": Użyj `Supplier`, aby wygenerować 5 losowych liczb z zakresu 1-100 i umieścić je w liście.
3. Zadanie "Transformacja": Masz listę cen (Double). Użyj `Function`, aby sformatować je do Stringa dodając walutę "PLN" na końcu.

