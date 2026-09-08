# Biblioteka Pandas

Biblioteka Pandas to podstawa analizy danych w języku Python. Biblioteka, które pozwala na łatwe wczytanie danych, czyszczenie i raportowanie.&#x20;

Najważniejszą strukturą w Pandas jest Data Frame (ramka danych). Jest to dwu-wymiarowa tablica, która ma etykiety osi (indeksy wierszy oraz nazwy kolumn). Zaletami ramki danych jest elestyczność co do typów danych, które są przechowywane w strukturze. Każda kolumna może przechowywać inny typ np. tekst, liczby zmiennoprzecinkowe czy date.&#x20;

Na początek należy importować biblioteki:

```python
import numpy as np
import pandas as pd
```

#### Tworzenie Ramek Danych

Aby rozpocząć pracę z ramkami danych należy wywołać konstruktor klasy DataFrame o podobnej nazwie `DataFrame()`, który może przyjąć różną kombinację&#x20;



**Tworzenie ramek z list**

W niekótych przypadkach wymagane jest stworzenie ramki danych na podstawie listy lub macierzy z danymi.

```python
matrix = np.array([
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
])

# Przekazujemy macierz i definiujemy nazwy kolumn oraz indeksy
df_matrix = pd.DataFrame(
    data=matrix,
    columns=['Kolumna_A', 'Kolumna_B', 'Kolumna_C']
)

print(df_matrix)
```

W przypadku macierzy nie są przechowywane nazwy kolumn czy wierszy. W konstruktorze jest możliwość zdefiniowania nazw kolumn.&#x20;

```
```



**Tworzenie ramek ze słowników**

Korzystająć ze słowników podczas tworzenia ramek danych&#x20;

```python
data = {
    'Uzytkownik': ['Anna', 'Bartek', 'Celina'],
    'Wiek': [28, 34, 22],
    'Wydano_PLN': [120.50, 450.00, 89.90]
}

df = pd.DataFrame(data)
print(df[df['Wydano_PLN'] > 100])
```

**Tworzenie ramek z innych źródeł**&#x20;

Częstym przypadkiem jest wczytywanie danych z plików, najpopularniejszym formatem plików jest CSV (ang. _comma-separated values_). Pliki tego typu możemy wczytać przy pomocy metody read\_csv(). Pierwszym parametrem jest lolalizacja pliku, kolejnymi parametrami może przyjąć separator, pominięcie pierwszego wiersza, itd.&#x20;

```python
pd.read_csv("test.csv")
```

Biblioteka pandas przygotowałą więcej metod, któe mogą wczytać pliki z takich formatów jak JSON, HTML, XML, XSLS.&#x20;



#### Odczytywanie informacji o ramkach danych

