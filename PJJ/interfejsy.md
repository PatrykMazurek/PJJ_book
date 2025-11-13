# Interfejsy

### Teoria

Rozdział 6 - Cay S. Horstmann, Gary Cornell, Java Podstawy

### Interfejsy

W języku Java interfejsy nie są klasą, ale zestawem wymagań co klasa implementująca dany interfejs powinna zawierać. Interfejsy zawierają definicję metody ale bez jej implementacji. to jak zostanie ona zaimplementowana powstawiają klasie.&#x20;

Interfejsy zawsze są publiczne, więc nie wymagane jest dodawanie słówka public przed nazwą metody, w interfejsie może być zdefiniowana jedna lub więcej metod, czasami spotykana jest deklaracja stałej.&#x20;

Klasa może implementować wiele interfejsów, co pozwala na pisanie bardziej elastycznego kodu. Przykład implementacji interfejsu.

```java
public interface Animal {
    
    void voice();
    
}
```

implementacja w klasie

```java
public class Cat implements Animal{
    @Override
    public void voice() {
        System.out.println("Mau!");
    }
}

public class Dog implements Animal{
    @Override
    public void voice() {
        System.out.println("Hu! Hu!");
    }
}

```

W powyższym przykładzie przedstawiono sposób implementacji interfejsu w klasie. Aby implementować wybrany interfejs należy po nazwie klasy dodać słówko `implements` i  podać nazwę wybranego interfejsu.&#x20;

**Metody domyślne i stałe w interfejsach**

Metody domyślne pozwalają na implementacji metody w interfejsie, dzięki temu można zastosować domyślne rozwiązanie w pierwszej implementacji w klasie. Metody domyślne można nadpisywać w klasie ale nie jest to wymagane.

```java
public interface Animal {
    
    void voice();
    
    default void eat(String food) {
        System.out.println(getName() + " is eating " + food + ".");
    }

    default void sleep() {
        System.out.println(getName() + " is sleeping...");
    }
    
    String getName();
}
```

&#x20;W powyższym przykładzie mamy zaimplementowane dwie metody domyślne (eat, sleep) dzięki czemu nie musimy wykonywać implementacji w klasie.&#x20;

**Metody prywatne**

Metody prywatne mogą być tylko wywoływane w definicji interfejsu, czyli mogą być tylko wykonywane z metodami domyślnymi. Zastosowanie metod prywatnych pozwala na usunięcie często powtarzającego się kodu w wielu miejscach.

```java
public interface Animal {
    
    void voice();
    
    default void eat(String food) {
        System.out.println(getName() + " is eating " + food + ".");
        logAction("Eating");
    }

    default void sleep() {
        System.out.println(getName() + " is sleeping...");
        logAction("Sleeping");
    }
    
    private void logAction(String action) {
        System.out.println("[LOG] " + getName() + " - action: " + action);
    }
    
    String getName();
}
```

W powyższym przykładnie została dodana prywatna metoda, która tworzy logi z każdej wywołanej akcji. Metoda `logAction(String action)` może być tylko wywoływana z poziomu interfejsu.

Przykład implementacji powyższych przykładów w klasie Dog

```java
public class Dog implements Animal {
    private String name;
    
    public Dog(String name) {
        this.name = name;
    }
    
    @Override
    public void voice() {
        System.out.println(name + " says: Woof woof!");
    }
    
    @Override
    public String getName() {
        return name;
    }
}
```

**Dziedziczenie interfejsów**

Interfejsy podobnie jak lasy mogą być dziedziczone z tą różnicą że interfejsy mogą dziedziczyć po wielu interfejsach. Dziedziczenie pozwala nam na pisanie bardziej elastycznego kodu&#x20;

```java
public interface Pet extends Animal {
    void play();

    default void feed() {
        System.out.println(getName() + " is being fed with pet food.");
    }
}
```

```java
public interface WildAnimal extends Animal {
    void hunt();
    default void flee() {
        System.out.println(getName() + " is fleeing into the wilderness!");
    }
}
```

Implementacja powyższych interfejsów w klasie&#x20;

```java
public class Dog implements Pet {    
    private String name;
    
    public Dog(String name) {
        this.name = name;
    }
    
    @Override
    public void voice() {
        System.out.println(name + " says: Woof!");
    }
    
    @Override
    public String getName() {
        return name;
    }
    
    @Override
    public void play() {
        System.out.println(name + " is playing with a ball!");
    }
}
```

### Zadania

1.  Twoim zadaniem jest zaprojektowanie i zaimplementowanie systemu powiadomień, który umożliwia wysyłanie różnych typów komunikatów do użytkowników. W systemie mogą występować różne kanały powiadomień (np. e-mail, SMS, powiadomienia push), które posiadają wspólne cechy, ale różnią się sposobem wysyłania wiadomości. Stwórz interfejs `Notification`, który będzie zawierał deklarację metody `send()`.&#x20;

    Stwórz przykładowe klasy np. `EmailNotification`, `SMSNotification`, `PushNotification` , które będą implementować interfejs Notification. Każda z klas będzie powinna zawierać prywatne pola **recipient, message.** Kazda z klas powinna implementować metodę send() w zależności w jaki sposób wysyła wiadomość np. `EmailNotification` w metodzie `send()` powinna wyświetlać w konsoli „Wysłano e-mail do \<recipient> : \<message>”.
2. Zadanie 1 z części Dziedziczenie proszę przerobić wykorzystując interfejsy i stwórz kilka klas, które będą reprezentować zwierzęta, w każdej klasie implementuj wymagane metody w sposób odpowiedni dla danej klasy.
3.  Stwórz system opisujący pojady, które mogą pełnić różne funkcje. Stwórz następujące interfejsy:

    `LandVehicle` zawierający metody: **void driveForward(double speed), void applyBrakes()**

    `WaterVehicle` zawierający metody: **void navigateOnWater(double headingDeg, double speed),  void anchor(), void removeAnchor()**

    `AirVehicle` zawierający metody: **void takeOff(), void land().**

    Stwórz dwie klasy `AmphibousVehicle` i `FlyingCar`, które będą implementować odpowiednie interfejsy.  Dodatkowo klasa `AmphibousVehicle` powinna zawierać metody **void switchToWaterMode(), void switchToLandMode()** a klasa `FlyingCar` powinna zawierać metody **void switchToDriveMode(), void switchToFlightMode()**. W klasach `AmphibousVehicle` i `FlyingCar` stwórz konstruktor i niezbędne pola (jeżeli są wymagane).
4. Bazując na zadaniu 3 dodaj dodatkowe interfejsy  `Vehicle`, `AmphibousVehicle` i `FlyingCar`.  Interfejs `Vehicle` zawiera metody: **void start(), void stop(), double getSpeed(), double getFulLevel()**. Interfejsy `AmphibousVehicle` i `FlyingVehicle` powinny zawierać metody, które zostały zdefiniowane w klasie. Stwórz odpowiednią hierarchie interfejsów, tak aby w klasie implementować jak najmniej interfejsów. Przetestuj rozwiązania tworząc klasy np. Car, Bus, Ship, airpalne, Amphibian. Klasy powinny zawierać niezbędne pola i metody z interfejsów.
5.

