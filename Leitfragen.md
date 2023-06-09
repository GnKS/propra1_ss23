# Lösungen zu Leitfragen

## Woche 1

### Aufgaben/Leitfragen Die Java-Klassenbibliothek

#### Fassen Sie zusammen, welche konkreten Collection-Klassen für welche Zwecke verwendet werden. Suchen Sie für die Verwendung jeweils ein Beispiel.
- HashSet: Elemente kommen höchstens ein mal vor. Beispiel: Eine Liste von Elementen die nicht doppelt benötigt werden und wo die Reihenfolge der Elemente egal ist. Bei z.B. einer Such oder Filterfunktion.
- TreeSet Elemente werden aufsteigend sortiert. Ist eine navigierbare Menge an Objekten dir zur Navigation in Objekten einer Klasse verwendet werden kann
- LinkedList doppelt verkettete Liste, jeder Knoten in der Liste hat eine Referenz auf den Nachfolger und den Vorgänger Beispiel: Queue
- ArrayList ist eine sequenzartige dynamische Datenstruktur, verwendet intern ein Array zur Datenspeicherung, sehr effizient auf beliebige Elemente per Index zuzugreifen. Beispiel: Daten organisieren

#### Was macht die Methode retainAll? Angenommen, wir verwenden zwei Mengen: Welcher mathematischen Operation entspricht retainAll? Implementieren Sie ein Beispiel.
- `retainAll` löscht alles was nicht in der Schnittmenge von zwei Mengen ist. Wenn man retainAll auf nur eine Menge anwendet wird nichts gelöscht.
```java
public class MyClass {
    public static void main(String args[]) {
        List<Integer> l1 = new ArrayList<>();
        List<Integer> l2 = new ArrayList<>();
        l1.addAll(List.of(1,2,3,4));
        l2.addAll(List.of(1,5,3,9));
        
        l2.retainAll(l1);
        
        for(int i=0; i<l2.size(); i++)
            System.out.println( l2.get(i) ); // => 1,3
    }
}
```

#### Im obigen Beispiel zu sortierten Mengen findet sich folgende Zeile ``Set<Integer> ints = new TreeSet<>();`` Muss es auf der linken Seite nicht SortedSet heißen? Warum (nicht)?
- Nein, muss es nicht da SortedSet Set erweitert und TreeSet SortedSet implementiert.

#### Schauen Sie sich den Comparator aus dem Beispiel ganz genau an und gehen Sie alle möglichen Eingaben durch (zwei unterschiedliche gerade Zahlen, zwei unterschiedliche ungerade Zahlen, eine gerade und eine ungerade Zahl, eine ungerade und eine gerade Zahl, zweimal die selbe Zahl) und schreiben Sie auf, welches Resultat Sie erhalten.
- Zwei unterschiedliche gerade Zahlen (eingabe 6,4) ausgabe 4,6
- Zwei unterschiedliche ungerade Zahlen (eingabe 5,3) ausgabe 3,5
- Eine gerade und eine ungerade Zahl (eingabe 4,7) ausgabe 4,7
- Eine ungerade und eine gerade Zahl (eingabe 3,4) ausgabe 4,3
- Zweimal die selbe Zahl (eingabe 2,2) ausgabe 2

#### Angenommen, wir wollen eine statische compareTo-Methode für int schreiben. Ein Vorschlag für die Implementierung ist: ``public static int compareTo(int a, int b) { return a - b; }`` Die Methode liefert einen negativen Wert für a < b, einen positiven Wert für a > b und bei Gleichheit den Wert 0. Warum wäre eine solche Implementierung nicht korrekt? Geben Sie ein Beispiel für a und b an, bei dem die Methode versagt.
- Die Methode versagt zum Beispiel in dem Max int bereich a = -2147483648 (32-bit int) und b = 1 die Methode sollte einen negativen Wert liefern da a < b liefert aber einen positiven.

#### Wir benötigen ein Wörterbuch, bei dem die Wörter der Länge nach durchlaufen werden. Verwenden Sie ein TreeSet und eine passende Implementierung von Comparator. In das Set sollen Wörter gespeichert werden und bei einem Durchlauf sollen die längsten Wörter zuerst rauskommen. Bei gleicher Wortlänge ist die Reihenfolge egal.
- Lösung:
```java
public class MyClass {
    public static int compareTo(int a, int b) { return a - b; }
    
    public static void main(String args[]) {
        Comparator<String> evenFirstComparator = new Comparator<String>() {
          @Override
          public int compare(String o1, String o2) {
            if (o1.length() == o2.length()) {
              return 1;
            }
            if (o1.length() < o2.length()) {
              return 1;
            } else {
              return -1;
            }
          };
        };
        
        SortedSet<String> set = new TreeSet<>(evenFirstComparator);
        set.addAll(List.of("a","kurzes Wort", "Laaaaaaaaaanges Woooooooooort", "Apfel", "Fuenf"));
        System.out.println(set); // => [Laaaaaaaaaanges Woooooooooort, kurzes Wort, Apfel, Fuenf, a]
    }
    
}
```

