# Obsługa plików

Manipulacja plikami jest jednym z podstawowych zagadnienia programowania w Javie. Niezależnie od tego czy chcesz zapisywać dane aplikacji, generować logi, czy obsługiwać zewnętrzne pliki konfiguracyjne. Obsługa plików nie obejdzie się bez wskazania lokalizacji, w której dany plik się znajduje.

W języku Java znajdują się dwa pakiety, za pomocą których można działać na plikach i katalogach:

* `java.io.*` - starsza wersja
* `java.nio.*` - nowsza wersja&#x20;

### Metoda Paths.get()

Metoda `Paths.get()` klasy `java.nio.file.Paths` w języku Java jest podstawowym narzędziem do obsługi ścieżek plików. Pozwala ona tworzyć obiekty `Path`, które mogą być używane do reprezentowania ścieżek plików i katalogów w sposób niezależny od platformy.

```java
Path path = Paths.get("C:", "Users", "Student", "Documents", "file.txt");
```

Metoda może przyjmować jeden lub więcej argumentów typu string. Pierwszy argument jest obowiązkowy i reprezentuje początkową część ścieżki. Wszelkie dodatkowe argumenty są traktowane jako pod ścieżki, które mają zostać dołączone do ścieżki początkowej.

**Ścieżka absolutna vs. relatywna**

Ścieżka bezwzględna to pełna ścieżka od katalogu głównego do docelowego pliku lub katalogu. Rozpoczyna się od katalogu głównego systemu plików i przechodzi przez hierarchię katalogów, aby zlokalizować cel. Ścieżki bezwzględne są jednoznaczne i mogą być używane do jednoznacznej identyfikacji pliku lub katalogu, niezależnie od bieżącego katalogu roboczego aplikacji.

Ścieżka względna określa lokalizację pliku lub katalogu względem innego katalogu, zazwyczaj bieżącego katalogu roboczego. W przeciwieństwie do ścieżek bezwzględnych, ścieżki względne nie zaczynają się od katalogu głównego, ale od katalogu, w którym aktualnie działa aplikacja.

### Klasa File

Klasa File pozwala nam na manipulowanie plikami tworzenie, usuwanie, przenoszenie czy sprawdzanie czy dany plik istniej lub jego prawa dostępu.&#x20;

```java
File file = new File("example.txt");

try {
    if (file.createNewFile()) {
        System.out.println("Plik utworzony: " + file.getName());
    } else {
        System.out.println("Plik już istnieje.");
    }
} catch (IOException e) {
    System.out.println("Wystąpił błąd.");
    e.printStackTrace();
}
```

W powyższym przykładzie próbujemy stworzyć plik w domyślnej lokalizacji,. Jeżeli plik już będzie istniał to nie zostanie utworzony, a jeżeli pliku nie będzie to zostanie stworzony.&#x20;

W sytuacji kiedy poturbujemy sprawdzić informacje o pliku możemy wykorzystać następujące metody&#x20;

```java
File file = new File("example.txt");
if (file.exists()) {
    System.out.println("Nazwa pliku: " + file.getName());
    System.out.println("Ścieżka absolutna: " + file.getAbsolutePath());
    System.out.println("Czy plik jest zapisywalny: " + file.canWrite());
    System.out.println("Czy plik jest odczytywalny: " + file.canRead());
    System.out.println("Rozmiar pliku: " + file.length() + " bajtów");
}
```

W sytuacji kiedy potrzebujemy zmienić nazwę wybranego pliku lub przenieść plik do innego katalogu możemy skorzystać z poniższego rozwiązania

**Przykład zmiany nazwy pliku**

```java
public class RenameFileExample {
    public static void main(String[] args) {
        Path source = Paths.get("stara_nazwa.txt");
        Path target = Paths.get("nowa_nazwa.txt");

        try {
            Files.move(source, target);
            System.out.println("Plik został przemianowany.");
        } catch (IOException e) {
            System.err.println("Błąd podczas zmiany nazwy: " + e.getMessage());
        }
    }
}
```

**Przykład przenoszenia plików między katalogami**

```java
public class MoveFileExample {
    public static void main(String[] args) {
        Path source = Paths.get("C:/dane/pliki/test.txt");
        Path target = Paths.get("C:/dane/backup/test.txt");

        try {
            Files.move(source, target);
            System.out.println("Plik został przeniesiony.");
        } catch (IOException e) {
            System.err.println("Błąd podczas przenoszenia pliku: " + e.getMessage());
        }
    }
}
```

**Przykład usuwania pliku**&#x20;

```java
public class DeleteFileExample {
    public static void main(String[] args) {
        Path path = Paths.get("test.txt");

        try {
            Files.delete(path);
            System.out.println("Plik usunięty.");
        } catch (IOException e) {
            System.err.println("Błąd podczas usuwania pliku: " + e.getMessage());
        }
    }
}
```

W powyższym przykładzie jeżeli plik nie zostanie usunięty to zostanie wywołany wyjątek&#x20;

### Odczyt i zapis do pliku

**obsług plików tekstowy**

**FileWrite** - Zapisuje dane do pliku z wykorzystaniem domyślnego kodowania systemowego, pozwala na zdefiniowanie czy dane mają nadpisane czy dopisane do pliku.&#x20;

