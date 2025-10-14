# String i tablice

## Teoria

Rozdział 2 - Podstawowe elementy języka Java

Rozdział 3 - Podstawowe elementy języka Java

### Klasa String

Obiekty String w języku Java jest niemodyfikowalny, czyli jeżeli zostanie utworzony to modyfikacja polega na utworzeniu nowego obiektu.

Praca z klasą String

```java
String text = "";
String text2 = "Dowolny tekst";
```

**Łączenie stringów (Konkatenacja)**

W Javie, podobnie jak w większości innych języków programowania, można łączyć (konkatenować)\
łańcuchy za pomocą znaku `+`.

```java
String tekst1 = "PG";
String tekst2 = "13";
String caly = tekst1 + tekst2;
```

W wyniku otrzymamy nową zmienną z wartością `PG13`, zauważ że nowy tekst nie posiada znaków spacji pomiędzy dwoma łańcuchami. Znak `+` łączy dwa łańcuchy w takiej kolejności, w jakiej zostały podane, nic w nich nie zmieniając.

W środowisku Java pozwala na wykonanie poniższej linijki kodu i jest to poprawne:

```java
System.out.println("Odpowiedź brzmi " + answer);
```

**Porównywanie łańcuchów tekstowych**

Do porównywania, czy dwa łańcuchy są identyczne, służy metoda `equals()`

```java
tekst1.equale(tekst2)
```

Metoda zwróci wartość `true` jeżeli tekst1 i tekst2 są identyczne, lub `false` w przeciwnym przypadku. Metoda porównuje łańcuchy znaków z pominięciem wielkości liter. Nie zalecane jest stosowanie `==!` i `==` do porównywania znaków, może to powodować błąd, którego będzie ciężko z identyfikować.

**Przykładowe metody na klasie String**

* `substring(int startIndex, int endIndex)` - Zwraca nowy łańcuch składający się ze wszystkich znaków znajdujących się na pozycjach od `startIndex` do końca łańcucha albo do `endIndex - 1`.
* `replace(CharSequence oldString, CharSequence newString)` - Zwraca nowy łańcuch, w którym wszystkie łańcuchy `oldString` zostały zastąpione łańcuchami `newString`. Jako obiekt `CharSequence` można podać `String` lub `StringBuilder`.
* `trim()` - Usuwa wszystkie białe znaki z początku i końca łańcucha, zwracając jako wynik nowy łańcuch.
* `length()` - Zwraca długość łańcucha znaków.
* Więcej metod można znaleźć w dokumentacji kasy [String](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)

### Klasa StringBuilder

Obiekt `String` jest niemodyfikowalny (immutable), co w przypadku modyfikacji łańcucha znaków (`+`, `concat()`) przez wiele mniejszych łańcuchów znaków może być kosztowne pamięciowo.

Rozwiązaniem problemu modyfikacji obiektu String jest klasa StringBuilder. Aby rozpocząć składanie łańcucha znaków musimy utworzyć nowy obiekt `builder` klasy `StringBuilder`

```java
StringBuilder builder = new StringBuilder();
```

W tym momencie możemy dodawać, wstawiać lub edytować nasz łańcuch znaków. Przykładowe metody dla klasy StringBuilder:

* `append(str)` - Dodanie pojedynczego znaku lub łańcucha znaków
* `insert(int offset, String str)` - Wstawianie pojedynczego znaku lub łańcucha znaków na pozycji offest.
* `delete(int startIndex, int endIndex)` - Usuwanie znaków znajdujących się na pozycjach `startIndex` i `endIndex - 1`.
* Więcej przydatnych metod można znaleźć w dokumentacji klasy [StringBuilder](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html).

Po złączeniu łańcucha znaków pozostaje nam zwrócić wynik do obiektu `String` wykonując metodę `toString()`.

```java
String completedString = builder.toString();
```

### Tablice jedno i dwuwymiarowe

Tworzenie tablic jedno wymiarowych `typ[] nazwa = typ[rozmiar];`

`int[] number = new int[10];`

Dostęp do poszczególnych elementów tablicy: `nazwa[idx]` gdzie `idx` to pozycja z tabeli liczona od zera.

```java
number[4] = 0;
System.out.prntln(nazwa[5]);
```

W ten sposób można wyświetlać wartość z tablicy i dodawać wartość do tablicy.

Tworzenie tabel dwuwymiarowych `typ[][] nazwa = new typ[wiersze][kolumny];`

`int[][] number2D = new int[4][3];`

W Javie tablice „dwuwymiarowe” są w rzeczywistości tablicami tablic. Każdy wiersz jest osobną tablicą w tablicy głównej. To oznacza, że wiersze mogą mieć różne długości.

Dostęp do poszczególnych elementów tablic: `nazwa[i][j]` gdzie i jest wierszami, j jest kolumnami.

```java
System.out.println(number2D[1][2]);
```

### Zadania

1. Przekształć podany łańcuch "Java to `wspaniały` język" na "Java to `najlepszy` język", korzystając z metody pod-łańcuchów.
2. poproś użytkownika o podanie całego zdanie (np. „`Ala ma kota, kot ma Ale`”), a następnie:
   * podziel je na słowa, używając `String.split()`
   * zapisz słowa do tablicy `String[]`
   * policz ile razy wprowadzony został każdy wyraz i wyświetl tą informację
3. Korzystając z StringBuilder: Połącz wyrazy wprowadzone przez użytkownika w pętli w jeden łańcuch znakowy
4. Stwórz obiekt StringBuilder na podstawie tekstu tekstu podanego przez użytkownika, następnie wykonaj: (wykonaj kolejno)
   1. Odwróć cały tekst (`reverse()`).
   2. Wstaw na początku frazę `"START-"`.
   3. Usuń wszystkie znaki od 3. do 6. indeksu (włącznie z 3., ale przed 6.).
   4. Zamień znaki od 2. do 5. na frazę `"XYZ"`.
5. Przeprowadź _mikro-benchmark_ w kodzie aby sprawdzić różnice w czasie dopisywania 100 000 razy "X" do startowego pustego tekstu za pomocą wzoru `text = text + "X";`
   1. wykorzystaj zwykły `+`
   2. wykorzystaj StringBuilder i append
   3. wyświetl czas trwania zapisu, możesz skorzystać z `Long czas = System.nanoTime()`
6. Napisz program który wypisze wszystkie samogłoski i ich pozycję w dowolnym łańcuchu znakowym wprowadzonym przez użytkownika
7. Napisz program, który w 10-elementowej tablicy jednowymiarowej umieści liczby od 9 do 0 i wypisze je na ekranie.
8. Napisz program, który utworzy 10-elementową tablicę liczb całkowitych i wypełni ją wartościami losowymi z przedziału {-20, …, 20} oraz:
   * wyznaczy najmniejszy i największy element w tablicy
   * wyznaczy średnią arytmetyczną elementów w tablicy
   * wyznaczy ile elementów jest mniejszych, a ile większych od średniej
   * wyznaczy ile razy każda liczb powtarza się w tablicy