#### Welchen Fehler haben die beiden Implementierungen von AwkwardMap? Beheben Sie das Problem.
- Lösung text


### Aufgaben/Leitfragen Idiomatische Verwendung von Schleifen

#### Fassen Sie zusammen, welche Schleife für welchen Zweck benutzt wird.
- Rekursion:
    - Algorithmen elegant ausdrücken (wenn man flexen will)
    - selten gute Idee außer diese Variante ist sehr viel einfacher als eine iterative Version
- Enhanced For Loop:
    - Wird verwendet wenn man über eine Sammlung von Werten iteriert
- For-Loop:
    - Wenn mehr als ein Element gleichzeitig oder Index benötigt wird
- While und Do-While:
    - Wenn es keine feste Grenze an Anzahl der Iterationen gibt
    - Do while führt einmal aus bevor die Bedingung geprüft wird

#### Schreiben Sie eine Methode, die eine Liste von Strings bekommt und diese auf der Konsole ausgibt. Verwenden Sie die richtige Art der Iteration.
- ```java
        static void iteratorBoy(List<String> s){
        for(String n : s){
            System.out.println(n);
        }
    }

    public static void main(String[] args) {
        List<String> stringyBoys = List.of("eins", "zwei", "drei", "vier", "fünf");
        iteratorBoy(stringyBoys);
    }
  ```

#### Erklären Sie, was hier passiert: 
```java
List<Integer> zahlen = List.of(1, 2, 3);

for(int zahl: zahlen) {
  zahl = 42;
}

zahlen.forEach(zahl -> System.out.println(zahl)); // Ausgabe: 1 2 3 oder 42 42 42?


List<int[]> komischeMatrix = List.of(new int[]{1, 2}, new int[]{3, 4}); // seltsame Konstruktion, nur fürs Beispiel!

for(int[] array: komischeMatrix) {
  array[0] = 42;
}

komischeMatrix.forEach(array -> System.out.println(array[0])); // Ausgabe: 1 3 oder 42 42?
```
- Bei Liste zahlen will jemand die Zahlen aus der Liste zahlen auf 42 setzen da List.of aber eine unveränderliche Liste erzeugt ist die ausgabe 1 2 3
- Bei komischeMatrix ist die Ausgabe 42 42 da das Array an Stelle 0 auf 42 gesetzt wird und die Erzeugung der Matrix nicht unveränderlich ist

#### Wir wollen einen Marsrover steuern. Der Rover hat eine KI eingebaut, die den Rover automatisch einen Schritt in einem Suchraster ausführen lässt. Das Interface des Rovers ist
```java
public interface Rover {
  void step();
  boolean wasserGefunden();
}
```
#### Schreiben Sie ein Methode wasserSuchen, die den Marsrover bewegt, bis er Wasser gefunden hat. Verwenden Sie die passende Schleife.
- ```java
    public void searchWater(){
        while(wasserGefunden() == false){
            step();
        }
    }
  ```

#### Wir wollen die Rennergebnisse eines Marathons ausgeben. Jede:r Teilnehmer:in ist ein Objekt vom Typ Ergebnis zugeordnet, das Name und die benötigte Zeit speichert. Es gibt einen Typ Zeit, der das Comparable-Interface erweitert.
```java
public class Ergebnis {
  // ...
  public String getName() { ... }
  public Zeit getZeit() { ... }
}

public class Zeit implements Comparable<Zeit> {
  // ...
  public int compareTo(Zeit other) { ... }
}

```
#### Schreiben Sie eine Methode print, die eine Liste von Ergebnissen bekommt und die Ergebnisse wie in folgendem Beispiel gezeigt auf der Konsole ausgibt:
```
1. Kipchoge, Eliud (02:02:37)
2. Geremew, Mosinet (02:02:55)
3. Wasihun, Mule (02:03:16)
4  Kitata, Tola Shura (02:05:01)
```
#### Verwenden Sie die für diesen Zweck idiomatische Schleife.
-