```java
FileWriter fw = new FileWriter("plik.txt");
fw.write("tekst");
fw.close();
```

**BufferedWriter** - Zapisuje dane do pliku większymi porcjami, większość trzyma w pamięci, dodaje metodę do dodawania nowej linii `newLine()`.&#x20;

```java
BufferedWriter bw = new BufferedWriter(new FileWriter("plik.txt"));
bw.write("Linia 1");
bw.newLine();
bw.write("Linia 2");
bw.close();
```

**PrintWriter** -  rozwiązanie, które ułatwia pisanie i formatowanie tekstu przez wykorzystanie odpowiednich metod `print`, `println`, `printf`.

```java
PrintWriter pw = new PrintWriter("plik.txt");
pw.println("Linia 1");
pw.printf("Liczba: %d%n", 42);
pw.close();
```

Łączenie powyższych metod w jedno użyteczne rozwiązanie do zapisu danych do pliku.

```java
PrintWriter pw = new PrintWriter(
        new BufferedWriter(
                new FileWriter("plik.txt")
        )
);
pw.println("Coś tam");
pw.close();
```

**FileReader** - odczytywanie danych z pliku z domyślnym kodowaniem, możemy czytać cały plik lub po określonej długości, nie mamy możliwości czytania linia po linii.

```java
public class FileReaderExample {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("plik.txt")) {
            int ch;
            while ((ch = fr.read()) != -1) {
                System.out.print((char) ch);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**BufferedReader** - najczęściej wykorzystywany z inną klasą odczytującą plik, pozwala na czytanie pliku po fragmentach np. linia po linii. metoda `readLine()`.&#x20;

```java
public class BufferedReaderExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("plik.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Obsługa plików binarnych**&#x20;

**OutputStream** - strumień surowcach bajtów (0,1). Klasa przekazuje do pliku lub w inne miejse ciąć0 i1 bez zwracania uwagi na kodowanie np. UTF-8.&#x20;

```java
try (OutputStream out = new FileOutputStream("plik.bin")) {
    out.write(65);                 // jeden bajt o wartości 65 (0x41, 'A' w ASCII)
    out.write(new byte[]{1, 2, 3});
} catch (IOException e) {
    e.printStackTrace();
}
```

**OutputStreamWriter** - Połączenie zwykłego tekstu (char / String) z zapisem do formatu binarnego z uwzględnieni odpowiedniego kodowania np. UTF-8.

```java
try (OutputStream out = new FileOutputStream("tekst.txt");
     OutputStreamWriter writer = new OutputStreamWriter(out, StandardCharsets.UTF_8)) {

    writer.write("Cześć UTF-8");
} catch (IOException e) {
    e.printStackTrace();
}
```

**InputStream** - odczytywanie zawartości pliku/sieci w postaci bajtów&#x20;

```java
try (InputStream in = new FileInputStream("obrazek.jpg")) {
    byte[] buffer = new byte[4096];
    int bytesRead;
    while ((bytesRead = in.read(buffer)) != -1) {
        // tutaj coś robisz z danymi
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

**InputStreamReader** - połączenie odczytywania bajtów z konwersją na tekst przy uwzględnieniu odpowiedniego kodowania np. UTF-8.&#x20;

```java
try (BufferedReader br = new BufferedReader(
        new InputStreamReader(
                new FileInputStream("tekst.txt"),
                StandardCharsets.UTF_8
        ))) {

    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### Zadania

1. Napisz program, który znajduje w podanym katalogu wszystkie pliki większe niż 2048 bajtów i zapisuje listę ich ścieżek do pliku tekstowego `big_files.txt`.
2. Napisz program, który stworzy coś w stylu dziennik użytkownika. Program ma pytać użytkownika o imię, zadawać pytanie w stylu "Jak minął dzień?" i zapisywać informacje pobrane od użytkownika  w formacie "`<data> | <użytkownik> |  <wiadomość>"` do pliku `dziennik.txt`, program ma sprawdzić czy plik istniej jeżeli tak to na końcu ma dopisać nową informację.&#x20;
3. Napisz program, który odczyta wybrany plik tekstowy i wyszuka określone słowa w tekście. W wyniku program powinien  wypisać całą linie, w której znalazł dane słowo.
4. Napisz program, który pobierze od użytkowania ścieżkę do pliku, sprawdzi czy plik istnieje jeżeli nie to przewie działanie programu z odpowiednim komunikatem. Jeżeli plik będzie istniał to ma sprawdzić jego wielkość oraz ile linie tekstu znajduje się w pliku.
5. Napisz program, który pobierze od użytkownika ścieżkę do pliku, sprawdzi czy plik istnieje jeżeli nie to go utworzy. Program powinien pobierać tekst od użytkownika i zapisywać do pliku w nowej linie do monomeru kiedy użytkownik nie poda pustej linii. Jeżeli poda pustą linie to ma zakończyć działanie.
6. Stwórz program, który pobierze od użytkownika ścieżkę do pliku, następnie pobiera tekst i szyfruje go szyfrem Cezara, następnie zapisuje zaszyfrowany tekst do pliku. wartość przesunięcia zapisz na końcu pliku w kodzie szesnastkowym (heksagonalnym).&#x20;
7. Stwórz program deszyfrujący dane zapisane w pliku z zadania 6.
