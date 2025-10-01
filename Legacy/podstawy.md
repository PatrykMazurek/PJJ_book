---
description: Podstawy języka Java
---

# Podstawy

## Teoria&#x20;

Rozdział 2 - Podstawowe elementy języka Java

Rozdział 3 - Podstawowe elementy języka Java

## **Narzędzia wiersza poleceń**

Jeżeli wymagane jest szybkie modyfikowanie kodu bez środowiska programistycznego można wykorzystać interaktywny interpreter wpisując w wiersz poleceń lub PowerShell polecenie `jshell`.&#x20;

Wykonując polecenie `javac` wykonywane jest kompilacja plików plików `*.java` do plików `*.class`.  Przykład wykonania kompilacji dal pliku `HellowWord.java`&#x20;

`javac HellowWord.java`

Po skompilowaniu plików java, aby je uruchomić należy wykonać polecenie `java`, dzięki temu uruchomimy napisany wcześniej program. Przykład wykonania.

`java HelloWord`&#x20;

### **Środowiska programistyczne**

1. [intellJ](https://www.jetbrains.com/idea/)
2. [VS Code](https://code.visualstudio.com/)

Nie zalecam stosować rozszerzeń za pomocą, których można generować kod. Zajęcia przeznaczone są do poznania się z podstawowymi zadami i mechanizmów działających w środowisku. W późniejszym etapie jak najbardziej polecam do pracy z SI ponieważ to codzienność. &#x20;

### **Sterowanie przebiegiem programu**

W języku Java wyróżniamy kilka struktór, które pozwalają nam na sterowanie przebiegiem programu, są to:

* wyrażenie warunkowe `if` \ `else`
* wyrażenie warunkowe `if` \ `else if`
* `switch - case`
* pętla `for` \ `foreach`
* pęlta `while`&#x20;
* pętla `do-while`

Po krótce przedstawię budowę i zasady działąnia każdej z pętli.

**Wyrażenie warunkowe if \ else**

```java
int x = 10;
if (x > 0) { 
    System.out.println("x jest dodatnie");
} else {
    System.out.println("x jest ujemne lub równe 0");
}
```

Warunek if sprawdza czy wartość zmiennej x > 0 i zwraca wartość true lub false. Jeżeli warunek zwróci true to wyświetlony będzie pierwszy komunikat, w innym przypadku wyświetlony będzie komunikat drugi.

**Wyrażenie warunkowe if \ else if**

```java
int grade = 75;
if (grade >= 90) {
    System.out.println("Ocena: 5");
} else if (grade >= 70) {
    System.out.println("Ocena: 4");
} else if (grade >= 50) {
    System.out.println("Ocena: 3");
} else {
    System.out.println("Ocena: 2");
}
```

W przedstawionym kodzie sprawdzane je wartość zmiennej `grade`, która jest sprawdzana do momentu aż któryś z warunków nie zwróci wartości true. Jeżeli jest zwracana wartość False, to przechodzimy do następnego warunku. Jeżeli zostanie zwrócona wartość true wtedy jest wykonywany fragment kodu a pozostałe warunki nie są już sprawdzane.&#x20;

**switch - case**

```java
int day = 3;
switch (day) {
    case 1: System.out.println("Poniedziałek"); break;
    case 2: System.out.println("Wtorek"); break;
    case 3: System.out.println("Środa"); break;
    case 4: System.out.println("Czwartek"); break;
    default: System.out.println("Weekend");
}
```

Wyrażenie `switch` pozwala na wykorzystanie różnych instrukcji kodu w zależności od wartości zmiennej. Jeżeli nie zostanie dopasowana wartość zmienne zostanie wykonana instrukcja domyślna (`default`).

**Pętla for**&#x20;

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("i = " + i);
}
```

Pętla for pozwala nam na wykonanie instrukcji kodu określoną liczbę razy. W przedstawionym kodzie powyżej wypisujemy poszczególne numery kroków do momentu aż będzie spełniony warunek `i <= 5`. &#x20;

**Pętla foreach**

```java
int[] numbers = {10, 20, 30, 40};    
for (int n : numbers) {
    System.out.println("Element tablicy: " + n);
}
```

Pętla **foreach** jest prostsza i bezpieczniejsza, bo nie trzeba pamiętać o indeksach.\
Wadą jest to, że nie mamy bezpośredniego dostępu do numeru indeksu – jeśli indeks jest potrzebny, lepiej użyć klasycznej pętli `for`.

**Pętla while**

```java
int n = 3;
while (n > 0) {
    System.out.println("n = " + n);
    n--; // zmniejszamy wartość
}
```

Pętla `while` działa do momentu kiedy warunek jest spełniony. Zaletą tego rozwiązania jest fakt że warunek zależy od instrukcji wywołanych w ciele pętli `while`. nie ma ustalonej liczby kroków jak w pętli `for`.

**Pętla do-while**

```java
int x = 0;
do {
    System.out.println("x = " + x);
    x++;
} while (x < 3);
```

W przedstawionym powyżej fragmencie kodu, na początku wykonywana jest kod z ciała pętli `while` a na końcu sprawdzany jest warunek, Jeżeli zostanie spełniony kod jest powtarzany, jeżeli nie zakończona jest pętla `while`.

### **Zadania**

1. Napisz program w którym wyświetlisz jakąś informację o sobie na ekranie.
2. Napisz program w którym podstawowe informacje o sobie (np. wiek, wzrost, waga) będą znajdować się w zmiennych i następnie wyświetl je na ekranie.
3. Napisz program wyświetlający na ekranie tabliczkę mnożenia dla liczb od 1 do 10
4. Napisz program zamieniający cyfry 1-7 na pełne nazwy dni tygodnia za pomocą instrukcji _switch_
5. Napisz program który w oparciu o instrukcję _do ... while_ zsumuje liczby całkowite od 1 do 100
6. Napisz program, w którym używając pętli `for` odliczysz do liczby `n`, liczba `n` podana przez użytkownika. Wykonaj następne kroki:
   * Wypisuje wszystkie liczby od `1` do `n` w osobnych liniach.
   * Przy każdej liczbie dopisuje informację:
     * `"PARZYSTA"` jeśli liczba jest parzysta,
     * `"NIEPARZYSTA"` jeśli liczba jest nieparzysta,
     * dodatkowo, jeśli liczba jest podzielna przez 3 → dopisz `" FIZZ"`,
     * jeśli liczba jest podzielna przez 5 → dopisz `" BUZZ"`.