#### Stellen wir uns vor, wir bekommen die Ergebnisse in einer zufälligen Reihenfolge. Schreiben Sie eine Methode, um die Ergebnisse in die richtige Reihenfolge zu bringen.
-

#### Ist eine Liste eigentlich eine gute Datenstruktur für Marathon-Resultate oder gibt es etwas Besseres?
-


## Woche 2

### Aufgaben/Leitfragen Klassenpfade, Packages und Jars

#### Ändern Sie das Beispiel in classpath/example4 so ab, dass die Klasse Person im Package nested liegt. Kompilieren und starten Sie das Programm dann von der Kommandozeile aus.
-

#### Angenommen, wir haben eine Java-Datei auf unserem Rechner unter /home/uni/propra1/pfad/Foo.java liegen. Die Klasse verwendet das Default Package. Wie lautet der Klassenpfad, wenn wir die Datei auf der Kommandozeile kompilieren wollen? Dabei soll es egal sein, aus welchem Verzeichnis wir javac aufrufen.
-

#### Angenommen, wir haben eine Java-Datei auf unserem Rechner unter /home/uni/propra1/pfad/Foo.java liegen. Die erste Zeile der Datei ist package pfad;. Wie lautet der Klassenpfad?
-

#### Entfernen Sie in der Klasse StaticInit die Zeile private static final String HELLO = hello();. Was passiert dann und warum? Es wird doch gar keine statische Methode mehr aufgerufen, die die Initialisierung anstoßen kann? (Oder vielleicht doch‽)
-

#### Schreiben Sie ein Programm, das die Länge der Ankathete und Gegenkathete eines rechtwinkligen Dreiecks übergeben bekommt und die Länge der Hypotenuse und den Winkel zwischen Ankathete und Hypotenuse ausrechnet. Verwenden Sie statische Imports für Methoden aus der Math-Klasse.
-

#### Erstellen Sie zwei Klassen A und B. Legen Sie A in das Default Package und B in de.propra. Versuchen Sie in B eine Instanz von A zu erzeugen.
-

#### Schreiben Sie zwei Klassen Greeter und Start. In Greeter soll es eine greet Methode geben, die eine Grußbotschaft als String zurückgibt und in Start soll die main-Methode liegen, die greet aufruft und die Grußbotschaft ausgibt. Verpacken Sie die kompilierten Klassen als startbare .jar-Datei.
-

#### Geben Sie Ihrer Begrüßungsanwendung etwas Struktur.
##### Legen Sie beide Klassen in das Package de.propra.greet und verstecken Sie die Greeter-Klasse, indem Sie die Klasse package-private machen. Testen Sie die Sichtbarkeit, indem Sie eine dritte Klasse außerhalb des Packages schreiben und versuchen, Greeter zu verwenden.
##### Legen Sie die Start-Klasse in de.propra.greet und Greeter in de.propra.greet.impl. Können Sie Greeter immer noch package-private machen?
-

### Aufgaben/Leitfragen Anwendungen bauen mit Gradle

#### In einem Gradle-Projekt mit einer Standard-Konfiguration liegt eine Java-Datei unter dem Pfad src/main/java/main/App.java. Wie lautet die erste Zeile der Java-Datei, die vom Java-Compiler beachtet wird?
-

#### In den Dateien zu dieser Woche finden Sie im Ordner gradle_uebung ein Beispielprojekt für diese Aufgabe.
##### Führen Sie das Programm aus. Das Programm gibt eine Zeile aus, die mit Works: beginnt.
##### Generieren Sie eine gezippte Version (Distribution) des Programms, entpacken Sie die Zip-Datei und starten Sie das Programm. (Sie finden des Ergebnis im build-Ordner.)
##### Werfen Sie einen Blick in den lib-Ordner der Distribution (also in der zip-Datei). Hätten Sie mit so vielen Dateien gerechnet?
##### Finden Sie heraus, warum ./gradlew tasks und ./gradlew ta das Gleiche machen. Was macht ./gradlew t? (Suchen Sie die Dokumentation von Gradle.)
-
##### Finden Sie das kürzestmögliche Kommando der Form ./gradlew <XXX> um eine gezippte Version der Anwendung zu generieren. (Tipp: Sie benötigen zwei Buchstaben.)
-
##### Was ist der Unterschied zwischen den Tasks assemble und build?
-

