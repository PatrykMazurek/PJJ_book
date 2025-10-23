# Dziedziczenie

### Teoria

Rozdział 5 - Java Podstawy, Cay S. Horstmann

### Dziedziczenie

Dziedziczenie w Javie to mechanizm, który pozwala jednej klasie (podrzędnej) przejmować pola i metody innej klasy (nadrzędnej), dzięki czemu można ponownie wykorzystywać kod. Umożliwia to tworzenie hierarchii klas, gdzie klasy potomne rozszerzają lub modyfikują zachowanie klas bazowych.

Przykład dziedziczenia:

**Klasa Person**

```java
public class Person {
    
    private String name;
    private String lastname;
    private int age;
    
    public Person(String name, String lastname, int age){
        this.name = name;
        this.lastname = lastname;
        this.age = age;
    }

    public void setName(String name) { this.name = name; }
    public String getName() { return name; }

    public void setLastname(String lastname) { this.lastname = lastname; }
    public String getLastname() { return lastname; }

    public void setAge(int age) { this.age = age; }
    public int getAge() { return age; }
}
```

**Klasa Student**

```java
public class Student extends Person{

    private String studentID;

    public Student(String name, String lastname, int age, String id) {
        super(name, lastname, age);
        this.studentID = id;
    }

    public void setStudentID(String studentID) { this.studentID = studentID; }
    public String getStudentID() { return studentID; }
}
```

W powyższym przykładzie użyliśmy słówka `extends` aby wskazać że klasa `Student` będzie dziedziczyć wszystkie pola i metody po klasie `Person`. W tej sytuacji nie musimy tworzyć dwóch obiektów tylko wystarczy że stworzymy obiekt `Student` aby mieć dostęp do pół klasy `Person`. Przykład.

W konstruktorze klasy `Student` używane jest słówko `super`, słówko to pozwala na wywołania konstruktorów i metod z nadklasy. Jeżeli słówko jest wywoływane w konstruktorze powinno być jako pierwsze i wywołuje odpowiedni konstruktor (argumentowy lub bezargumentowy).

```java
public class Main {
    public static void main(String[] args) {
        
        // stworzenie obiektu Person
        Person p = new Person("Jak", "Kowalski", 34);
        System.out.println(p.getName());
        
        // stworzenie obiektu Student
        Student s = new Student("Ewa", "Nowak", 23, "p00012");
        System.out.println(s.getName());
        System.out.println(s.getStudentID());
    }
}
```

W powyższym przypadku stworzyliśmy dwa obiekty `Person` i `Student`. Obiekt `Student` przez to że dziedziczy po klasie `Person` ma dostęp do takich metod jak np. `getName()`.

### **Nadpisywanie metod (@override)**

W niektórych sytuacja klasa bazowa posiada metodę, którą chcemy nadpisać w klasie pochodnej. w tym celu dla zachowania czystości kodu dopisujemy przed tą metodą słówko `@override`, nie jest to wymagane ale zalecane. Poniżej przykład nadpisywania metod.

**Klasa Person**

```java
public class Person {

    private String name;
    private String lastname;
    private int age;

    public Person(String name, String lastname, int age){
        this.name = name;
        this.lastname = lastname;
        this.age = age;
    }

    // gettery, settery

    public void present(){
        System.out.println("Imię: " + this.name + " " + " Nazwisko: " + this.lastname);
        System.out.println("wiek: " + this.age);
    }
}

```

**Klasa Student**

```java
public class Student  extends Person{

    private String studentID;

    public Student(String name, String lastname, int age, String id) {
        super(name, lastname, age);
        this.studentID = id;
    }

    public void setStudentID(String studentID) { this.studentID = studentID; }
    public String getStudentID() { return studentID; }

    @Override
    public  void present(){
        super.present();
        System.out.println("student nr " + this.studentID);
    }
}
```

W powyższym przykładzie w klasie `Person` została zdefiniowana metoda `persent()`, której zadaniem jest przedstawianie się. W klasie `Student` została nadpisana metoda `present()`, w której poza tym że wykorzystujemy metodę z klasy bazowej to dodajemy dodatkową informację o numerze studenta. Aby wykorzystać metody z klasy bazowej musimy w klasie pochodnej zastosować słówko `super` przed wywołaniem metody.

### Klasa Abstrakcyjna

W języku Java klasy mogą być zwykłe lub abstrakcyjne.\
Klasy abstrakcyjne są szablonami, które nie mogą być bezpośrednio tworzone (instancjonowane), ale mogą zawierać wspólne elementy dla innych klas.

Klasa abstrakcyjna w definicja zawiera słowo kluczowe `abstract`. Taka deklaracja powoduje pewien problem ponieważ taka klasa nie może być utworzona (`new` jest niedozwolone). Klasa abstrakcyjna może zawierać pola, zwykłe metody ( z implementacją), metody abstrakcyjne (tylko definicja), Każda klasa, która dziedziczy po klasie abstrakcyjnej musi zaimplementować metody abstrakcyjne, chyba że sama jest klasą abstrakcyjną.

**Przykład klasy abstrakcyjnej**

