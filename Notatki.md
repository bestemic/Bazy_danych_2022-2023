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
* Selekcja $\sigma_C(R)$ - wybranie z tabeli $R$ krotki spełniające warunek wyboru $C$
* Rzutowanie $\pi A_1,A_2,...(R)$ - wybranie z tabeli $R$ tylko kolumn obecnych na liście rzutowania $A_1,A_2,...$
* Przemianowanie $\rho_{S(B_1, B_2,...)}(R)$ - zmiana nazwy atrybutów w tabeli R na $B_1,B_2,...$
* Złączenie $R \Join_{C(R,S)}S$ - podzbiór iloczynu kartezjańskiego $R \times S$ który obejmuje tylko krotki spełniające warunek złączenia $C(R,S)$
    * Złączenie równościowe - złączone tabele mają takie same atrybuty (powtarzające się w obu tabelach), a złączenie obejmuje tylko równość powtarzających się atrybutów
    * Złączenie naturalne - złączenie równościowe po wszystkich powtarzających się kolumnach 


## Wykład nr 3

---

### Zależności funkcyjne 

$ X = {A_1, A_2, ..., A_n} $<br>
$ Y = {B_1, B_2, ..., B_m} $<br>
$ Z = {C_1, C_2, ...} $

Mówimy że zbiór atrybutów Y **zależy funkcyjnie** od zbioru atrybutów X wtedy i tylko wtedy, gdy każda ustalona wartość X jest **jednoznacznie** powiązana z wartością Y. Zapisujemy je w postaci:

$$
A_1, A_2, ..., A_n \rightarrow B_1, B_2, ..., B_m\\
X \rightarrow Y
$$

Alternatywnie mówimy że jeśłi dwie krotki w tabeli są zgodne w atrybutach X to musza być zgodne w atrybutach Y.

* Zależności funkcyjne są więzami nałożonymi na dopuszczalne wartości danych 
* Zależności funkcyjne odkrywamy w procesie analizy fragemntu rzeczywistości który baza ma opisywać
* Zależności należą do schematu bazy
* Zależności są matematycznym modelem więzów jednoznaczoności w relacyjnym modelu
* O zależnościach nie możęmy jedynie wnioskować na podstawie instancji tabel

### Zależności trywialne 

Trywialna zależność funkcyjna to zależność $A_1, A_2, ..., A_n \rightarrow B$ w której atrybut B jest równy któremuś atrybutowi w $A_{1, 2, ..., n}$

* **Trywialna** jeśli zbiór złożony z atrybutów B jest podzbiorem zbioru atrybutów A
* **Nietrywialna** jeśli co najmniej jednen B nie jest A 
* **Całkowicie** nietrywaialna jeśli żaden B nie jest A
    
### Reguły wnioskowania (aksjomaty Armstronga)

* Zwrotność 

    Jeżeli $\{B_1, B_2, ..., B_m\} \subseteq \{A_1, A_2, ..., A_n\}$, to $A_1, A_2, ..., A_n \rightarrow B_1, B_2, ..., B_m$
* Rozszerzenie

    Jeżeli $A_1, A_2, ..., A_n \rightarrow B_1, B_2, ..., B_m$, to $A_1, A_2, ..., A_n, C_1, C_2, ..., C_k \rightarrow B_1, B_2, ..., B_m, C_1, C_2, ..., C_k$ dla dowolnych $C_1, C_2, ..., C_k$

* Przechodniość 

    Jeżeli $A_1, A_2, ..., A_n \rightarrow B_1, B_2, ..., B_m$ oraz $B_1, B_2, ..., B_m \rightarrow C_1, C_2, ..., C_k$, to $A_1, A_2, ..., A_n \rightarrow C_1, C_2, ..., C_k$

* Sumowanie

    Jeżeli X $\rightarrow$ Y oraz X $\rightarrow$ Z, wtedy X $\rightarrow$ Y, Z  

* Rozkład 

    Jeżeli X $\rightarrow$ Y oraz Z $\subseteq$ Y, to X $\rightarrow$ Z 

* Pseudoprzechodniość

    Jeżeli X $\rightarrow$ Y oraz Y, Z $\rightarrow$ W, to X, Z $\rightarrow$ W

### Domknięcia

$\{A_1, A_2, ..., A_n\}$ jest zbiorem atrybutów, S jest zbiorem zależności funkcyjnych. Domnięciem tego zbioru nad S nazywamy taki zbiór atrybutów B, taki że jeśli jego elementy spełniają wszystkie zależności funkcyjne z S, to spełniają także zależność $A_1, A_2, ..., A_n \rightarrow B$, a zatem zależność $A_1, A_2, ..., A_n \rightarrow B$ wynika z S.