#### Schreiben Sie ein Programm, das Namen und Telefonnummern verwalten kann. Wir gehen der Einfachheit halber davon aus, dass Namen und Nummern jeweils eindeutig sind. Verwenden Sie gradle, um das Programm zu bauen.
##### Das Programm soll die Datenstruktur BiMap aus der Bibliothek Google Guava verwenden.
##### Als Schlüssel und Wert der BiMap verwenden Sie jeweils Strings.
##### Die Map können Sie vorab mit Werten befüllen (z. B. im Konstruktor).
##### Das Programm soll dann mit zwei Parametern aufgerufen werden: Der erste Parameter ist entweder name oder nummer und gibt an, ob nach einem Namen oder einer Telefonnummer gesucht wird. Der zweite Parameter ist der Name bzw. die Telefonnummer, nach dem bzw. der gesucht wird. Das Programm soll folgendermaßen aufgerufen werden: 
```
./gradlew run --args="name Name"
+49 211 81-10714

./gradlew run --args="nummer '+49 211 81-10714'"
Name

./gradlew run --args="nummer 123"
Nicht vorhanden
```

#### Wichtig bei der Software-Entwicklung ist zu wissen, welche Arbeit wir uns nicht selber machen müssen! In dieser Aufgabe sollen Sie daher etwas recherchieren.
##### Wir wollen Excel-Tabellen in einem Programm einlesen. Finden Sie eine Bibliothek, mit der das geht.
-
##### Als Alternative wollen wir .csv-Dateien (Comma Separated Values) einlesen. Welche Bibliothek könnte da weiterhelfen?
-
##### Die Kommandozeilenprogramme, die wir kennengelernt haben, benutzen im Normalfall Parameter, die auf der Kommandozeile übergeben werden. Zum Beispiel können wir unter Unix ein Verzeichnis als Liste mit allen versteckten Dateien mit ls -a -l anzeigen lassen. Es funktionieren aber auch ls -l -a, ls -la oder ls -al. Ein Blick auf die Handbuchseite von ls zeigt, dass es noch viel mehr Schalter und folglich sehr viele gültige Kombinationen der Schalter gibt. So etwas selber zu schreiben, indem wir selbst die Programmparameter untersuchen, ist keine echte Freude. Aber zum Glück gibt es Bibliotheken. Finden Sie eine!
-

###  Aufgaben/Leitfragen Generics

#### In einer Hosentasche kann genau ein Ding gespeichert werden oder die Hosentasche kann leer sein. Eine Hose hat zwei Taschen und es ist natürlich vollkommen klar, dass man nicht beliebige Dinge in die Taschen steckt – unsere Hosen sind selbstverständlich typsicher! Schreiben Sie also eine parametrisierte Klasse Tasche, in der ein Datentyp gespeichert wird, und eine Klasse Hose, die zwei Taschen hat. Ihre Implementierung soll folgendermaßen benutzt werden:
```java
 public static void main(String[] args) {
    Hose<Taschentuch, Portemonnaie> hose = new Hose<>();
    hose.inDieLinkeTaschePacken(new Taschentuch());
    System.out.println(hose); // links: Taschentuch, rechts: leer

    // kompiliert nicht
    // hose.inDieRechteTaschePacken(new Taschentuch());
}
```

#### Wir haben folgende Java-Klasse, die einen Wert vom Typ T speichert.
```java
public class ConvertibleBox<T> {
  private final T content;

  public ConvertibleBox(T content) {
    this.content = content;
  }

  public static void main(String[] args) {
    ConvertibleBox<Integer> box = new ConvertibleBox<>(42);

    String asString = box.convert(e -> "Wert: " + e);
    System.out.println(asString);

    Double asDouble = box.convert(e -> Math.PI * e);
    System.out.println(asDouble);
  }
}
```
Es fehlt der Klasse eine convert-Methode, die den Inhalt der Box mithilfe einer Function<T,R> in verschiedene Datentypen konvertieren kann.
##### Schreiben Sie die Methode. Tipp: Die Methode muss generisch sein.
-

##### Warum können wir das nicht mit einem zweiten Typparameter für die Klasse erledigen?
-

    
## Woche 3

### Aufgaben/Leitfragen Methoden-Referenzen

#### Warum verwenden wir in dem Primzahlbeispiel einen Comparator und implementieren nicht einfach das Comparable-Interface
-
 
#### Geben Sie ein Beispiel für einen Lambda-Ausdruck an, der nur eine Methode aufruft, aber nicht direkt in eine Methodenreferenz umgeschrieben werden kann.
-

### Aufgaben/Leitfragen Funktionen Höherer Ordnung