```java
public abstract class Animal {

    String name;

    public Animal(String name) {
        this.name = name;
    }

    // metoda zwykła (z implementacją)
    public void introduceYourself() {
        System.out.println("Jestem zwierzęciem o imieniu " + name);
    }

    // metoda abstrakcyjna (bez implementacji)
    public abstract void voice();
}
```

**Dziedziczenie po klasie abstrakcyjnej**

Klasa, która dziedziczy po klasie abstrakcyjnej dodatkowo musi implementować wszystkie metody abstrakcyjne klasy nadrzędnej.

```java
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    @Override
    public void voice() {
        System.out.println("Hau! Hau!");
    }
}

public class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }

    @Override
    public void voice() {
        System.out.println("Miau!");
    }
}
```

**Przykład użycia**

```java
public class Main {
    public static void main(String[] args) {
        // Animal a = new Animal("Burek"); – nie można tworzyć obiektu klasy abstrakcyjnej!

        Dog dog = new Dog("Reksio");
        Cat cat = new Cat("Filemon");

        dog.introduceYourself();
        dog.voice();

        cat.introduceYourself();
        cat.voice();
    }
}
```

W wyniku wykonania powyższego kodu zostaną utworzone dwa obiekty typu `Dog` i `Cat`. Każdy z nich dziedziczy metodę `introduceYourself()` za pomocą, której przedstawia się. Oraz implementuje metodę `voice()`, która powoduje że dany obiekt daje głos. poniżej przedstawiony jest wynik poniższego kodu

```
Jestem zwierzęciem o imieniu Reksi
Hau Hau!
Jestem zwierzęciem o imieniu Filemon
Miau!
```

### Polimorfizm

Polimorfizm w języku Java to jedna z podstawowych zasad programowania obiektowego, która pozwala różnym obiektom reagować w odmienny sposób na to samo wywołanie metody. Zachowanie to pozwala na tworzenie kodu bardziej elastycznego, i bazującego na typach ogólnych, a mimo to poprawnie wywołuje metody właściwe dla konkretnego typu obiektu w czasie działania programu.

```java
public class Main {
    public static void main(String[] args) {
        // Animal a = new Animal("Burek"); – nie można tworzyć obiektu klasy abstrakcyjnej!

        Animal dog = new Dog("Reksio");
        Animal cat = new Cat("Filemon");

        dog.introduceYourself();
        dog.voice();
        cat.introduceYourself();
        cat.voice();
        
        Animal[] groupAnimal = {
            new Cat("Filemon"), 
            new Dog("Reksio"), 
            new Dog("Pimposz")
            };
        
    }
}
```

W powyższym przypadku klasy `Dog` i `Cat` dziedziczą po klasie abstrakcyjnej `Anima.` To rozwiązanie pozwala na wykorzystanie ogólnego typu `Animal` do przechowywanie obiektów klas `Dog` i `Cat` i jednoczenie zapewnia odpowiednie działanie metod dla odpowiednich obiektów.

### Zadania

1.  Napisz hierarchię klas, która symuluje różne typy zwierząt w zoo.\
    Każde zwierzę potrafi się przedstawić i wydawać dźwięki — ale każde robi to inaczej. Stwórz klasę bazową `Animal` z polami **name** i **age** oraz metody

    `introduceYourself()` - wypisuje imię i weki

    `voice()` i `eat()` - które domyślnie wypisują "głos" i "jedzenie".

    Stwórz kilka klas pochodnych, które będą reprezentować zwierzęta mieszkające w zoo. nadpisz metody `voice()` i `eat()` dostosowując je do odpowiednich zwierząt. Wyświetl w pętli informacje o zwierzętach mieszkających w zoo.
2. Stwórz system, który potrafi obliczać pola różnych figur geometrycznych.\
   Każda figura ma nazwę i sposób obliczania pola — ale sposób ten zależy od typu figury. Stwórz klasę abstrakcyjną `Figura`, która będzie zawierać prywatne pola **nazwa, obwod, pole**, konstruktor ustawiający nazwę oraz dwie metody abstrakcyjne `void obliczPole()` i `void obliczObwod()`. oraz jedną metodę zwykłą `wyswietlInfo()`. Stwórz klasy potomne, które będą dziedziczyć po klasie Figura. Wykorzystaj tablicę `Figura[]` do przetestowania powyższego rozwiązania.
3.  Korzystając z zadania 4 z lekcji Obiekty i Klasy stwórz klasę `Employee` jako klasę abstrakcyjną. Dodaj metodę abstrakcyjną `CalculateSalaries()`, która w zależności od klasy będzie obliczać pensje pracownika. Stwórz klasy pochodne, które będą reprezentować różne formy zatrudnienia np.&#x20;

    `FullTimeEmployee`  - posiadający stałe wynagrodzenie

    `ContractEmployee` - posiadający stawkę razy liczba godz.&#x20;

    `Intern` - Jako pensja jest stypendium czyli stałą kwota wynagrodzenia.

    Przetestuje działanie klasy tworząc tablicę lub listę pracowników zatrudnionych w różnych formach zatrudnienia.