* Algorytm obliczania domknięć:

    1. Niech X oznacza zbiór $\{A_1, A_2, ..., A_n\}$
    2. Znajdujemy wszystkie zależności funkcjyjne postaci $B_1, B_2, ..., B_m \rightarrow C$, gdzie $B_i$ należą do X i C nie należy. Dołączamy C do X.
    3. Powtarzamy krok 2 tyle ile da się dołączyć jakiś nowy atrybut. Po skończonej liczbie kroków nie da się już nic dodać do X.

* Algorytm ten jest prosty ale mało efektywny - w najgorszym przypadku w czasie kwadratowym.

### Bazy zależności funkcyjnych 

**Baza zbioru zależności funkcyjnych** - każdy zbiór zależnośc funkcyjnych pewniego zbioru atrybutów z którego można wyprowadzić wszystkie inne zależności funkcyjne

**Baza minimalna** - baza w której żaden podzbiór bazy nie jest bazą

### Klucze

Zbiór atrybutów $\{A_1, A_2, ..., A_n\}$ tworzy **klucz**, jeśli wszystkie pozostały atrybuty są funkcyjnie zależne od wskazanego zbioru. 

> Dwie różna krotki nie mogą mieć tych samych kluczy.

**Klucz minimalny** to klucz złożony z jak najmniejszej ilość atrybutów.

**Nadklucz** to jest to każdy nadzbiór klucza minimalnego.

> Obliczanie dokmnięć jest formalnym narzędziem służącym do identyfikacji klucza.

### Pierwsza postać normalna

1. Tabela posiada klucz
2. Wszystkie składowe krotek są atomowe

> Pierwsza postać normalna jest warunkiem by baza była w systemie relacyjnym. Warunek posiadania krotek jest równoważny temu, że tabela jest zbiorek krotek. 

### Atomowość danych 

Składowych krotek nie można podzielić.

> Warunek atomowości krotek uniemożliwia aby składowe były złożone struktury danych.

### Anomalie baz danych 

* Redundancja - ta sama infirmacja niepotrzebnie przechowywana w kilku krotkach 
* Anomalia modyfikacji - informacja może zostać zmodyfikowana tylko w pewnych krotkach
* Anomalia usuwania - usinięcie części danych powoduję utratę innej informacji
* Anomalia dołączania - wprowadzenie informacji jest możliwe tylko gdy wprowadzamy inną informację (chwilowo niedostęoną)

### Druga postać normalna

1. Tabela jest 1PN
2. Wszystkie atrybuty, które nie należą do klucza zależą funkcyjnie od pełnego klucza

### Złączenie bezstratne

Normalizację przeprowadzamy poprzez dzielenie tabeli na tabele potomne. 

> Wymogiem jest aby te tabale pozwalały na pełne odtworzenie informacji po dokonaniu złączenia naturalnego.

**Dekompozycja bezstratnego złączenia** to podział tabeli R na tabele $R_1, R_2, ..., R_n$ takie że ich naturalne złączenie jest równe tabeli R.

### Twierdzenie Heatha

Tabelę R o atrybutach X, Y, Z, spełniającą zależność funkcyjną X $\rightarrow$ Y możn bezstratnie zdekomponować na wyniku rzutowania $R_1 = \pi_{XY}(R)$ oraz $R_2 = \pi_{XZ}(R)$

### Trzecia postać normalna

1. Tabela jest 2PN
2. Dla wszystkich atrybutów tabeli zachodzi:

    Jeżeli $A_1, A_2, ..., A_n \rightarrow A_m$, to albo $\{A_1, A_2, ..., A_n\}$ jest nadkluczem albo $A_m$ jest elementem innego klucza.

### Zależności przechodnie i cykliczne

* Przechodznie 

    Jeśli w tabeli nie występują zależności cykliczne to 3PN zakazuje wystęowania zależności przechodnich.

* Cykliczne

    W tych zależnościach są zależności przechodnie ale atrybuty niekluczowe są elementami innych kluczy. 

### Postać normalne Boyce'a Codda (BNCF)

1. Jest 2PN
2. Dla każdej zależności nietrywaialnej, jeżeli $A_1, A_2, ..., A_n \rightarrow A_m$, to $\{A_1, A_2, ..., A_n\}$ jest nadkluczem.

> Każda tabela BCNF jest też w 3PN ale nie odwrotnie!