#### Gegeben seien die Funktion Function<Integer, Collection<Double>> wurzeln = n → List.of(-Math.sqrt(n), Math.sqrt(n)) und die Liste List.of(1,2,3). Was ist das Ergebnis, wenn sie wurzeln über die Liste mappen? Was erhalten Sie, wenn Sie stattdessen flatMap verwenden?
-
    
#### Was berechnet der folgende Ausdruck?
```java
    reduce(
    new ArrayList<Integer>(),
    (acc, e) -> {
        ArrayList<Integer> newAcc = new ArrayList<>(acc); // erstellt neue ArrayList als Kopie von acc
        newAcc.add(e+1);
        return newAcc;
    },
    List.of(1,2,3)
    )
```
-
    
#### Schreiben Sie den Ausdruck aus der vorherigen Aufgabe so um, dass map statt reduce benutzt wird. Testen Sie Ihre Lösung, z. B. in der JShell.
-
    
#### Implementieren Sie die filter-Funktion selber. Sie können die Funktion wahlweise direkt implementieren oder als Spezialfall von reduce.
-

#### Welchen großen Nachteil hat unsere Implementierung von map mithilfe von reduce gegenüber unserer direkten Implementierung?
-

### Aufgaben/Leitfragen Streams
  
#### Angenommen, es gäbe keine generate-Methode. Schreiben Sie eine statische Methode myGeneration, die einen Supplier bekommt und einen Stream zurückgibt, in dem die Werte sind, die generate erzeugen würde. Verwenden Sie iterate zur Implementierung.
-
    
#### Gegeben sei folgende Klasse Lebensmittel:
    ```java
    public class Lebensmittel {
    private final String name;
    private final boolean abgelaufen = (Math.random() > 0.8);

    public Lebensmittel(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public boolean isAbgelaufen() {
        return abgelaufen;
    }

    @Override
    public String toString() {
        return "Lebensmittel[name=" + name + ", abgelaufen=" + abgelaufen + ']';
    }
    }
    ```
    Schreiben Sie eine Methode inventur, die eine Liste von Lebensmitteln bekommt und eine Liste von Lebensmitteln, die nicht abgelaufen sind, zurückgibt.      Verwenden Sie dazu die Stream-API und verwenden Sie ausschließlich Methodenreferenzen, keine Lambda-Ausdrücke.
-
    
#### Um den Umgang mit den Stream-Funktionen weiter zu üben, können Sie auch zusätzlich noch folgende Informationen über den Lebensmittelbestand berechnen und ausgeben:
##### Geben Sie aus, ob es abgelaufene Lebensmittel gibt.
-
##### Wie viele abgelaufene Lebensmittel gibt es?
-
##### Geben Sie eine alphabetisch sortierte Liste der ersten fünf abgelaufenen Lebensmittel aus.
-

### Aufgaben/Leitfragen Reduktionen
    
#### Schreiben Sie eine Methode int evenSum(int n), die die geraden Zahlen zwischen 1 und n aufsummiert. Benutzen Sie dazu einen Stream.
-
   
#### Berechnen die folgenden vier Ausdrücke dasselbe? Erstellen Sie ein Ranking danach, welchen der Ausdrücke Sie in der Praxis bevorzugen würden.
    ```java
    Stream.of(1,2,3).reduce(
    new ArrayList<Integer>(),
    (acc, e) -> {
        ArrayList<Integer> newAcc = new ArrayList<>(acc);
        newAcc.add(e + 1);
        return newAcc;
    },
    (acc1, acc2) -> { // hängt zwei Listen aneinander (relevant für parallele Streams)
        ArrayList<Integer> newAcc = new ArrayList<>(acc1);
        newAcc.addAll(acc2);
        return newAcc;
    })
    ```
    ```java
    Stream.of(1,2,3).collect(
    () -> new ArrayList<Integer>(),
    (acc, e) -> acc.add(e + 1),
    (acc1, acc2) -> acc1.addAll(acc2))
    ```
    ```java
    Stream.of(1,2,3).collect(
    ArrayList::new,
    (acc, e) -> acc.add(e + 1),
    ArrayList::addAll)
    ```
    ```java
    Stream.of(1,2,3).map(e -> e + 1).toList()
    ```
-
    
