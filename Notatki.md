# Wykład bazy danych

## Wykład nr 1

---

### Bazy danych

* tematycznie wyodrębniony, ustrukturalizowany zbiór danych
* duża kolekcja danych odpowiednio ustrukturalizowany w calu szybkiego dostępu do informacji

> Baza zawiera struktury które przechowują dane i opis struktur. Jest to **katalog systemowy / metadane**. Pozwala to na niezależność danych od aplikacji.

### Bazy danych są wszechobecne

* Użytkownik widzie frontend
* Programiści aplikacji bazodwanowych używają baz
* Projektanci i administratorzy baz danych tworza bazy danych dla aplikacji
* Programiści systemów bazodanowych czyli systemów do zarządania bazami danych (izolują dane od technologi)

> DBMS - DataBase Management Systems

### Architektura klient serwer

* Logikę biznesowaa umieszczamy po stronie serwera
* Większość operacji wykonuje serwer
* Prosta w przygotowaniu
* Serwer przechowuje dane o architekturze bazy (schematach, więzach) a nie aplikacja co zwiększa bezpieczeństwo
* Mało elastyczna, słabo rozszerzalna
* Największym kosztem jest przesył danych

### Schemat i instancja

* Przy projektowaniu zastanawiamy się co przechowywujemy
* Jakie są związki między elementami bazy danych
* Baza to abstrakcyjny model o określonym schemacie

**Schemat** zawiera informacje o tabelach, kolumnach, typach danych, indeksach i wzajemnych relacjach.

**Instancja** jest konkretnym wystąpieniem bazy danych wraz z konkretną chwilową jej zawartością. Każda instancja jest
fizycznie zlokaloizowana na sprzęcie.

### Skalowanie i elastyczność

**Skalowalność** to zdolność systemu do wykonywania narastającej liczby zadań lub potencjalna możłiwość rozbudowania
sytemu tak aby sobie poradził z liczbą zadań.

* Pionowe (vertical) - dokładanie zasobów do istniejącego serwera
* Poziome (horizontal) - dokładnie serwerów które przechowują fragmenty bazy i obsługują część ruchu

**Elastyczność** to stopień w jakim system potrafi dostosować się do zmiennego obciążenia poprzez uruchamianie i
zwalnianie zasobów.

### Wady i zalety skalowań

* Pionowe
    * Zalety
        * Brak spowolnień w celu zapewnienia spójności danych, wszystko znajduje się w jednym miejscu
        * Mniejsze koszta mocy, chłodzenia, przestrzeni
    * Wady
        * Niska elastyczność, przy przenoszeniu na inną maszynę trzeba przenieść całą bazę
        * Wysokie koszty jednostkowe
        * Awaria unieruchamia cały system
        * Prawo malejących przychodów (Amdahla)
* Poziomwe
    * Zalety
        * Duża elastyczność
        * Niższy koszt jednostkowy
        * Awaria nie uruchamia systemu
    * Wady
        * Opóźnienia w celu zapewnienia spójność danych, dane trzeba aktualizować na wielu serwerach
        * Większe koszty eksploatacyjne
        * Wymaga wielu połączeń sieciowych
        * Niejednorodne oprogramowanie
        * Nierównomierne obciążenie serwerów

### Prawo Amdahla

* Nazywamy prawem malejących przychodów
* Używane do znajdowania maksymalnego zwiększenia wydajności całkowitej jeśli ulepszamy część systemu
* Pozwala znaleść wydajność całego systemu gdy zmieniamy pewną część
* Mając wiele procecorów dokładanie kolejnego zmniesza zysk

[comment]: <> (TODO dodać wzór na prawo )

### Bazy relacyjne

* Opierają się na silnych podstawach matematycznych
* Wymagają przemyślanego zaprojektowania
* Chronią przed błędami i zapewniają bezpieczeństwo danych
* Ciągła spójność między serwerami, ale generują opóźnienia
* Długi okres życia ale problem gdy dane nie pasują do schematu

> **Spójność danych** to wierne odzwierciedlenie danych rzeczywistych, spełniają ograniczenia nałożone przez użytkownika (
reguły). Nie zawiera anomali wynikających ze współbierznego dostęu do danych.

* Stosujemy skalowanie poziome, replikujemy dane dla zapewnienia bezpieczeństwa, gdy dane do odczytu nie powoduje to
  spowolnień, w przeciwnym razie ogromne opóźnienia
* Duże tabele dzielimy ze względu na klucz

### Bazy nierelacyjne (NoSQL)

* NoSQL - Not only SQL
* Gorzej zdefiniowane podstawy
* Szybko projektujemy, odpowiedzialność spoczywa na programiście
* Wykorzystywane z nowymi technologiami
* Nie muszą zapewniać spójności danych między serwerami
* Lepsza dostępność ale niespójność danych
* Krótki czas życia, ale elastyczne przy różnych danych

## Wykład nr 2

--- 
cdn. 

