# Java to Python Translator

## Table of Contents
1. [Description](#description)
2. [Technologies](#technologies)
3. [Definition of grammar, lexer and parser generation](#definition-of-grammar-lexer-and-parser-generation)
- [Lexer](#lexer)
- [Parser](#parser)
5. [Functional testing of lexer and parser](#functional-testing-of-lexer-and-parser)
6. [Description of translator functionality](#description-of-translator-functionality)
7. [Documentation](#documentation)

## Description
The project puropse was to implement translator from subset of Java language to Python. During implementation it was essential to use specific lexer and parser generator (depending on selected programming language).

## Technologies
- **Java** - Translator implementation
- **ANTLR** - Lexer and parser generator

ANTL is attached using Maven plugin - it is the easiest way to set a project using ANTLR, without without downloading and installing .jar library.
 
## Definition of grammar, lexer and parser generation
**Grammar:** Is is used pre-prepared grammar file by ANTL - [java8.g4](https://github.com/antlr/grammars-v4/tree/master/java/java8).

`mvn package` - generating Java code corresponding to the given grammar file (names of files are based on the name of the grammar file):

<img width="150" alt="Screenshot 2021-08-15 at 13 28 31" src="https://user-images.githubusercontent.com/34041060/129477105-caf1efd2-3b4b-4453-8dde-17374259b51e.png">

- `Java8Lexer.java` – includes lexer implementation. There are defined rules which transform input words to tokens.
- `Java8Paraser.java` – includes parser implementation. There are defined rules which trasnform tokens to syntactic tree.
- `Java8Listener.java, Java8BaseListener` – these files describe interface and class which allow to traverse within syntactic tree using listeners mechanism.
 
## Functional testing of lexer and parser
Aby móc przetestować Lexer oraz Parser za pośrednictwem org.antlr.v4.gui.TestRig była konieczna instalacja ANTLR:
1. Dodanie klas z pobranego pliku do zmiennej CLASSPATH.
2. Utworzenie aliasów, które uproszczą składnię z linii komend – plik .bash_profile /plik .zshrc:
<img width="600" alt="Screen Shot 2021-08-15 at 14 30 45 PM" src="https://user-images.githubusercontent.com/34041060/129478702-32444c87-f598-431a-9a8c-ae16f532198b.png">
3. Skompilowanie wszystkich wygenerowanych plików .java:

`javac Java8*.java`

### Lexer
Wykorzystane narzędzie to dostarczone przez ANTLR, Testring. Komenda przyjmuje następujące argumenty:
- Nazwa gramatyki / paczki implementującej Lexer: `Java8`.
- Nazwa reguły: `java8_file`.
- Opcja wygenerowanego wyniku: tokens (analiza wygenerowanych tokenów).
- Ścieżka do pliku testowego: `ToBeTranslated.java`

**Command:**

` grun Java8 java8 -tokens ToBeTranslated.java`


**Command result (fragment):**

<img width="200" alt="Screenshot 2021-08-15 at 13 28 31" src="https://user-images.githubusercontent.com/34041060/129479784-88726368-f9ba-4fb6-9150-c612de53920d.png">

**Token structure:**
1. Numer tokenu.
2. Numer początkowego i końcowego znaku, z którego skłąda się token.
3. Tekst z jakiego składa się token.
4. Typ tokenu (regułaa z gramatyki zaczynająca się z dużej litery lub symbol w apostrofach).
5. Pozycja tokenu (numer wiersza oraz numer znaku w tym wierszu).

<img width="400" alt="Screenshot 2021-08-15 at 13 28 31" src="https://user-images.githubusercontent.com/34041060/129480440-24a985b6-0f53-4d36-aa44-a797597ccfe5.png">

### Parser
Wykorzystane narzędzie to również Testring, tak jak w przypadku Lexera. Komenda przyjmuje następujące argumenty:
- Nazwa gramatyki / paczki implementującej Lexer: `Java8`
- Nazwa reguły: `java8_file`
- Opcja wygenerowanego wyniku: `tree` (analiza wygenerowanego drzewa synaktycznego)
- Ścieżka do pliku testowego: `ToBeTranslated.java`
- Flaga: `gui` (pozwala na wizualizację drzewa synaktycznego - bez tego generowane jest w formie tekstu).

**Command:**

`grun Java8 methodDeclaration -tree ToBeTranslated.java -gui`

**Command result:**

<img width="1030" alt="Screen Shot 2021-08-15 at 15 48 24 PM" src="https://user-images.githubusercontent.com/34041060/129480738-4419946c-de09-4a1d-845b-5a93765413af.png">

## Description of translator functionality
Sposób przechodzenia po drzewie opiera się na mechanizmie listenerów, które reagują na wydarzenia związane z przechodzeniem po drzewie syntaktycznym. Podstawowymi
zdarzeniami są wejścia i wyjścia z danego typu węzła.

**Implemented Listeners in JavaToPythonListener class:**
- Method declaration
- Method arguments declaration
- Variables declaration
- Class declaration
- Loop definition and preincrementation / posincrementation
- Print method definition
- Conditional statement definition
- Return instruction definition

### Input file:
<img width="230" alt="Screen Shot 2021-08-15 at 17 32 30 PM" src="https://user-images.githubusercontent.com/34041060/129483848-b352c44e-1003-4c39-9be7-77fcaf2140a1.png">

### Program result:
<img width="1000" alt="Screen Shot 2021-08-15 at 17 34 49 PM" src="https://user-images.githubusercontent.com/34041060/129483921-ddb7ac2d-e893-412e-99c0-3a6d7b83d2f5.png">

## Documentation
[Translator documentation (in Polish)](https://github.com/igordzie97/java-to-python-translator/blob/main/documentation/SprawozdanieKompilatory.pdf)

## Authors
- Igor Dzierwa
- Adrian Nędza