#### Wir wollen ein Programm schreiben, welches die Häufigkeit von Wörtern in einer Textdatei zählt. Das Gerüst ist schon fertig, es fehlt „nur“ noch das Zählen der Wörter. Wir wollen Groß-/Kleinschreibung nicht unterscheiden, Bar und baR sollen das gleiche Wort in der Zählung sein.
```java
public class WortHaufigkeit {
    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Requires exactly one filename");
            System.exit(-1);
        }
        Path file = Path.of(args[0]);

        Map<String, Long> frequency = new HashMap<>();

        try (Stream<String> words = new Scanner(file).tokens()) {

            // Im Stream »words« stehen jetzt alle Wörter der Datei. (Den Code drumherum müssen Sie jetzt noch nicht vollständig verstehen.)

            /* frequency =  mit Hilfe von Streams implementieren */

        } catch (IOException e) {
            e.printStackTrace();
        }
        System.out.println(frequency);
    }
}
```
-
    
#### Die beiden folgenden Codeschnipsel berechnen dasselbe Ergebnis. Welchen finden Sie idiomatischer? Ist es sinnvoll, wenn Stream-Operationen den Zustand von Objekten „außerhalb“ verändern? Warum?
    
```java
List<Integer> zahlen = List.of(1, 5, 3, 2, 5, 6, 4);
List<Integer> geradeZahlen = new LinkedList<>();
zahlen.stream().filter(n -> n % 2 == 0).forEach(geradeZahlen::add);
```
    
```java
List<Integer> zahlen = List.of(1, 5, 3, 2, 5, 6, 4);
List<Integer> geradeZahlen = zahlen.stream().filter(n -> n % 2 == 0).toList();    
```
-

## Woche 4

### Aufgaben/Leitfragen Einführung ins Testing
  
#### Schreiben Sie die Assertions in der Klasse assertj.AssertionsAufgaben im junit-Projekt in den vorgegebenen Dateien (d. h. ersetzen Sie die assertThat(true).isFalse(); durch sinnvollen Code). Machen Sie sich damit vertraut, wie Sie die Tests mit Gradle auf der Konsole und in Ihrer IDE ausführen können.
-
  
#### Überlegen Sie sich für jede FIRST-Regel: Warum ist diese Regel sinnvoll und notwendig?
-

#### Angenommen, Sie haben, um den Umgang mit Referenzen zu üben, eine einfach verkette Liste selbst implementiert. Es gibt eine Methode void remove(T needle) zum Löschen des ersten Elements, das gleich needle ist. Welche (Rand-)Fälle sollten Ihre Tests abdecken?
-
  
#### Schauen Sie sich an, welchen Typ die folgenden Methoden zurückgeben und welche Methoden AssertJ auf den zurückgegebenen Objekten anbietet. Sie können dazu die IDE verwenden und sich die Vorschläge anschauen.
```java
?? number = assertThat(4);
?? string = assertThat("foo");
?? bool = assertThat(false);
?? ldt = assertThat(LocalDate.now());
?? collection = assertThat(List.of(1,2,3));
```
-
  
#### Wir wollen die Methode lottoZahlenZiehen testen.
```java
public static List<Integer> lottoZahlenZiehen() {
  ArrayList<Integer> auswahl =
      IntStream.rangeClosed(1, 49)
          .boxed()
          .collect(Collectors.toCollection(ArrayList::new));
  Collections.shuffle(auswahl);
  return auswahl.stream()
      .limit(6)
      .sorted()
      .collect(Collectors.toList());
}
```
Schreiben Sie AssertJ-Assertions, die folgendes prüfen:

1. Die Anzahl der Zahlen stimmt

2. Jede Zahl kommt nur einmal vor

3. Alle Zahlen liegen zwischen 1 und 49

Schreiben Sie ausschließlich Assertions, keine Schleifen, etc. Den Code und einen vorbereiteten Test finden Sie im Ordner junit (Unterordner lotto); importieren Sie das Gradle-Projekt in Ihre IDE und nutzen Sie die Suchfunktion der IDE, um die für die Aufgaben relevanten Codestellen schnell zu finden.
-
  
#### Schauen wir uns einmal folgende Methode an, die eine Zufallszahl zwischen 1 und n zurückgibt.
```java
public int w(int n) {
  return (int)(Math.random() * n + 1);
}
```
Bei mehreren Aufrufen mit demselben Parameter gibt die Funktion unterschiedliche Werte zurück, sie kann also, nach unserer Behauptung, nicht pure sein. Aber wo ist der Seiteneffekt?
-
  
#### Lassen Sie die Tests im junit-Ordner mit ./gradlew check von der Kommandozeile aus laufen und schauen Sie sich den generierten Report an (build/reports/tests/test/index.html). Schalten Sie einen Test aus, ändern Sie den DisplayName, bringen Sie einige Tests dazu fehlzuschlagen, und schauen Sie sich an, wie sich die einzelnen Änderungen auf den Report auswirken.
-
  