> Nie każdą tabelę da się znormalizować do BCNF, priorytetem jest zachowanie zależności funkcyjnych oraz bezstratności złączeń.

### Zależności wielowartościowe

Zbiory X, Y są związane zależnośćią wielowartościową, co zapisujemy $X \rightarrow\rightarrow Y$ jeżeli po utworzeniu zbioru wszystkich kombinacji $x_cyz$ realnie występujących w tabeli stwierdzamy, że $x_c$ jest stowarzyszone z tymi samymi wartościami y bez względu na wartość z. 

> Zależności wielowartościowe nie odnoszą się do schematu a do instancji tabeli.

### Czwarta postać normalna 

1. Jest 3PN
2. Dla każdej nietrywaialnej zależności wielowartościowej $A \rightarrow\rightarrow B$, A jest nadkluczem.

> Każda tabela BCNF, która nie zawiera nietrywaialnych zależności wielowartościowych jest 4PN.


## Wykład nr 4

---

### SQL (Structured Query Language)

Jest to interpretowany język programowania. Jego polecenia nazywamy zapytaniami. 

* Części SQL 
    * DDL (Data Definition Language) - zmiany schematu, tworzenie, usuwanie, modifikacja tabel i indeksów
    * DML (Data Manipolation Language) - wprowadzanie, modyfikowanie i usuwanie danych
    * DQL (Data Query Language) - właściwy język zapytań
    * DCL (Data Control Language) - nadawanie uprawnień do obiektów bazodanowych 
* SQL jest językiem deklaratywnym (mówimy co chcemy osiągnąć bez podania jak to osiągnąć)

### SELECT

Służy do uzyskiwania zawartości tabeli lub obliczeń matematycznych.

### Zmienne tymczasowe 

Zmienne tymczasowe definiujemy poprzez:

```sql
SET @nazwaZmiennej=wartość;
```

Do zmiennej możemy również przypisać wynik zapytania oraz istnieje dopóki nie zakończy się połączenie z serwerem.

### Tworzenie bazy danych 

1. Utworzenie bazy
    ```sql
    CREATE DATABASE nazwaBazy
    ```
2. Wejście do bazy
    ```sql
    USE nazwaBazy
    ```
3. Wyświetlenie listy baz danych na serwerze 
    ```sql
    SHOW DATABASES
    ```
4. Tworzenie tabeli 
    ```sql
    CREATE TABLE nazwaTabeli (definicja pól)
    ```
5. Dodawanie kolumny do tabeli
    ```sql
    ALTER TABLE nazwaTabeli
    ADD COLUMN (dofinicja kolumny)
    ```
6. Uzyskanie definicji tabeli
    ```sql
    DESCRIBE nazwaTabeli
    ```
7. Wstawianie wartości 
    ```sql
    INSERT INTO nazwaTabeli VALUES
    (wartości) 
    ```
8. Zmiana wartości
    ```sql
    UPDATE nazwaTabeli 
    SET nazwaKolumny = wartość
    WHERE warunek
    ```
9. Usuwanie z tabeli 
    ```sql
    DELETE FROM nazwaTabeli
    WHERE warunek
    ```
10. Usuwanie tabeli
    ```sql
    DROP nazwaTabeli
    ```

### Porównywanie napisów

```sql
WHERE nazwaPola LIKE warunek
```

% - 0 lub więcej znaków <br>
_ - pojedynczy znak <br>
[] - pojednyczy znak z zakresu <br>
[^] - pojednyczy znak z poza zakresu


## Wykład nr 5

---

### Złączenia teoriomnogościowe

* UNION

    Złączenie wyników kilku zapytań w jednym zestawieniu. Powtarzające wiersze nie są wybierane i wyniki są sortowane.

    ```sql
    SELECT * FROM tabela1
    UNION
    SELECT * FROM tabela2
    ```

* UNION ALL 

    Zwraca złączenie wszystkich wyników z duplikatami.

    ```sql
    SELECT * FROM tabela1
    UNION ALL
    SELECT * FROM tabela2
    ```

* CROSS JOIN

    Zwraca wszystkie możliwe kombinacje jakie były w wierszach łączonych tabel.

    ```sql
    SELECT tabela1.kolumna1 AS t1k1, tabela1.kolumna2 AS t1k2, tabela2.kolumna1 AS t2k1, tabela2.kolumna2 AS t2k2
    FROM tabela1 CROSS JOIN tabela2
    ```

