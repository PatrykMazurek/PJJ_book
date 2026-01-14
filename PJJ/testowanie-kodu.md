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
2.  Rozszerz klasę `Calculator` z `add(int a, int b)` o `history` (lista wyników). Napisz testy z `@BeforeEach` (czyszczenie historii) i `@AfterEach` (logowanie wyników).

    Dodaj `private List<Integer> history = new ArrayList<>();` i `addHistory(int result)`.\
    **Pytania:**

    1. Co się stanie bez `@BeforeEach`?&#x20;
    2. Czy `@AfterEach` wykona się przy failu?
