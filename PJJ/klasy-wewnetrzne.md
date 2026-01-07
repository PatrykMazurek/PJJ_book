# Klasy wewnętrzne

**Klasy wewnętrzne** to po prostu klasy zdefiniowane wewnątrz innej klasy. Stosowanie tego typu rozwiązań pozwala na logiczne grupowanie powiązanych encji, zwiększania enkapsulacji i upraszczania kodu w specyficznych kontekstach. Klasy wewnętrzne mają dostęp do metod prywatnych z klasy zewnętrznej. Wyróżniamy następujące rodzaje klas:&#x20;

1.  **Zagnieżdżone statyczne (static nested class)**

    Klasa, tylko zagnieżdżona w innej klasie dla zachowania porządku nazw oraz zachowania logicznej części klasy zewnętrznej.

    **cechy**:

    &#x20;\- nie posiada referencji do istniejącej klasy zewnętrznej

    &#x20;\- może używać tylko statycznych pól/metod klasy zewnętrznej&#x20;

    **Przykład**:

```java
public class OuterStatic {
    static class Nested {
        void hello() {
            System.out.println("Hello from static nested");
        }
    }

    public static void main(String[] args) {
        // tworzenie NIE wymaga instancji OuterStatic
        OuterStatic.Nested n = new OuterStatic.Nested();
        n.hello();
    }
}
```

2.  **Wewnętrzne niestatyczne (inner class)**&#x20;

    Klasa związana z konkretną instancją klasy zewnętrznej, w sytuacji kiedy klasa wewnętrzna ma logiczny sens w połączeniu z klasą zewnętrzną np. iterator, widok, kontroler stanu.

    **Cechy**:

    &#x20;\- ma dostęp do wszystkich pól/metod klasy zewnętrznej nawet tych prywatnych)

    &#x20;\- tworzenie wymaga obiektu `outer.new Inner()`.

    **Przykład**:

```java
public class OuterInner {
    private int counter = 0;

    class Inner {
        void inc() {
            counter++;
            System.out.println("counter=" + counter);
        }
    }

    public static void main(String[] args) {
        OuterInner outer = new OuterInner();

        // tworzenie WYMAGA instancji OuterInner
        OuterInner.Inner inner = outer.new Inner();
        inner.inc();
        inner.inc();
    }
}
```

3.  **Lokalna klasa w metodzie (mtod class)**

    Klasa definiowana w metodzie lub bloku if / for. Przeznaczona do małych pomocniczych obiektów używanych w konkretnym miejscu.

    **Cechy**:

    &#x20;\- może korzystać z pól klasy zewnętrznej

    &#x20;\- ograniczona widoczność do funkcji lub danego bloku

    &#x20;\- może korzystać ze zmiennych lokalnych jeżeli są typu **final**

    **Przykład**:&#x20;

```java
public class OuterLocal {

    public void run(String prefix) {
        int x = 10; // musi być effectively final (nie zmieniaj potem x ani prefix)

        class LocalPrinter {
            void print() {
                System.out.println(prefix + " x=" + x);
            }
        }

        LocalPrinter lp = new LocalPrinter();
        lp.print();
    }

    public static void main(String[] args) {
        new OuterLocal().run("INFO:");
    }
}
```

3.  **Anonimowa klasa (anonymous class)**&#x20;

    implementacja "jednorazowa" interfejsu lub klasy bazowej, najczęściej wykorzystywana do implementacji interfejsów lub nasłuchiwania na jakieś wydarzenie (akcje związane z GUI)

    **Cechy**

    &#x20;\- bez nazwy, tworzona od razu np. `new Inferface() {...}`

    &#x20;\- przydatna przy nadpisywaniu metod lub przy użyciu klas abstrakcyjnych.

    **Przykład**:

```java
ublic class OuterAnonymous {

    interface Greeter {
        void greet();
    }

    public static void main(String[] args) {
        Greeter g = new Greeter() {
            @Override
            public void greet() {
                System.out.println("Hello from anonymous class");
            }
        };

        g.greet();
    }
}
```

**Wady klas wewnętrznych i kiedy stosować**

