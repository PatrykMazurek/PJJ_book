# Obiekty i klasy

## Teoria&#x20;

Rozdział 4 - Podstawowe elementy języka Java

### Obiekty i klasy

W języku **Java** klasy stanowią podstawowy budulec programów obiektowych. Klasa to swoisty „szablon” (ang. _blueprint_), który opisuje, jakie dane (pola, czyli atrybuty) oraz zachowania (metody) będą miały tworzone na jej podstawie obiekty. Dzięki klasom można grupować dane i funkcjonalności w logiczne całości, co ułatwia organizację kodu i ponowne wykorzystanie. Obiekty powstałe z klasy są instancjami tej klasy i mogą różnić się wartościami atrybutów, ale zawsze posiadają ten sam zestaw metod.

Java wspiera programowanie obiektowe w pełni, dlatego klasy mogą korzystać z takich mechanizmów jak dziedziczenie, enkapsulacja czy polimorfizm. Pozwala to budować rozbudowane systemy, które są czytelne, łatwiejsze w utrzymaniu i rozszerzalne. Programista może zdefiniować własne klasy, a także wykorzystywać gotowe klasy dostępne w bogatej bibliotece standardowej Javy.

Deklaracja klasy  Person

<pre class="language-java"><code class="lang-java"><strong>public class Person {
</strong>    // Pola (atrybuty)
    private String name;
    private int age;
}
</code></pre>

Aby stworze nowy obiekt typu Person należy użyć słowa kluczowego new, Powoduje to wywołanie konstruktora na obiekcie Person. Jeżeli nie zdefiniujemy konstruktora w klasie Person środowisko Java dostarczy automatycznie konstruktor bez argumentowy.&#x20;

```java
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person();
        Person p2 = new Person();
    }
}
```

### **Konstruktor**

Konstruktor w języku **Java** to specjalna metoda w klasie, która służy do inicjalizacji nowo tworzonych obiektów. Wywoływany jest automatycznie w momencie użycia słowa kluczowego `new` i ma taką samą nazwę jak klasa, ale nie posiada typu zwracanego (nawet `void`). Konstruktor może przyjmować argumenty, aby ustawić początkowe wartości pól obiektu, a jeśli programista nie zdefiniuje własnego, kompilator automatycznie tworzy **konstruktor domyślny** (bezargumentowy). Dzięki konstruktorom można zapewnić, że każdy obiekt danej klasy zostanie poprawnie zainicjalizowany już w chwili utworzenia.

<pre class="language-java"><code class="lang-java"><strong>public class Person {
</strong>    // Pola (atrybuty)
    private String name;
    private int age;
    
     // Konstruktor bez argumentowy
    public Person() {
        System.out.println("Wywołanie konstruktora bez agrumentowego");    }
    
     // Konstruktor argumentowy
    public Person(String name, int age) {
        System.out.println("wywołanie konstruktora z agrumentami");
        this.name = name;
        this.age = age;
    }
}
</code></pre>

Przykład wywołania

```java
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person();
        Person p2 = new Person("Jan", 30);
    }
}
```

### Pola i metody

**pole** - to zmienna przypisana do obiektu, która przechowuje jego dane lub stan.

**metoda** - to zmienna przypisana do obiektu, która przechowuje jego dane lub stan.

**Gettery i Settery**

* **Gettery -** metody zwracające wartość prywatnego pola, zwykle w formie `getPole()`
* **Settery -** metody przyjmujące parametr i ustawiające go do pola, zwykle w formie `setPole()`

```java
public class Person {
    // Pola (atrybuty)
    private String name;
    private int age;
    
    // Konstruktory
    // ...
    // koniec konstruktorów
    
    // metody
    public String getName();
        return this.name;
    }
    
    public void setName(String name){
        this.name = name;
    }
    
    public int getAge(){
        return this.age;
    }
    
    public void setAge(int age){
        this.age = age;
    }
}
```

Zastosowanie powyższych metod

```java
public class Main {
    public static void main(String[] args) {
        Person p1 = new Person();
 
         p1.setName("Tomasz");
         p1.setAge(34);
         
         System.out.println(p1.getName() + " " + p1.getAge());       
    }
}
```

Metoda **`toString()`** w Javie służy do zwracania tekstowej reprezentacji obiektu. Domyślnie każda klasa dziedziczy ją z klasy bazowej `Object`, a jej wynik to zazwyczaj nazwa klasy i adres w pamięci (np. `Person@6f2b958e`). W praktyce jednak bardzo często się ją **nadpisuje (override)**, aby zwracała czytelną i przydatną informację o obiekcie, np. wartości jego pól. Dzięki temu można łatwiej debugować program albo prezentować obiekty użytkownikowi w zrozumiałej formie.



```java
public class Person {
    private String name;
    private int age;

    // konstruktory
    // metody getter i setter

    @Override
    public String toString() {
        return "Osoba: " + this.name + ", wiek: " + this.age;
    }
}
```

Zastosowanie&#x20;

```java
public static void main(String[] args) {
    Person p = new Person("Ala", 20);
    System.out.println(p); // automatycznie wywoła p.toString()
}
```

### Zadania