* INTERSECT 

    Zwraca tylko wspólne wiersze.

    ```sql
    SELECT * FROM tabela1
    INTERSECT
    SELECT * FROM tabela2
    ```

### Złączenie wewnętrzne

Jest to podzbiór iloczynu kartezjańskiego spełniający podane warunki złączenia.

```sql
SELECT * FROM tabela1 JOIN tabela2 ON warunek
```

W momencie gdy mamy w onu tabelach takie same nazwy kolumn to wykonując złączenie musimy się odnieść do nazwy tabeli. W takim przypadku można też użyć konstrukcji z USING

```sql
SELECT * FROM tabela1 JOIN tabela2 
USING (kolumna)
```

### Złączenie naturalne 

Łączy po wszystkich powtarzających się kolumnach. A tylko jeden powtarzający się atrybut dodawany jest do wyniku.

```sql
SELECT * FROM tabela1 NATURAL JOIN tabela2
```

### Złączenie $\theta$ (theta)

Warunek złączenia zapisujemy w WHERE

```sql
SELECT tabela1.kolumna1 AS t1k1, tabela1.kolumna2 AS t1k2, tabela2.kolumna1 AS t2k1, tabela2.kolumna2 AS t2k2
FROM tabela1, tabela2
WHERE warunek
```

### Złączenia zewnętrzne

Ten typ złączeń może obejmować krotki które nie należą do iloczynu kartezjańskiego tabel wejściowych.

* RIGHT JOIN

    Zwracane są wszystkie rekordy z prawej tabeli i pasujące rekordy z lewej tabeli. Tam gdzie nie ma dopasowania dla elementów z prawej tabeli w lewej uzupełniane są `NULL`.

    ```sql
    SELECT * FROM tabela1 RIGHT JOIN tabela2
    ON warunek
    ```

* LEFT JOIN

    Zwracane są wszystkie rekordy z lewej tabeli i pasujące rekordy z prawej tabeli. Tam gdzie nie ma dopasowania dla elementów z lewej tabeli w prawej uzupełniane są `NULL`.

    ```sql
    SELECT * FROM tabela1 LEFT JOIN tabela2
    ON warunek
    ```

* Pełne złączenie zewnętrzne

    Jest połączeniem lewego i prawego złączenia.

    ```sql
    SELECT * FROM tabela1 RIGHT JOIN tabela2
    ON warunek
    UNION 
    SELECT * FROM tabela1 LEFT JOIN tabela2
    ON warunek
    ```

* INNER JOIN

    Zwraca tylko te dane które są złączeniem obu tabel i mają odpoweidniki w drugiej tabeli.

    ```sql
    SELECT * FROM tabela1 INNER JOIN tabela2
    ON warunek
    ```

### Typy złączeń

* Proste
* Drzewiaste
* Zapętlone

### Podzapytanie

Jest to zapytanie SQL umieszczone wewnątrz innego zapytania. 

* Tworzenie strukturalnych podzapytań 
* Izolowanie poszczególnych instrukcji
* Alternatywne rozwiązania dla skomplikowanych złączeń
* Większa czytelność kodu

Możemy też zamiast zapytania do tabeli wykonywać zapytanie do wyniku innego podzapytania albo użyć podzapytania jako wyrażenie w liście polecenia `SELECT`

### Operatory podzapytań

* ANY

    Coś musi spełnić relację z miniumum jedną wartością z drugiej relacji.

* IN

    Coś musi być równe minumum jednej wartości z innej relacji.

* ALL

    Coś musi spełnić relacją z każdym wynikiem innej relacji.

* EXISTS

    Warunek jest prawdziwy jeśli podzapytanie zwraca niepusty zbiór wierszy.

### Podzapytania skorelowane

W podzapytaniach możemy odwoływać się do kolumn występujących w zapytaniach zewnętrznych, wtedy powstaje podzapytanie skorelowane. 

### Grupowanie

Polega ono na utworzeniu **partycji** tabeli czyli rozbiciu jej na rozłączne części, których suma mnogściowa odtwarza tabelę. Przynależność do danej grupy określamy poprzez atrybuty. 

### HAVING

Zwracane są grupy spełniające tylko podane kryterium. Działa ona już po etapie grupowania i filtrowania danych.


## Wykład nr 6

---

### Rodzaje tabel

* tabela podstawowa - jest to tabale utworozna przy pomocy `CREATE TABLE`
* tabela pochodna - jest to wynik każdego zapytania `SELECT` 
* underlying tables - tabela użyta do stworzenia widoków

### Widok

