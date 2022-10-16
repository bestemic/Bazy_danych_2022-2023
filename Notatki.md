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
* $\alpha$ - liczba operacji sekwencyjnych<br>
$P$ - liczba procesorów
$$S = \frac{1}{\alpha + \frac{1 - \alpha}{P}}$$

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

### Cykl życia oprogramowania

* Analiza
* Modelowanie
* Implementacja
* Wdrożenie
* Utrzymanie

Analiza to etap, w którym przygotowujemy i analizujemy zapotrzebowania biznesowe, aby następnie w etapie modelowania
przygotować model bazy danych.

### Model rzeczywistości

Baza danych jest określeniem pewnego modelu rzeczywistości i ma odpowiadać potrzebom klienta, a nie wyobrażeniom
projektanta. Część elementów musimy odrzucić, aby usunąć niepotrzebne informacje o świecie zewnętrznym. Z tego powodu
bazy danych są tylko pewnym **fragmentem rzeczywistości**.

### Diagram związków encji E/R

**Zbiór encji** to abstrakcyjna klasa reprezentująca fragment rzeczywistości. Posiada swoje atrybuty (wszystkie encje z
danego zbioru te same). W atrybutach oczekujemy, że znajdzie się atrybut jednoznacznie rozróżniający encje w zbiorze.

**Związki** zbiory par uporządkowanych, podzbiór iloczynu kartezjańskiego zbiorów. Łączą elementy jednego zbioru encji z
elementami innego. Związki encji mogą być wieloargumentowe i posiadać swoje atrybuty. W praktyce eliminujemy te
przypadki wprowadzając "sztuczne" związki dwuargumentowe.

### Rodzaje związków

* Wiele do wielu - nie wszystkie elementy zbioru muszą wchodzić we wskazany związek
* Wiele do jednego
* Jeden do wielu
* Jeden do jednego

### Integralność referencyjna

Typ związku wiele do jednego występujący tylko w kontekście bazodanowym, w którym wskazany element musi istnieć. Często
nazywany więzem integralności referencyjnej.

### Relacyjny model bazy danych

> Założenie, że cała baza jest przechowywana na jednym serwerze.

Nazwa modelu pochodzi od tabeli (ang. relation), a nie od związków między tabelami.

### Tabela

* Każda **kolumna** zawiera informacje o jednym atrybucie.
* Kolumny są uporządkowane.
* Każdy wiersz (**krotka**) odpowiada jednemu rekordowi danych.
* Tabela jest **zbiorem krotek**
    * Krotki nie mogą się powtarzać.
    * Krotki mogą być w dowolnej kolejności.

### Dane i metadane

**Schemat bazy danych** to zbiór wszystkich projektów tabel, relacji, atrybutów.

**Metadane** to schemat wraz z informacjami o użytkownikach i ich uprawnieniami.

**Instancja tabeli** zbiór krotek istniejących w danej chwili.

### Dwanaście zasad Codda

1. Informacje są reprezentowane logicznie w tabelach.
2. Dane są logicznie dostępne poprzez nazwę tabeli, klucz i nazwę kolumny.
3. Wartość `null` traktowana jest jako brak informacji.
4. Metadane umieszczone w bazie danych jak zwykłe dane.
5. Język obsługi ma mieć możliwość definiowania danych, widoków, więzów integralności, obsługi transakcji, manipulacji.
6. Widoki reagują na zmiany tabel bazowych, tabele bazowe reagują na zmiany w widokach.
7. Istnieją operacje pozwalające na wyszukiwanie, wstawianie, uaktualnianie i usuwanie danych.
8. Operacje użytkownika logicznie oddzielone od fizycznych danych i metod dostępu.
9. Operacje użytkownika pozwalają na zmianę schematu bazy danych bez tworzenia jej od nowa.
10. Więzy integralności przechowywane w metadanych.
11. Język manipulacji danych powinien działać niezależnie od rozmieszczenia danych fizycznych i nie powinien wymagać
    zmiany, gdy dane są centralizowane lub rozpraszane.
12. Operacje na pojedynczych rekordach podlegają tym samym zasadom co operacje na zbiorach danych.

### Algebra relacyjności

* Suma mnogościowa $R \cup S$ - zbiór krótek które należą do $R$ lub $S$
* Iloczyn mnogościowa $R \cap S$ - zbiór krótek które należą jednocześnie do $R$ i $S$
* Różnica mnogościowa $R - S$ - zbiór krótek które należą do $R$ i nie należą do $S$
* Iloczyn kartezjański $R \times S$ - zbiór wszystkich par krótek w których pierwszy element pary należy do $R$ drugi do $S$. 
* Selekcja $\sigma_C(R)$ - wybranie z tabeli %R% krotki spełniające warunek wyboru $C$
* Rzutowanie $\pi A_1,A_2,...(R)$ - wybranie z tabeli $R$ tylko kolumn obecnych na liście rzutowania $A_1,A_2,...$
* Przemianowanie $\rho_{S(B_1, B_2,...)}(R)$ - zmiana nazwy atrybutów w tabeli R na $B_1,B_2,...$
* Złączenie $R \Join_{C(R,S)}S$ - podzbiór iloczynu kartezjańskiego $R \times S$ który obejmuje tylko krotki spełniające warunek złączenia $C(R,S)$
    * Złączenie równościowe - złączone tabele mają takie same atrybuty (powtarzające się w obu tabelach), a złączenie obejmuje tylko równość powtarzających się atrybutów
    * Złączenie naturalne - złączenie równościowe po wszystkich powtarzających się kolumnach 

## Wykład nr 3

---

cdn.