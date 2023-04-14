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
-

#### Schreiben Sie eine Methode, die eine Liste von Strings bekommt und diese auf der Konsole ausgibt. Verwenden Sie die richtige Art der Iteration.
-

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
-

#### Wir wollen einen Marsrover steuern. Der Rover hat eine KI eingebaut, die den Rover automatisch einen Schritt in einem Suchraster ausführen lässt. Das Interface des Rovers ist
```java
public interface Rover {
  void step();
  boolean wasserGefunden();
}
```
#### Schreiben Sie ein Methode wasserSuchen, die den Marsrover bewegt, bis er Wasser gefunden hat. Verwenden Sie die passende Schleife.
-

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