Jest to trwała definicja tabeli pochodnej. Definicja taka przechowywana jest w bazie. Widoki używamy aby ograniczać dostęp danych dla okreslonych użytkowników. 

### Tworzenie widoku

1. Słowo kluczowe `CREATE VIEW`
2. Nazwa widoku
3. Słowo kluczowe `AS`
4. Treść zapytania które buduje nam widok

Widok nazywamy alaisem gdy zwraca nam cąłą tabelę podstawową.

Widok możemy też tworzyć na podstawie innych widoków. 

Widoki reagują na zmianę danych w tabelach których użyto do ich stworzenia. Ale nie reagują one na zmianę definicji tabeli, o ile nie narusza ona integralności widoku.

### Widoki modyfikowalne 

Zmiana danych w widoku może powodować zmianę danych w tabelach używanych do stowrzenia widoku. Ale nie da się dodać lub zmienić wiersza w momencie gdy zmiana ta naruszyła by więzy integralności widoku. 

Wiersza możęmy usówać z widoku tylko wtedy gdy SQL potrafi przetłumaczyć zapytanie usuwające wiersze z widoku na zapytanie usuwające wiersze z underlying table.

### Widoki niemodyfikowalne

Niektórych widoków nie możęmy modyfikować. Są to widoki które zawierają:

- `UNION`
- `UNION ALL`
- `DISTINCT`
- `DISTINCTROW`
- inny widok niemodyfikowalny
- podzapytanie

### Więz `CHECK`

Gdy w zapytaniu tworzącym widok mamy `WHERE` możęmy dodać więz `CHECK` który uniemożliwi zmodyfikowanie danych w widoku które naruszały by to ograniczenie.

### Dangling views

Są to widoki których tabela na której są budowane zostanie usunięta. 

Aby dowiedzieć się czy dana tabela lub widok nie są uszkodzone używamy `CHECK TABLE nazwaTabeli`

### Widoki zmaterializowane

Są to widoki które fiycznie przechowują dane, tworzymy kopię danych będącej wynikiem zapytaniem zadanego tabeli na odległym lub rozproszonym serwerze. Dostęp do takich danych jest szybszy, ale co jakiś czas należy taki widok odświeżyć.

> Dane w takich widokach mogą chwilowo łamać wymóg spójności danych.

### Klucze obce 

Jest to powiązanie indeksowanej kolumny jakiejś tabeli z indeksowaną kolumną innej tabeli co pozwala na automatyczne zmiany w powiązanych tabelach i nakłada więzy integralności.

```SQL
FOREIGN KEY (nazwaKolumny) REFERENCES nazwaTabeli (nazwaKolumny)
    [{ON DELETE | ON UPDATE} {RESTRICT | CASCADE | SET NULL | NO ACTION}]
```

`ON DELETE` - sprawdzanie stanu przy usuwaniu

`ON UPDATE` - sprawdzanie stanu przy modyfikacji

`RESTRICT` - nie pozwala na dokonanie zmian naruszającyh powiązanie

`CASCADE` - nakazuje na propagację kaskadową zmian wzdłóż drzewa powiązanych tabel

`SET NULL` - ustawia odpowiednie atrybuty powiązanych tabel, dotąd wskazujący na element klucza obcego na wartość `NULL` 

`NO ACTION` - wyłącza mechanizm klucza obcego dla danej operacji

### Wyzwalacze

Są to procedury wykonywane automatycznie po zmianie zawartości wskazanej tabeli.

```SQL
CREATE TRIGGER nazwa
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON nazwaTabeli
FOR EACH ROW
wyrażenieSQL
```

> Nogą się odwoływać tylko do trwałych tabel podstawowych. I może być co najwyżej jeden typ wyzwalacza na tabelę.

> Wyzwalacze nie są uruchamiane przez zdarzenia kaskadowe kluczy obcych.

> Wyzwalacz nie może zacząć, skończyć i odwołać transakcji.

### Do czego wyzwalacze?

- Zapisywanie w logu danych dotyczących zmian
- Uruchamianie kaskady zdarzeń `DELETE` i `UPDATE`
- Automatyzowanie operacji które powinny być wykonane po zmianie wiersza w jakiejś tabeli
- Wyzwalaczy możemy używać do modyfikacji wielkości zapisanych w innych tabelach niż w tabeli w której zdefiniowano wyzwalacz

### Wady wyzwalaczy 

- Błędy spowodowane ich działaniem trudne do wytropienia
- Użytkownicy zaskoczeniu zmianami
- Wyzwalacz modyfikujący tabele z wyzwalaczem może spowodować nawałnicę wyzwalaczy


