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

3.  Anonimowa klasa (anonymous class) &#x20;



**Wady klas wewnętrznych i kiedy stosować**



**Zadania**



**Dodatkowe materiały**&#x20;
