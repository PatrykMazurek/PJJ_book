# Kolekcje

### Kolekcje List

List - uporządkowana kolekcja, która pozwala zachować kontrole nad elementami, Dostęp do elementu na podstawie indeksu. interfejs List dziedziczy po interfejsie Collection. Najpopularniejsze obiekty List:

* ArrayList
* LinkedList
* Vector

Przykłady zastosowań:

```java
List<String> animal = new ArrayList<>();
animal.add("słoń");
animal.add("lew");
animal.add("pingwin");
animal.addFirst("tygrys");
if (animal.remove("krokodyl")){
    System.out.println("usunięto z listy");
}else{
    System.out.println("nie ma obiektu na liście");
}
String removeObj = animal.remove(1);
String obj1 = animal.get(0);
String obj2 = animal.getLast();
int idx = animal.indexOf("lew");
if (idx != -1) {
    System.out.println("obiekt jest na liście");
}else {
    System.out.println("obiektu nie ma na liście");
}
```

Więcej dostępnych metod można znaleźć w dokumentacji&#x20;

{% embed url="https://docs.oracle.com/javase/8/docs/api/java/util/List.html" %}

### Kolekcje Map

Map - Kolekcja, która składa się z klucza i wartości, w kolekcji mam klucz powinien być unikalny a wartość może się powtarzać. Interfejs Map nie dziedziczy po interfejsie Collection. Najpopularniejsze obiekty Map:

* HashMap
* LinkedHashMap
* TreeMap

Przykład zastosowania&#x20;

```java
Map<String, String> student = new HashMap<>();
student.put("s0001", "Jan Kowalski");
student.put("s0002", "Ewa Nowak");
student.put("s0003", "Jan Nowak");
String temp = student.remove("s0001");
if (student.containsKey("s0005")){
    System.out.println("student jst na liście");
}else {
    System.out.println("studenta nie ma na liście");
}
```

Więcej dostępnych metod można znaleźć w dokumntacji&#x20;

{% embed url="https://docs.oracle.com/javase/8/docs/api/java/util/Map.html" %}

### Kolekcje Set

Set - kolekcja nie uporządkowana, w której nie masz kontroli na kolejnością elementów, nie można odwołać się do elementów po indeksie. Set nie pozwala na przechowywanie duplikatów. Interfejs Set dziedziczy po interfejsie Collection. Najpopularniejsze obiekty Set:

* HashSet
* LinkedHashSet
* TreeSet

Przykład zastosowania&#x20;

```java
Set<String> product = new HashSet<>();
product.add("mleko");
product.add("jabłko");
product.add("woda");
if(product.contains("ser")){
    System.out.println("produkt jest na liście");
}else{
    System.out.println("produktu nie ma na liście");
}
if (product.remove("woda")){
    System.out.println("produkt usunięty z listy");
}else{
    System.out.println("produktu nie udało się usunąć");
}
```

Więcej dostępnych metod można znaleźć w dokumentacji&#x20;

{% embed url="https://docs.oracle.com/javase/8/docs/api/java/util/Set.html" %}

### Zadania

1.  Stwórz funkcję, która jako parametr przyjmie listę liczb (dowolnej długości). Funkcja ma kilka zadań:

    &#x20;\- zamienić liczby ujemne na dodatnie (jeżeli takie występują)

    &#x20;\- sprawdzić czy występują duplikaty, jeżeli tak to usunąć je&#x20;

    &#x20;\- posortować rosnąco

    Funkcja powinna zwrócić listę&#x20;
2. Korzystając z kolekcji Map stwórz licznik słów i zwróć N najczęściej występujących słów. Dla wybranego tekstu policz wszystkie słowa pomijając prostych "stopwords" `["i","a","oraz","ale","lub","to","na","w","do","o"].` Zwróć najczęściej występujące słowa .

### Materiały dodatkowe

{% embed url="https://www.geeksforgeeks.org/java/list-interface-java-examples/" %}

{% embed url="https://www.digitalocean.com/community/tutorials/java-list" %}

{% embed url="https://www.geeksforgeeks.org/java/set-in-java/" %}

{% embed url="https://www.digitalocean.com/community/tutorials/java-set" %}

{% embed url="https://www.geeksforgeeks.org/java/map-interface-in-java/" %}

{% embed url="https://javastart.pl/baza-wiedzy/klasy/interfejs-map" %}