## Wykład nr 7

---

### Transakcje

Są to zbiory operacji w bazie danych stanowiące pewną całość i jako takie powinny być wykonane w całośći wszystkie lub żadna z nich. Jeżeli wystąpi jakiś błąd to całą sekwencję operacji można cofnąć i przywrócić bazę do stanu sprzed rozpoczęcia sekwencji. W przypadku systemu wielodostępowego ważne jest też zapewnienie aby procesy odwołujące się do tych samych tabel nie kłóciły się ze sobą. 

> **Spójność danych w bazie rozproszonej** - każdy serwer musi zwrócić taką samą odpowiedź na dane zapytania gdy zadajemy je w tym samym czasie.

```SQL
START TRANSACTION;
zapytanie1;
...
zapytanieN;
COMMIT; -- zatwierdza zmiany
ROLLBACK; -- odrzuca zmiany
```

### Zasady ACID

- Atomicity - atomowość 

    Transakcja jest niepodzielna. Albo wszystko się wykona albo nic.

- Consistency - spójność 

    Transakcje nie mogą naruszać integralności danych. Serwery muszą przechowywać tę samą bazę i więzy integralności muszą zostać zachowane.

- Isolation - izolacja

    Transakcja nie może widzieć wyników innej niezatwierdzonej transakcji. Musi się ona odbywać w czasie w którym żadna inna nie trwa.

- Durability - trwałość

    Zmiany wprowadzone w transakcji zatwierdzonej muszą być stałe.

### Wielodostęowość - problemy

1. Niespójność odczytów - transakcja odczytuje zmiany wprowadzone przez inną niezatwierdzoną jeszcze transakcję.

2. Niepowtarzalność odczytów - transakcja odczytuje dane kilka razy i dostaje różne wyniki mimo że nie została jeszcze zatwierdzona.

3. Odczyty fantomowe - jedna transakcja dodaje wiersz, druga aktualizuje. Nowy wiersz nie został zaktualizowany. 

### Izalacja 

Transakcje blokują tabele lub ich fragmenty które są im potrzebne. 

- 2PL (strict two-phase locking)

    Transakcja zakłada blokadę na rekord który chce odczytać. Zakłąda też wyłączną transakcję na fragment danych które chce zapisać. Zakładane jest że odczytywane dane będą w tym samym czasie regularne modyfikowane. 

- OCC (optimistic concurrency control)

    Zakłada że w czasie gdy jeden użytkownik odczytuje to inni nie będą modyfikować. Wiele może jednocześnie modyfkiwać i odczytywać ale dokonują zapisu histori operacji. Następnie jeśli wykryto konflikt to jedna z transakcji jest odwoływana. Tylko modyfikujący blokuję innych modyfikujących. 

    **Algorytm**

    1. Begin - zapis czasu startu
    2. Modify - odczyt i zapis zmian do `WAL` czyli dziennika systemowego w którym indeksowane są operacje. W systemie istnieje też `Undo log` zawierający informacje które w przyszłości należało by wycofać.
    3. Validate - sprawdzenie czy inne transakcje nie modyfikowały danych które używała bierząca transakcja. 
    4. Commit/Rollback

> Instrukcje DDL nie są transakcyjne - tworzenia, usuwania, modyfikacji bazy i tabeli nie można wycofać. 

### 2PC (two-phase COMMIT)

Jeden węzeł sieci jest koordynatorem (TM) i działa jako master. Pozostałe węzły to Resource Menagers. Wszystkie węzły uczesniczące w transakcji tworzą *kohortę*. Koordynator rozpoczyna 2PC i członkowie kohorty albo zgadzają się na zapis zmian albo przerywają transakcję. 

- Faza commit request

    1. TM wysyła zapytanie o gotowości wszystkich członków i czeka na odpowiedź.
    2. Każdy RM wykonuje transakcje aż do punktu w którym wydaje COMMIT a także przygotowuje swój undo log.
    3. Ci którym się udał pkt 2 zgłaszają koordynatorowi że można zaakceptować transakcję.

- Faza commit (jeśli wszyscy członkowie kohorty zatwierdzili)

    1. TM wysyła polecenie COMMIT do wszystkich członków
    2. RM zatwierdzają transakcję na swoich węzłach i zwalniają blokady 
    3. RM wysyłają potwierdzenie do koordynatora
    4. TM zatwierdza transakcję i zwalnia blokady po otrzymaniu wszystkich potwierdzeń