Wady klas wewnętrznych to przede wszystkim pogorszona czytelność kodu, zwłaszcza gdy w jednej klasie znajduje się wiele zagnieżdżonych definicji. Klasy wewnętrzne są też silnie powiązane z klasą zewnętrzną, co może prowadzić do problemów z pamięcią: niestatyczna klasa wewnętrzna przechowuje referencję do obiektu klasy zewnętrznej, więc długie przetrzymywanie obiektu klasy wewnętrznej może nieumyślnie uniemożliwić zwolnienie obiektu zewnętrznego (tzw. wyciek pamięci). Dodatkowo klasy anonimowe i lokalne mogą utrudniać debugowanie, ponieważ w śladach stosu pojawiają się mało czytelne nazwy (np. `Outer$1`).

**Zadania**

1.  Stwórz klasę `Samochod`, która zawiera klasę wewnętrzną `Silnik`, oraz prywatne pola `marka`, `model`, `czySilnikUruchomiony`, `prendkosc`. Klasa `Silnik` powinna mieć prywatne pole `moc` (int), `czyPracuje` oraz metody `uruchom()`, `zgas()`, `pobierzMoc()`. W klasie `Samochod` dodaj metody&#x20;

    &#x20;\- `uruchomSilnik()`, która tworzy instancję `Silnik` jeżeli jeszcze nie istniej i zwraca prędkość,

    &#x20;\- `zgaśSilnik()` metoda, która usuwa ślinik i ustawia prędkość na 0.&#x20;

    Zwróć uwagę na walidację danych, nie można ustawić mocy < 0 Zwróć uwagę na konieczność posiadania instancji klasy zewnętrznej do tworzenia klasy wewnętrznej.
2. Rozwijając klasę `Samochod`, dodaj statyczną klasę zagnieżdżoną `KoloryNadwozia` z metodą `losowyKolor()`, która zwraca losowy kolor z tablicy (np. "czerwony", "niebieski"). Użyj tej klasy w metodzie statycznej klasy `Samochod`, aby przypisać kolor bez tworzenia instancji `Samochod`. Porównaj różnice w dostępie do pól klasy zewnętrznej.
3. Stwórz interfejs `Obserwator` z metodą `zaktualizowano(String dane)`. W klasie `SerwerDanych` utwórz listę obserwatorów i metodę `dodajObserwatora(Obserwator o)`. Użyj klas anonimowych do dodania dwóch różnych obserwatorów: jeden wypisuje dane na konsolę, drugi zapisuje do pliku. Symuluj aktualizację danych i sprawdź działanie.
4. Napisz klasę `PasswordService`, która będzie zawierała metodę `boolean isStrong(String password)`. Wewnątrz tej metody zdefiniuj lokalną klasę (local class) o nazwie `Rules`, odpowiedzialną za sprawdzanie, czy podane hasło spełnia wymagania bezpieczeństwa. Hasło ma zostać uznane za silne, jeśli ma co najmniej 8 znaków, zawiera przynajmniej jedną wielką literę, przynajmniej jedną cyfrę oraz przynajmniej jeden znak specjalny spośród `!@#$%^&*`. Lokalna klasa `Rules` powinna udostępniać metodę `boolean checkAll()`, która wykonuje wszystkie sprawdzenia i zwraca wynik. W rozwiązaniu wykorzystaj fakt, że lokalna klasa może odwoływać się do zmiennej `password` przekazanej do metody, pamiętając jednocześnie o zasadzie, że zmienne lokalne używane wewnątrz klasy lokalnej muszą być `final` lub „effectively final” (czyli nie mogą być później modyfikowane). Na koniec przygotuj metodę `main`, w której przetestujesz działanie rozwiązania na czterech przykładowych hasłach — dwóch słabych i dwóch silnych — i wypiszesz wynik w postaci informacji, czy dane hasło jest silne.

**Dodatkowe materiały**&#x20;

{% embed url="https://dev.to/dhanush9952/java-inner-classes-and-nested-classes-39a6" %}

{% embed url="https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html" %}

{% embed url="https://codegym.cc/pl/groups/posts/pl.1031.klasy-wewntrzne-java" %}