#### Ändern Sie das Attribut counter in der CounterTest-Klasse so, dass es statisch ist, und lassen Sie die Tests laufen. Welcher Test schlägt fehl und warum gerade dieser?
-
  
#### Bringen Sie den Test in DivisionTest durch Veränderung von Division (also nicht durch Veränderung des Tests!) zum Fehlschlag.
-
  
### Leitfragen/Aufgaben Testgetriebene Entwicklung, Part 1
  
#### Beschreiben Sie in drei Sätzen die drei Schritte bei TDD.
-
  
#### In der Programmierung haben Sie schon ein paar Regeln für „guten“ Code kennengelernt. Welche fallen Ihnen noch ein?
-
  
#### Implementieren Sie testgetrieben eine Funktion, die bestimmt, ob ein gegebenes Jahr ein Schaltjahr ist. Achten Sie darauf, den Code im Refactoring so umzustrukturieren, dass er möglichst gut lesbar ist.
-

## Woche 5

### Aufgaben/Leitfragen Konventionen/Bennenung

#### Angenommen, Sie wollen eine Todo-Listen-Anwendungen schreiben. An einer Stelle soll es ein privates Attribut vom Typ List<Task> geben, in dem alle Aufgaben der Todo-Liste gespeichert sind. Schlagen Sie drei unpassende Namen für dieses Attribut vor (verletzen Sie also ausnahmsweise mal vorsätzlich die oben genannten Regeln). Versuchen Sie Namen zu finden, die aus unterschiedlichen Gründen unpassend sind.
-
    
#### Bei öffentlichen Schnittstellen können in Java manche Namen bedenkenlos geändert werden (also ohne, dass Änderungen am aufrufenden Code notwendig sind). Denken Sie z. B. konkret an folgendes Interface:
```java
 public interface Stack {
    void push(int a);
    int pop();
}   
```
Welche Namen können Sie im Interface ändern, ohne dass Sie Klassen, die das Interface implementieren, ändern müssen?
- pop
- push
- a
- stack

- ohne die Klassen die das Interface implementieren zu ändern kann man hier nur den Variablennamen `a` ändern.
    
### Leitfragen/Aufgaben DRY/Code Smells
    
#### Warum ist die Einhaltung des DRY-Prinzips wichtig für die Wartbarkeit von Software? Zu welchen Problemen kann eine Verletzung des Prinzips bei der Weiterentwicklung der Software führen?
    
#### Warum ist der identische Code der Funktionen validate_age und validate_quantity keine Verletzung des DRY-Prinzips?
    
#### „Wir sollten Code Smells aus unserem Code entfernen, weil sie auf ein Problem im Code hindeuten.“ Stimmen Sie der Aussage zu? Wann ist es wichtig, Code Smells zu entfernen?

### Aufgaben zu SLAP
- Im Code-Repo zu diesem Wochenblatt finden Sie im Ordner cosinus ein Gradle-Projekt. Der Code stammt aus einem Lösungsvorschlag zu einem Übungsblatt der Vorlesung Programmierung.

- Schauen Sie sich den Code mit Ihrem heutigen Wissen an. Welche Code Smells finden Sie?

- Refactorn Sie den Code. Lassen Sie nach jeder Änderung die vorhandenen Tests laufen.

- Finden Sie heraus, welche Tastenkombination es in Ihrer IDE für das Refactoring „Extract Method“ gibt, und üben Sie, dieses automatische Refactoring anzuwenden.
    
- Prüfen Sie am Ende, ob noch alle Namen sinnvoll sind und benennen Sie ggf. Variablen und Methoden mithilfe der IDE um.

    
## Woche 6

### Aufgaben/Leitfragen Debugging in der IDE

#### Im Ordner debugger im Code-Repo zu dieser Woche finden Sie das Projekt aus dem Video. Finden Sie den letzten Fehler mithilfe des Debuggers und beheben Sie das Problem.
-
    
#### Fügen Sie in der main-Methode von WordAnalyzerTester den Aufruf test(null); hinzu und lassen Sie das Programm laufen. Setzen Sie dann einen Exception-Breakpoint und starten Sie das Programm im Debugger-Modus.
-
    
### Aufgaben/Leitfragen Systematische Fehlersuche