- Gdy którykolwiek z RM zasygnalizuje brak zgody lub gdy nastąpi timeout

    1. TM wysyła polecenie ROLLBACK do wszystkich członków
    2. RM wycofują transakcję i zwalniają blokady 
    3. RM wysyłają potwierdzenie do koordynatora
    4. TM wycofuje transakcję i zwalnia blokady po otrzymaniu wszystkich potwierdzeń

> Wadą jest blokowanie danych przez członków kohorty, jeśli koordynator ulegnie awarii lub zostanie przerwana komunikacja niektórzy nie będą wiedzieć jak zakończyć transakcję. Wtedy jest timeout i powiadamiają użytkownika ale TM dalej znajduje się w stanie niewiadomym. 

### Blokowanie tabel 

```SQL
LOCK TABLES nazwa_tabeli [READ | [LOW PRIORITY] WRITE];
```

`READ` - czytanie tabeli, brak zgody na zapis

`WRITE` - brak zgody innym na zapis i odczyt

`LOW PRIORITY WRITE` - zezwala innym na założenie `READ`

`UNLOCK TABLES;` - zwalnia wszystkie zablokowane przez wątek tabele


## Wykład nr 8

---

### Procedury składowane

Używane są do wykonywania powtarzających się i nie wymagających ingerencji użytkownika zadań. 

- Jest to rodzaj skryptu przechowywanego w schemacie bazy
- Posiada parametry wejściowe, wyjściowe i wartości wynikowe
- Uruchamiana jak pojedyncza instrukcja 

```SQL
CREATE PROCEDURE nazwa(parametry)
    deklaracje lokalne
    treść procedury;
```

> Ważne aby redefiniwoać średnik poleceniem `DELIMITER`

Procedurę wywołujemy używająć instrukcji `CALL`

Procedurę usuwamy używając `DROP PROCEDURE nazwa`

Deklaracja zmiennych lokalnych i przypisanie:

```SQL 
DECLARE nazwa typ;

SET zmienna = wyrażenie;
```

> Procedury nie mogą zmieniać innych procedur, funkcji i trigerów. Mogą natomiast modyfikować, usuwać, tworzyć tabele i widoki. 

### Parametry wywołania

Parametry są trójkami - tryb, nazwa, typ.

- IN

    Jest to tryb domyślny, przekazuje wartość do programu ze środowiska. Zachowuje się jak stała i nie można mu przypsiać wartości. 

- OUT

    Musi zostać określony, przekazuje wartość do programu ze środowiska. Zachowuje się jak nie zainicjalizowana zmienna. 

- IN OUT

    Musi zostać określony, przekazuje wartość do programu ze środowiska i na odwrót. Zachowuje się jak zainicjalizowana zmienna. 

### Zalety procedur składowanych 

- Mniejsze ryzyko błędu gdy aplikacje używają procedur
- Zapewniają bezpieczeństwo 
- Ograniczają liczbę danych przesyłanych między serwerem a klientem
- Umożliwiają pisanie całych bibliotek
- Ułatwiają obsługę błędów

### Instrukcje

```SQL
-- instrukcja warunkowa
IF warunek THEN
    instrukcja;
ELSE 
    instrukcja;
END IF;
```

```SQL
-- instrukcja case
CASE zmienna
    WHEN wartość THEN insturkcja;
    WHEN wartość THEN insturkcja;
    ELSE instrukcja;
END CASE;
```

```SQL
-- pętla while
WHILE warunek DO
    instrukcje
END WHILE;
```

```SQL
-- pętla repeat
REPEAT
    instrukcje
    UNTIL warunek
END REPEAT;
```

```SQL
-- pętla loop
LOOP
    instrukcje
END LOOP;
```

> Loop jest etykietowane aby można było ją przerywać stosując instrukcję `LEAVE etykieta`

`ITERATE` ignoruję dalszy fragment pętli i przechodzi do nowej iteracji.

### Funkcje składowane

Nie mają dostęu do danych przechowywanych w bazie i mogą przyjmować tylko parametry wejściowe.

```SQL
CREATE FUNCTION nazwa(parametry)
    RETURNS typ
    deklaracje lokalne
    treść procedury;
```

### Kursory

Pozwalają na obsługę tabel wiersz po wierszu. Realuzujemy je używając procedur składowanych. Kursor jest wskaźnikiem na krotkę danych.

### Operacja na kursorze

- Zadeklarowanie `DECLARE nazwa CURSOR FOR zapytanie`
- Otwarcie `OPEN nazwa`
- Pobranie wiersza z bazy `FETCH nazwa INTO lista zmiennych`
- Zamknięcie `CLOSE nazwa`

