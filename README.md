# Java to Python translator

### Cel
Celem projektu była realizacja translatora podzbioru języka Java do języka Python.
Podczas implementacji należało skorzystać z generatora skanerów oraz parserów, w zależności
od wybranego języka programowania do implementacji translatora.

### Stos technologiczny
- **Java** - implementacja translatora
- **ANTLR** - generator analizatora składni

ANTLR został dołączony w postaci Maven plugin co pozwala w wygodny sposób skonfigurować środowisko, bez konieczności pobierania i instalowania biblioteki .jar.
 
### Określenie gramatyki, wygenerowanie lexera oraz parsera
Wykorzystany został gotowy pliku gramatyki Javy w wersji 8, który znajdował się w głównym repozytorium projektu ANTLR – plik Java8.g4.

Za pośrednictwem komendy `mvn package` zostaje wygenerowanych kilka plików na podstawie pliku gramatyki Java8.g4.
<img width="150" alt="Screenshot 2021-08-15 at 13 28 31" src="https://user-images.githubusercontent.com/34041060/129477105-caf1efd2-3b4b-4453-8dde-17374259b51e.png">

- **Java8Lexer.java** – zawiera implementację lexera dla gramatyki. Są to reguły, które przekształcają słowa wejściowe na tokeny. Zapisane są w gramatyce w postaci dużych liter lub jako symbole w apostrofach.
- **Java8Paraser.java** – zawiera implementację parsera dla gramatyki. Są to reguły, które przekształcają tokeny wejściwe na drzewo syntaktyczne zgodnie z produkcjami zapisanymi w gramatyce.
-  **Java8Listener.java i Java8BaseListener** – to interfejs i klasa, które umożliwiają przechodzenie po drzewie syntaktycznym poprzez mechanizm listenerów.
 
### Testy działania lexera oraz parsera
Aby móc przetestować Lexer oraz Parser za pośrednictwem org.antlr.v4.gui.TestRig była konieczna instalacja ANTLR:
1. Dodanie klas z pobranego pliku do zmiennej CLASSPATH.
2. Utworzenie aliasów, które uproszczą składnię z linii komend – plik .bash_profile /plik .zshrc:
<img width="600" alt="Screen Shot 2021-08-15 at 14 30 45 PM" src="https://user-images.githubusercontent.com/34041060/129478702-32444c87-f598-431a-9a8c-ae16f532198b.png">
3. Skompilowanie wszystkich wygenerowanych plików .java: `javac Java8*.java`

### Testowe wykonanie programu




