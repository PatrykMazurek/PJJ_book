# Wyjątki

### Teoria

Rozdział 11 - Cay S. Horstmann, Gary Cornell, Java Podstawy

### Wyjątki

Wyjątki to mechanizm pozwalający na przechwytywanie błędów w trakcie programu. Zastosowanie wyjątków pozwala na obsłużenie problemów, które mogłyby spowodować zablokowanie programu.

W środowisku Java wyjątki możemy podzielić na dwa rodzaje:

* **Errors** - błędy krytyczne JVM (niebsługiwalne)
* **Exception** - wyjątki aplikacyjne:
  * wyjątki niejawne (unchecked) - głównie błędy programistyczne np. NullPointException, IndexOutOfBundsException.
  * wyjątki jawne (checked) - należy je jawnie obsłużyć przy pomocy `try  / chatch` lub `throws` np. IOException, FileNotFoundException

Jeżeli chcemy przechwycić błąd jawnie poniżej przedstawiony jest przykładowy blok przechwytujący błędy.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Nie dziel przez zero!");
} finally {
    System.out.println("To wykona się zawsze.");
}
```

Powyższy fragment przedstawia blok `try` / `catch` / `finally` który odpowiada za przechwytywanie wyjątków i obsługiwanie ich. Blok `try` zawiera kod, który może powodować wystąpienie błędu. Jeżeli wystąpi błąd, blok `catch` przechwytuje błąd i wyświetla informacje o błędzie i pozwala na dalszą pracę programu. Jeżeli błąd nie wystąpi blok `catch` nie jest uruchamiany. Blok `finally` jest zawsze wykonywany niezależnie od tego czy błąd wystąpi czy nie. Zastosowanie `finally` pozwala na bezpieczne zakończenie fragmentu programu np. zamknięcie dostępu do pliku.

Innym rozwiązaniem jest poinformowanie że na całej metodzie może zostać wyrzucony wyjątek. Deklaracja odbywa się przez dodanie słówka `throws` i rodzaju błędu przy deklaracji metody. Takie rozwiązanie pozwala na ograniczenie bloków `try` / `catch` / `finally` w całej metodzie.

```java
public void readFile(String path) throws IOException {
    // ...
}
```

W powyższym przykładzie informujemy że metoda `readFilel` może wyrzucić wyjątek `IOException`, który odpowiada za błąd wejścia wyjścia.&#x20;

**Ręczne wywoływanie wyjątków**

Czasami można wywołać ręcznie wyjątek informując użytkownika o niewłaściwej akcji czy przekazaniu złego argumentu. służy do tego `throw`. Przykład ręcznego wywołania wyjątku.     &#x20;

```java
throw new IllegalArgumentException("Zły argument!");
```

**Tworzenie własnych wyjątków**

Środowisko Java pozwala na tworzenie własnych wyjątków, co może pomóc przy dokładniejszym określeniu problemu i lepsze dopasowanie komunikatu o błędach w projekcie. Przechwytywanie wyjątków możemy stworzyć dla błędów obsługiwanych (checked) i dla błędów nieobsługiwanych (unchecked). Przykład własnych błędów.

Przykład wyjątku (checked)

```java
public class MyCheckedException extends Exception {
    public MyCheckedException(String message) {
        super(message);
    }
}
```

Przykład wyjątku (unchecked)

```java
 public class MyUncheckedException extends RunetimeException {
    public MyUncheckedException(String message) {
        super(message);
    }
}   
```

W powyższych przykładach zostały stworzone dwie klasy, które dziedziczą po klasie `Exception` i `RunetimeException`. W zależności od typu wyjątku jaki chcemy obsługiwać wybieramy odpowiednią klasę i dostarczamy komunikat, który chcemy wyświetlić użytkownikowi.  Przykład zastosowania wyjątku w metodzie.

```java
public void doSomething() throws MyCheckedException {
    throw new MyCheckedException("Wystąpił błąd!");
}
```

**Zadania**

1. Napisz program, który wczytuje dwie liczby całkowite od użytkownika, następnie dzieli pierwszą przez drugą. Zapewnij bezpieczeństwo w przypadku gdy użytkownik będzie chciał podzielić przez zero oraz zastosuj wyjątek (`NumberFormatException`) gdy będzie błędny format liczby.
2. Stwórz metodę `int getCharIndex(String text, car ch)`, Zadaniem metody jest zwrócenie pierwszego indeksu pod, którym występuje podany znak. Jeżeli znak nie występuje to wywołaj  `IllegalArgumentException`. Jeżeli tekst jest `null` zwróć wyjątek `NullPointerException`. &#x20;
3.  Stwórz klasę wyjątku `AgeTooLowException`, dziedziczącą po `Exception`. Następnie stwórz metodę

    `void registerUser(int age) throws AgeToLowException`

    Jeżeli wiek przekazany do metody będzie mniejszy niż 18 żuć wyjątkiem stworzonym przez Ciebie z komunikatem "Użytkownik musi być pełnoletni". Rozwiązanie przetestuj w `Main` obsługując wyjątki i wypisując komunikat. &#x20;
