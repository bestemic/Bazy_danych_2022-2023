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

cdn.