#### Die Methode binarySearch aus der Klasse Collections sucht einen Wert in einer Kollektion. Sie gibt den Index des Wertes in der Kollektion zurück. Ein negativer Wert zeigt an, dass der Wert nicht vorhanden ist. Was ist der Fehler in folgendem Code? Reparieren Sie den Fehler.
```java
List<Integer> results = List.of(13,7,2,19,27,22,55,33,8);
 System.out.println(Collections.binarySearch(results,27)); // => 4 (stimmt)
 System.out.println(Collections.binarySearch(results,55)); // => 6 (stimmt)
 System.out.println(Collections.binarySearch(results,7)); // => 1 (stimmt)
 System.out.println(Collections.binarySearch(results,22)); // => -5 (falsch)
 System.out.println(Collections.binarySearch(results,2)); // => -1 (falsch)
 System.out.println(Collections.binarySearch(results,13)); // => -4 (falsch)
```
#### Im Ordner debugreduce finden Sie ein Programm, das eine Liste von Personendaten einliest und eine Häufigkeitsverteilung über die Toplevel-Domänen (TLD) der Mailadressen erstellt (also .de, .com usw.). Das Programm ist leider fehlerhaft und wir wollen nun das Problem beheben.
-
    
##### Reproduzieren Sie den Fehler, indem Sie das Programm laufen lassen. Sie stellen fest, dass es abstürzt und eine ArrayIndexOutOfBoundsExcption produziert.
-
    
##### Schreiben Sie einen automatisierten Test, der den Fehler reproduziert. Kopieren Sie dazu die Datei entries.csv und benennen Sie diese zum Beispiel in testentries.csv um. Verwenden Sie die Kopie für den Test. Wie sollte die Assertion lauten?
-

##### Minimieren Sie die Eingabedatei für den Test, so dass der Absturz immer noch auftitt. Verwenden Sie dazu eine „binäre Suche“. Entfernen Sie die Hälfte der Eingabedaten. Stürzt das Programm ab? Wenn nein, dann war wahrscheinlich in den gelöschten Daten die Fehlerursache. Wenn ja, dann gibt es eine Fehlerursache in den noch vorhandenen Daten. Fahren Sie solange fort, bis die Datei eine minimale Größe hat.
-
##### Warum nicht mit dem Debugger arbeiten?
-
    
##### Warum ist es wichtig, eine minimale Eingabe zu erzeugen?
-
    
##### Finden Sie den Defekt im Programm, wir wollen nicht die Schuld am Absturz an die Person weiterreichen, die die Eingabedatei produziert hat, sondern unser Programm robuster gestalten. Sie können die Ursache hier ziemlich sicher mithilfe der Fehlermeldung finden, Sie können aber auch mit dem Debugger arbeiten.
-
    
##### Nachdem Sie die Ursache gefunden haben, beheben Sie das Problem und überprüfen Sie mithilfe des Tests, dass das Problem behoben wurde. Es gibt verschiedene Arten, das Problem sinnvoll zu beheben, treffen Sie eine Entscheidung.
-
    
##### Worauf sollten wir achten, damit ein solches Problem in Zukunft vermieden werden kann?
-
    
##### Es gibt noch einen zweiten Fehler. Beheben Sie auch diesen Fehler.
-
   
    
### Aufgaben/Leitfragen Minor Changes: Sinnvolle Commits
    
#### Schauen Sie sich diese Klasse auf GitHub an. Wer hat die Zeile catch (NullPointerException e) geschrieben und warum? Hilft Ihnen die Commit-Nachricht weiter? (Sie müssen die Begründung für die Codezeile nicht nachvollziehen können, Sie sollen aber einmal den Umgang mit der Git-History (auf der Konsole oder auf GitHub) üben und sehen, dass verständliche Commit-Nachrichten hilfreich sind.)

#### Nehmen Sie sich irgendein Repository von Ihnen und verändern Sie irgendentwas an einer bereits versionierten Datei.

1. Lassen Sie sich anzeigen, welche Änderungen es seit dem letzten Commit gab. (git diff)

2. Committen Sie die Änderungen. Vergeben Sie dabei eine Commit-Nachricht, die aus mehr als einer einzelnen Zeile besteht. (git commit)
    
#### Fassen Sie zusammen: Warum sind Commits mit zusammenhängenden Code-Änderungen und einer guten Commit-Nachricht sinnvoll?
-
    
#### Sofern Sie die erste Übung nicht besucht haben: Arbeiten Sie die Aufgaben zur Gitignore durch.

#### Lassen Sie sich eine gitignore-Datei für Ihr Betriebssystem generieren. Richten Sie diese Datei als globale gitignore ein. Testen Sie mit einem Repository von Ihnen, dass die globale gitignore-Datei funktioniert.
    