> Zmiany wprowadzone po otwarciu kursora nie są w nim widoczne.


## Wykład nr 9

---

### Przeszukiwanie posortowanego pliku 

Znalezienie wiersza w takim pliku o długości N wymaga dokonania $O(\log_2N)$ porównań i dostępów do dysku. 

> Tabele w bazie nie są posortowane. Zapisywanie za każdym razem sortowanych danych znacząco spowolnił by działanie.

### Indeksy 

Specjalna struktura przechowująca tylko atrybuty względem których sortujemy (klucze sortowania). Wraz z kluczem przechowywany jest fizyczny adres krotki na dysku.

### B-drzewo

1. Jest to drzewo ukorzenione
2. Każdy węzeł ma nie więcej niż *m* potomków
3. Każdy węzeł (oprócz korzenia i liści) ma nie mniej niż *m/2* potomków. Jest to zaokrąglane w dół i nazywane **czynnikiem minimalizacji**
4. Korzeń ma minimum dwóch potomków
5. Wszystkie liście leżą na tym samym poziomie
6. Węzeł posiadający *k* potomków ma *k-1* kluczy
7. Węzeł ma nie więcej niż *m-1* kluczy. Liść natomiast posiada nie mniej niż *(m/2)-1* kluczy

> Budjąc b-drzewo węzły pozostawia się nie do końca wypełnione, ułatwia to później wstawianie nowych elementów.

### Wyszukwianie

Zaczynamy od korzenia, każdy węzeł przeszukujemy przeglądająć kolejne klucze które są w porządku niemalejącym. Gdy znajdziemy wartość większą lub równą poszukiwanej wiemy że poszukwiana wartość znajduje się w poddrzewie którego korzeniem jest znaleziona wartość. Czas przeszukwiania wynosi $O(\log_{m/2}N)$.

### Podział

Medianę węzła dzielonego wstawimy do jego rodzica. Następnie tworzymy nowy węzał i wstawiamy do niego wartośći większe od mediany. Z dzielonego usuwamy medianę i wartości od niej większe. Proces podziału to koszt stału O(m). 

### Wstawianie klucza

Najpierw przeszukujemy drzewo i znajdujemy odpowiedni liść gdzie należy wstawić wartość. Gdy wstawienie powoduje przepełnienie dokonujemy podziałów. Wstawianie kluczy niesie koszt $O(m\log_{m/2}N)$.

### Usuwanie kluczy 

Po usunięciu klucza z drzewa należy je najcześniej zrównoważyć. 

### Indeksy w SQL

Klucz główny zawsze jest indeksem. Gdy chcemy stworzyć klócz główny na kilka kolumn podczas tworzenia tabeli dopisujemy `PRIMARY KEY(kol1, kol2)`. 

Dodatkowe indeksy możemy tworzyć w czasie tworzenia tabeli poprzez `INDEX nazwa (kolumna)` lub osobnym polecniem `CREATE INDEX nazwa on tabela (kolumny)`.

> Efektywność wykorzystania indeksów zależy od tego jak duży procent tabeli zwraca zapytanie. 

### Wymuszanie indeksów

W większości przypadków optymalizator sam wybiera czy używac indeksów i jakich. Gdy chcemy wymusić indeksy możemy użyć:

- przeglądanie ze wskazanym indeksem `SELECT ... FROM tabela USE INDEX (nazwaIndeksu)`
- przeglądanie ze wskazanym indeksem i zakazem pełnego przeglądania tabeli `SELECT ... FROM tabela FORCE INDEX (nazwaIndeksu)`
- ignorowanie wskazanego indeksu `SELECT ... FROM tabela USE INDEX (nazwaIndeksu)`

### Update

Przy updatowaniu danych wykorzystująć indeksy możę się zdarzyć że kilkukrotnie zmienimy jedną krotkę ponieważ indeks się przebuduje i ponownie wskaże nam daną krotkę do zmiany. Musimy więc używając indeksów stworzyć tabelę pomocniczą wybranych krotek, dalej przeglądamy tabelę z kluczami krotek które trzeba zmienić i używając indeksu z kluczem głównym zmieniamy krotki w głównej tabeli. 

### Wyszukiwanie pełnokontekstowe 

Służy do znajdywania podanych ciągów znaków. Zakłąda się specjamy indeks `FULLTEXT(kolumny)`. Następnie mamy zapytanie `SELECT` z elementem `WHERE MATCH(kolumny) AGAINST(wzorzec)`.