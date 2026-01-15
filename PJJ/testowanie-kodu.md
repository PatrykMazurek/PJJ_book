# Testowanie kodu

### JUnit Test

JUnit - Jeden z najpopularniejszych frameworków to tworzenie i uruchamiania testów jednostkowych w środowisku Java.&#x20;

Umożliwia weryfikowanie poprawności działania małych fragmentów kodu (np. metod, lub klas) poprzez zapewnieni gotowych mechanizmów do testowania.

JUnit pozwala na tworzenie prostych testów jednostkowych bez dodatkowych konfiguracji.

**Asercje (Assertions)** Pozwalają na weryfikowanie oczekiwanych wyników w testach:

* `assertEquals(expected, actual)`
* `assertTrue(condition)`
* `assertFalse(condition)`
* `assertNotNull(object)`
* `assertThrows(exceptionClass, executable)`

**Anotacje** Oznaczają metody testowe, pomagają definiować cykl życia testu:

* `@Test` – oznacza metodę jako testową.
* `@BeforeEach`, `@AfterEach` – metody uruchamiane przed i po każdym teście.
* `@BeforeAll`, `@AfterAll` – uruchamiane jednorazowo przed/po wszystkich testach.
* `@Disabled` – pomijanie testu.

### Przygotowanie testu&#x20;

**Dodanie do środowiska**&#x20;

W przypadku niektórych środowisk IDE JUnit jest domyślnie dodany. W sytuacji kiedy nie mamy JUnit możemy skorzystać z dodania adnotacji do pliku Maven w naszym projekcie.

```
<dependencies>
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.2</version>
    <scope>test</scope>
  </dependency>
</dependencies>

<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>3.2.5</version>
    </plugin>
  </plugins>
</build>
```

Tworzymy klasę, która będzie testowana.

```java
public class Calculator {

    public int add(int a, int b) {
        return a + b;
    }
}
```

Następnie należy przygodowa test

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class CalculatorTest {

    @Test
    void shouldAddTwoNumbers() {
        // given
        Calculator calculator = new Calculator();
        // when
        int result = calculator.add(2, 3);
        // then
        assertEquals(5, result, "2 + 3 powinno dać 5");
    }
}
```

Adnotacje `@BeforeEach` i `@AfterEach` w JUnit służą do zarządzania cyklem życia testów – uruchamiają się przed i po każdej metodzie testowej. Są idealne do inicjalizacji obiektów i sprzątania zasobów w materiałach dydaktycznych

Metoda z `@BeforeEach` wykonuje się automatycznie przed każdym testem `@Test`, np. do tworzenia świeżej instancji klasy testowanej.

Metoda z `@AfterEach` uruchamia się po każdym teście, np. do zwalniania zasobów jak pliki czy połączenia bazodanowe.

Kolejność stosowania to: `@BeforeEach` → `@Test` → `@AfterEach`

**Zastosowanie takich adnotacji**  &#x20;

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class CalculatorTest {

    private Calculator calculator;

    @BeforeEach
    void setUp() {
        calculator = new Calculator(); 
    }
    @Test
    void shouldAddPositiveNumbers() {
        assertEquals(7, calculator.add(3, 4));
    }
    @Test
    void shouldAddNegativeNumbers() {
        assertEquals(-5, calculator.add(-2, -3));
    }
}
```

#### Parametryzowanie testów <a href="#parametryzowanie-testow" id="parametryzowanie-testow"></a>

Używając `@ParameterizedTest` pozwala na efektywne testowanie różnych przypadków danych wejściowych, co znacznie poprawia pokrycie testami i czytelność testowego kodu.

**Źródła parametryzowania testów:**

* `@EnumSource`: generowanie wartości testowych z enumów.
* `@MethodSource`: źródłem danych jest dedykowana metoda.
* `@CsvFileSource`: dane są pobierane z pliku CSV.

Przykład takiego testu



```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;

import static org.junit.jupiter.api.Assertions.assertEquals;

class CalculatorParamTest {

    private final Calculator calculator = new Calculator();

    @ParameterizedTest(name = "{0} + {1} = {2}")
    @CsvSource({
            "1,   2,   3",
            "0,   0,   0",
            "-1,  5,   4",
            "-3, -7, -10"
    })
    void shouldAddNumbers(int a, int b, int expected) {
        assertEquals(expected, calculator.add(a, b));
    }
}
```

Zadania

1. Stwórz klasę `StringUtils` z metodami `isPalindrome(String)` i `reverse(String)`. Napisz 4 testy w `StringUtilsTest` używając `@Test` i `assert*`.
2.  Stwórz klasy `Calculator`, która będzie posiadać następujące metody:

    1. `add(int a, int b)` – zwraca sumę dwóch liczb.
    2. `divide(int a, int b)` – zwraca wynik dzielenia. Jeśli `b` wynosi 0, rzuca wyjątek `ArithmeticException`.
    3. `isEven(int n)` – zwraca `true`, jeśli liczba jest parzysta, i `false` w przeciwnym razie.

    Stwórz testy sprawdzające klasę `Calculator`, testy mają sprawdzić:

    1. Sprawdź poprawność dodawania dla liczb dodatnich i ujemnych.
    2. Sprawdź poprawność dzielenia liczb całkowitych.
    3. Kluczowe: Użyj `assertThrows`, aby sprawdzić, czy dzielenie przez 0 rzuca odpowiedni wyjątek.
    4. Przetestuj metodę `isEven` dla liczb parzystych, nieparzystych oraz dla zera.
3.  Stwórz klasy `ShoppingCart`, która będzie symulować koszyk zakupowy i będzie posadać następujące metody:

    1. `addItem(String item, double price)` – dodaje przedmiot do listy i zwiększa sumę koszyka. Cena nie może być ujemna (powinien polecieć wyjątek).
    2. `removeItem(String item)` – usuwa przedmiot i zmniejsza sumę. Jeśli przedmiotu nie ma, nic nie robi.
    3. `getTotalPrice()` – zwraca aktualną wartość koszyka.
    4. `clear()` – czyści koszyk.

    Stwórz testy sprawdzające klasę `ShoppingCart`, testy mają sprawdzić:

    1. Użyj adnotacji `@BeforeEach` do inicjalizacji pustego koszyka przed każdym testem.
    2. Sprawdź, czy dodanie przedmiotów poprawnie aktualizuje sumę (`assertEquals` z deltą dla liczb zmiennoprzecinkowych).
    3. Sprawdź, czy próba dodania przedmiotu z ujemną ceną rzuca wyjątek.
    4. Zweryfikuj, czy po wywołaniu `clear()` lista przedmiotów jest pusta, a suma wynosi 0.0.
