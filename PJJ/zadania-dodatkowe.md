# Zadania dodatkowe

1.  Napisz aplikację, która będzie zarządzać kontaktami osób i firm.  Aplikacji powinna zawierać następującą funkcjonalność  dodawać i edytować kontakty oraz filtrować zapisane dane. Podstawowe założenia co do struktury klas:

    **Typy kontaktu:**

    klasa abstrakcyjna `Contact` zawierająca pola id, displayName, methods (liat\<ContactMethod>) createdAt, updatedAt (LocalDateTime).

    Każda z poniższych klas dziedziczy po klasie `Contact`

    Klasa `Person`  zawierająca pola: FirstName, LastName, birthDate (opcjonalne), tag.

    klasa `Company` zawierająca pola: name, industry, tag.

    **Metody kontaktu**

    klasa abstrakcyjna `ContactMethod` zawierający pola: label (np. prywatny, firmowy), isPrimary.

    Każda z poniższych klas dziedziczy po klasie `ContactMethod`

    klasa `Address` zawierająca pola: country, city, street, postalCode (walidacja wprowadzonego kodu pocztowego).

    klasa `Phone` zabierająca pole phoneNubem (walidacja  danych, usuwanie niepotrzebnych znaków).

    Klasa `Email` zawierająca pole: emailAddress (walidacja danych i usuwanie niepotrzebnych znaków).

    **Funkcjonalność programu**

    Dodawanie kontaktu (osoba/firma) i metody kontaktu (dowolna liczba)

    Edycja / usunięcie kontaktu lub metody kontaktu.

    Proste wyświetlenie kontaktu w postaci

    &#x20;\- osoba imię nazwisko telefon, email.

    &#x20;\- firma nazwa firmy, telefon, email.

    Program powinien działać w konsoli. Wraz z poznaną wiedzą zadanie będzie otrzymywać kolejne uaktualnienia i dodatkowe rozwiązania.
