# Obiekty Steam

### Stream (Strumienie)

Strumienie to sekwencje elementów, które mogą być przetwarzane sekwencyjnie, ale także równolegle (parallel), przez różnego rodzaju operacje agregujące. W Javie wiele elementów takich jak kolekcje, czy tablice, mogą być przetwarzane jako strumienie (lub mówiąc bardziej precyzyjnie mogą być konwertowane na strumienie).

Steam-y możemy podzielić na trzy etapy:

1. **dane źródłowe** np ArraList, String\[] ,
2. **operacje pośrednie (Intermediate)** np. operacje filtrowania (filter), operacje zmiany formatu, kształtu, wielkości (map), sortowania (sorted)
3. **Operacje kończące (Terminal)** zwrócenia danych w odpowiednim formacie np. list, zbiorów.

Obiekty Steam nie przechowują danych tylko je przetwarzają bez modyfikacji źródła danych.

Załóżmy że mamy listę imion z której chcemy wyciągną wszystkie imiona zawierające literę "a". &#x20;

```java
List<String> nameList = Arrays.asList("Ala", "Tomek", "Renata", "Marek", "Ewa", "Paweł");
List<String> resultList = new ArrayList<>();

for (String s : nameList){
    if (s.contains("a")){
        resultList.add(s.toUpperCase());
    }
}
```

Powyższy przykład wykonuje założone zadanie ale im większa struktura tym więcej warunkowi i pętli, co może powodować powstanie błędów. Obiekty steam mogą uprościć powyższy kod

```java
resultList = nameList.stream()                        //rozpoczęcei Steam-a
                .filter(name -> name.contains("a"))   //filtrowanie
                .map(String::toUpperCase)             //zmiana kształtu
                .collect(Collectors.toList());        //zwrucenie wyników do listy
```

&#x20;Powyższy przykład wykonuje to samo zadanie tylko w sposób dużo prostszy.&#x20;

**Operacje dostępne dla obiektów Stream**

operacje pośrednie, które możemy łączyć ze sobą

* map – mapuje jeden obiekt na inny
* flatMap – zwraca _„spłaszczony”_ strumień elementów (np. strumień, który powstał z kolekcji)
* distinct – zwraca strumień unikalnych elementów
* sorted – zwraca strumień naturalnie posortowanych elementów
* peek – zwraca element strumienia (można jej użyć jako pomoc przy debugowaniu)
* limit – ogranicza elementy strumienia
* skip – pomija określoną ilość elementów strumienia

Operacje terminalne&#x20;

* collect – grupuje elementy strumienia do odpowiedniego obiektu
* forEach – wykonuje zadaną akcję dla każdego elementu strumienia
* reduce – redukuje strumień do jakiejś wartości (np. obiektu)
* min – wyciąga minimalną wartość ze strumienia
* max – wyciąga maksymalną wartość ze strumienia
* count – zlicza elementy strumienia
* anyMatch – sprawdza, czy którykolwiek z elementów strumienia odpowiada zadanemu predykatowi
* allMatch – sprawdza, czy wszystkie elementy strumienia odpowiadają zadanemu predykatowi
* noneMatch -sprawdza, czy wszystkie elementy nie odpowiadają zadanemu predykatowi
* findFirst – zwraca pierwszy element z przetworzonego strumienia
* findAny – zwraca jakiś element strumienia (w przypadku strumieni przetwarzanych równolegle w wielu wątkach, poszukiwany element może być dowolnym elementem strumienia)

### Parallel Stream

W sytuacji kiedy mamy duży zbiór danych i wymagamy zwiększyć wydajność zamiast pojedynczego przetwarzania (Stream) możemy wykorzystać przetwarzanie równoległe (ParallelStream). Lista dzielona jest na mniejsze części i przekazywane jest do osobnego wątku i przetwarzanie równolegle, a na koniec dane są łączone. Przykład działania

```
// Wersja sekwencyjna (jeden wątek)
list.stream()
    .filter(...)
    .collect(...);

// Wersja równoległa (wiele wątków)
list.parallelStream()  // <--- Tylko ta zmiana!
    .filter(...)
    .collect(...);
```

Nie zawsze jest polecane stosowanie ParallelStream, ponieważ przy zbiorach niewielkich liczących np sto, tysiąc elementów etap podziału, wykonania operacji i łączenia danych może zająć więcej czasu niż wykonanie operacji na jednym wątku przez Stream.

#### Kiedy używać Parallel Stream? (Checklista)

Używaj `parallelStream()` tylko, gdy spełnione są te warunki:

1. Duża ilość danych: Masz tysiące lub miliony elementów (nie dziesiątki).
2. Ciężkie obliczenia: Operacja na każdym elemencie zajmuje dużo czasu (np. skomplikowana matematyka, przetwarzanie obrazu).
3. Brak zależności (Stateless): Przetwarzanie jednego elementu nie zależy od innego.
4. Brak współdzielonych zasobów: To najważniejsze! Jeśli w środku strumienia modyfikujesz jakąś wspólną zmienną spoza strumienia, doprowadzisz do katastrofy (tzw. Race Condition).

### Zadania



### Literatura dodatkowa&#x20;

{% embed url="https://www.samouczekprogramisty.pl/strumienie-w-jezyku-java/" %}

{% embed url="https://nullpointerexception.pl/kurs-java-dla-poczatkujacych-8-streamy-i-lambdy/" %}

{% embed url="https://justjoin.it/blog/zastosowanie-stream-api-z-java-8-przyklady" %}
