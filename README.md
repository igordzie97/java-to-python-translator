# Java to Python translator

## Spis Treści
1. [Opis](#opis)
2. [Stos technologiczny](#stos-technologiczny)
3. [Określenie gramatyki, wygenerowanie lexera oraz parsera](#określenie-gramatyki-wygenerowanie-lexera-oraz-parsera)
4. [Testy działania lexera oraz parsera](#testy-działania-lexera-oraz-parsera)
5. [Opis działania programu](opis-działania-programu)

## Opis

Celem projektu była realizacja translatora podzbioru języka Java do języka Python.
Podczas implementacji należało skorzystać z generatora skanerów oraz parserów, w zależności
od wybranego języka programowania do implementacji translatora.

## Stos technologiczny
- **Java** - implementacja translatora
- **ANTLR** - generator analizatora składni

ANTLR został dołączony w postaci Maven plugin co pozwala w wygodny sposób skonfigurować środowisko, bez konieczności pobierania i instalowania biblioteki .jar.
 
## Określenie gramatyki, wygenerowanie lexera oraz parsera
Wykorzystany został gotowy pliku gramatyki Javy w wersji 8, który znajdował się w głównym repozytorium projektu ANTLR – plik Java8.g4.

Za pośrednictwem komendy `mvn package` zostaje wygenerowanych kilka plików na podstawie pliku gramatyki Java8.g4.

<img width="150" alt="Screenshot 2021-08-15 at 13 28 31" src="https://user-images.githubusercontent.com/34041060/129477105-caf1efd2-3b4b-4453-8dde-17374259b51e.png">

- **Java8Lexer.java** – zawiera implementację lexera dla gramatyki. Są to reguły, które przekształcają słowa wejściowe na tokeny. Zapisane są w gramatyce w postaci dużych liter lub jako symbole w apostrofach.
- **Java8Paraser.java** – zawiera implementację parsera dla gramatyki. Są to reguły, które przekształcają tokeny wejściwe na drzewo syntaktyczne zgodnie z produkcjami zapisanymi w gramatyce.
-  **Java8Listener.java i Java8BaseListener** – to interfejs i klasa, które umożliwiają przechodzenie po drzewie syntaktycznym poprzez mechanizm listenerów.
 
## Testy działania lexera oraz parsera
Aby móc przetestować Lexer oraz Parser za pośrednictwem org.antlr.v4.gui.TestRig była konieczna instalacja ANTLR:
1. Dodanie klas z pobranego pliku do zmiennej CLASSPATH.
2. Utworzenie aliasów, które uproszczą składnię z linii komend – plik .bash_profile /plik .zshrc:
<img width="600" alt="Screen Shot 2021-08-15 at 14 30 45 PM" src="https://user-images.githubusercontent.com/34041060/129478702-32444c87-f598-431a-9a8c-ae16f532198b.png">
3. Skompilowanie wszystkich wygenerowanych plików .java:

`javac Java8*.java`

### Test działania Lexera
Wykorzystane narzędzie to dostarczone przez ANTLR, Testring. Komenda przyjmuje następujące argumenty:
- Nazwa gramatyki / paczki implementującej Lexer: `Java8`.
- Nazwa reguły: `java8_file`.
- Opcja wygenerowanego wyniku: tokens (analiza wygenerowanych tokenów).
- Ścieżka do pliku testowego: `ToBeTranslated.java`

**Polecenie:**

` grun Java8 java8 -tokens ToBeTranslated.java`


**Fragment wykonanego polecenia:**

<img width="200" alt="Screenshot 2021-08-15 at 13 28 31" src="https://user-images.githubusercontent.com/34041060/129479784-88726368-f9ba-4fb6-9150-c612de53920d.png">

W skład każdego tokenu wchodzi:
1. Numer tokenu.
2. Numer początkowego i końcowego znaku, z którego skłąda się token.
3. Tekst z jakiego składa się token.
4. Typ tokenu (regułaa z gramatyki zaczynająca się z dużej litery lub symbol w apostrofach).
5. Pozycja tokenu (numer wiersza oraz numer znaku w tym wierszu).

<img width="400" alt="Screenshot 2021-08-15 at 13 28 31" src="https://user-images.githubusercontent.com/34041060/129480440-24a985b6-0f53-4d36-aa44-a797597ccfe5.png">

### Test działania Parsera
Wykorzystane narzędzie to również Testring, tak jak w przypadku Lexera. Komenda przyjmuje następujące argumenty:
- Nazwa gramatyki / paczki implementującej Lexer: `Java8`
- Nazwa reguły: `java8_file`
- Opcja wygenerowanego wyniku: `tree` (analiza wygenerowanego drzewa synaktycznego)
- Ścieżka do pliku testowego: `ToBeTranslated.java`
- Flaga: `gui` (pozwala na wizualizację drzewa synaktycznego - bez tego generowane jest w formie tekstu).

**Polecenie:**

`grun Java8 methodDeclaration -tree ToBeTranslated.java -gui`

**Rezultat wykonanego polecenia:**

<img width="1030" alt="Screen Shot 2021-08-15 at 15 48 24 PM" src="https://user-images.githubusercontent.com/34041060/129480738-4419946c-de09-4a1d-845b-5a93765413af.png">

## Opis działaniu programu
Sposób przechodzenia po drzewie opiera się na mechanizmie listenerów, które reagują na wydarzenia związane z przechodzeniem po drzewie syntaktycznym. Podstawowymi
zdarzeniami są wejścia i wyjścia z danego typu węzła.

**Zaimplementowane Listenery w klasie JavaToPythonListener:**
- Deklaracja metody
- Deklaracja argumentów w metodzie
- Deklaracja zmiennych
- Deklaracja klasy
- Definicja pętli for oraz preinkrementacji i postinkrementacji
- Definicja metody print()
- Definicja instrukcji warunkowej oraz wyrażenia warunkowego
- Definicja instrukcji return

### Plik wejściowy:
<img width="230" alt="Screen Shot 2021-08-15 at 17 32 30 PM" src="https://user-images.githubusercontent.com/34041060/129483848-b352c44e-1003-4c39-9be7-77fcaf2140a1.png">

### Rezultat programu:
<img width="1000" alt="Screen Shot 2021-08-15 at 17 34 49 PM" src="https://user-images.githubusercontent.com/34041060/129483921-ddb7ac2d-e893-412e-99c0-3a6d7b83d2f5.png">

## Autorzy
- Igor Dzierwa
- Adrian Nędza
