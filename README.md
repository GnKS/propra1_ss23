# ProPra I Zusammenfassung

# Woche 1

## Die Java Klassenbibliothek

### Collection
Folgendes Bild ist ein UML-Klassendiagramm (Interfaces I, Klassen C).
Ein gestrichelter Pfeil ist eine Implementierungsbeziehung (bsp. LinkedList implements Interface List und Deque).
Ein durchgezogener Pfeil ist eine Erweiterungsbeziehung (bsp. SortedSet extends Interface Set).
Eine Erweiterungsbeziehung kann auch zwischen Klassen bestehen, ist auf diesem Diagramm allerdings nicht vorhanden.

![Classrelations](images/classrelations.png)

Das Basis-Interface ist Collection. Dort sind Methoden definiert, die für alle sequenzartigen Kollektionen sinnvoll sind:
- `add` und `addAll`, um Elemente in die Kollektion einzufügen
- `remove`, `removeAll`, `removeIf`, `retainAll` und `clear`, um Elemente zu löschen
- `contains` und `containsAll`, um herauszufinden, ob Elemente in der Kollektion vorhanden sind
- `size` und `isEmpty`, um die Anzahl der Elemente abzufragen, bzw. herauszufinden, ob eine Kollektion leer ist.
- `toArray` und `stream` um die Kollektion in ein Array bzw. einen Stream zu konvertieren

Konkrete Klassen implementieren üblicherweise eines der drei spezifischeren Interfaces `List`, `Set` und `Queue`.

### List
Das List-Interface ist für Kollektionen gedacht, bei denen Elemente geordnet positioniert sind.
Elemente sind nicht sortiert, sondern haben haben eine bestimmte Position in der Kollektion und können mehrfach vorkommen.

Wesentliche Methoden die `List` zusätzlich zu `Collection` spezifiziert, sind
- `get`, um ein Element, das an einer bestimmten Position in der Liste gespeichert ist, zu lesen
- `set`, um ein Element, das an einer bestimmten Position in der Liste gespeichert ist, zu überschreiben

`List` stellt außerdem eine zusätzliche Variante von `add` bereit:
```java
List<Integer> ints = init(); //Liste mit Werten erzeugen
ints.add(1, 6); //fügt an Position 1 den Wert 6 ein
```
Mit `of` lässt sich eine Liste direkt erzeugen die sich im Nachhinein nicht mehr ändern lässt.
Eine solche Methode, die kein Konstruktor ist, nennt man statische Factorymethode.

```java
List<Integer> numbers = List.of(2,3,4,5,6,7,8,9,16);
System.out.println(numbers); // => [2,3,4,5,6,7,8,9,16]
numbers.add(23); // => Exception java.lang.UnsupportedOperationException
```

#### ArrayList
`ArrayList` verwendet intern ein Array zur Datenspeicherung somit ist Zugriff per Index sehr effizient.
Einfügen von Elementen an einer beliebeigen Stelle ist hingegen teuer, da alle Elemente an Folgepositionen verschoben werden müssen.
Wenn das Array voll ist weid ein neues mit min. 50% größerer Kapazität erzeugt und das alte Array umkopiert.

`ArrayList` Beispiel:
```java
List<String> names = new ArrayList<>();
// Beobachtung 1: Der Typ der Variablen kann eine Superklasse vom erzeugten Typ sein oder ein Interface, das die Klasse implementiert (das kennen Sie schon von den Flying Objects aus der Programmierung).
// Beobachtung 2: Die Collection-Klassen sind parametrisiert, hier mit String.
// Beobachtung 3: Sie müssen den Typ-Parameter bei der Instanziierung auf der rechten Seite in den spitzen Klammern seit Java 7 nicht wiederholen.

System.out.println(names); // => []

// Ein erstes Element wird eingefügt, Rückgabe ist true, wenn es erfolgreich war
System.out.println(names.add("Java Mc Javaface")); // => true

names.add("James Gossling"); // => true

// ArrayList zählt intern mit, der Aufruf ist billig (schnell)!
System.out.println(names.size()); // => 2

System.out.println(names); // => [Java Mc Javaface, James Gossling]

// Einfügen in der Mitte. Das kann teuer (langsam) werden, wenn eine ArrayList viele Elemente beinhaltet!
names.add(1, "Brian Goetz");

System.out.println(names); // => [Java Mc Javaface, Brian Goetz, James Gossling]

// Beim Überschreiben bekommen wir den überschriebenen Wert zurück
System.out.println(names.set(0, "Joshua Bloch")); // => "Java Mc Javaface"

System.out.println(names); // => [Joshua Bloch, Brian Goetz, James Gossling]

ArrayList<String> javaleute = new ArrayList<>();

// Alle Elemente einer Liste in eine andere einfügen
System.out.println(javaleute.addAll(names)); // => true

// Alle Elemente entfernen
names.clear();

System.out.println(names); // => []
System.out.println(javaleute); // => [Joshua Bloch, Brian Goetz, James Gossling]
```

#### LinkedList
`LinkedList` ist eine doppelt verkettete Liste (jeder Knoten hat eine Referenz auf Vorgänger und Nachfolger)

![LinkedList](images/linkedlist.png)

Vorteile einer doppelten Verkettung:
- Man kann schnell von vorne nach hinten und von hinten nach vorne durch Listenelemente iterieren
- Man kann hinten und vorne effizient (in konstanter Zeit) Elemente einfügen und entfernen

`LinkedList` eignet sich aufgrund ihrer Eigenschaften gut als Implementierung für das Queue- und Deque-Interface. Ist aber nicht gut geeignet als Liste (man verwendet dafür `ArrayList`).
`LinkedList` wird häufig als Implementierung für einen Stack oder Queue verwendet.

### Queue
Das `Queue`-Interface spezifiziert Methoden, die man bei einer Queue-Implementierung erwartet:
- `offer` zum einfügen in Queue
- `peek` zum anschauen des nächsten Elements ohne es zu entfernen
- `poll` zum entfernen des nächsten Elements

`LinkedList` ist eine Implementierung einer FIFO-Queue (Elemente hinten einfügen und vorne entfernen).

Beispiel:
```java
Queue<String> q = new LinkedList<>();

q.offer("a");
q.offer("b");
q.offer("c");

System.out.println(q); // => [a, b, c]
System.out.println(q.peek()); // => a
System.out.println(q); // => [a, b, c]
System.out.println(q.poll()); // => a
System.out.println(q); // => [b, c]
```
Die Implementierung für `Deque` mit `LinkedList` ist ähnlich:
- `offerFirst`, `offerLast` zum einfügen vorne oder hinten in Queue (analog für die anderen Methoden)
- `push` um Element auf den Stack zu legen
- `pop` um Element vom Stack zu holen

Stacks haben ein LIFO-Verhalten.

Beispiel:
```java
Deque<String> stack = new LinkedList<>();

stack.push("x");
stack.push("y");
stack.push("z");

System.out.println(stack); // => [z, y, x]
System.out.println(stack.peek()); // => z
System.out.println(stack); // => [z, y, x]
System.out.println(stack.pop()); // => z
System.out.println(stack); // => [y, x]
```

### Set
In einem `Set` gibt es keine doppelten Elemente ähnlich wie bei einer Menge in der Mathematik.
Eine häufige Implementierung ist das `HashSet`:
```java
Set<Integer> ints = new HashSet<>();
ints.addAll(List.of(3,4,5,6,7,8,9,16));
System.out.println(ints); // =>  [16, 3, 4, 5, 6, 7, 8, 9]
```
Eine Klasse die nur `Set` aber nicht `SortedSet` implementiert gibt es keine Garantie in welcher Reihenfolge Elemente durchlaufen werden, daher sollten keine Annahmen über die Reihenfolge gemacht werden.

Wenn eine bestimmte Reihenfolge nötig ist verwendet man Klassen die `SortedSet` implementieren.
Entweder kann man eine Instanz des `Comparator`-Interfaces benutzen oder die natürliche Reihenfolge (definiert für alle Datentypen die das `Comparable`-Interface implementieren wie z.B. `Integer` oder `String`).
Eine Klasse die `SortedSet` implementiert, ist `TreeSet`:

```java
Set<Integer> ints = new TreeSet<>();
ints.addAll(List.of(7,6,4,9,3,8,16,5));
System.out.println(ints); // =>  [3, 4, 5, 6, 7, 8, 9, 16]
```
Natürliche Reihenfolge mit Comparator:

```java
// erstellt ad hoc ein Objekt einer "anonymen" (namenlosen) Klasse, die das Comparator-Interface implementiert
Comparator<Integer> evenFirstComparator = new Comparator<Integer>() {
  @Override
  public int compare(Integer o1, Integer o2) {
    if (o1 % 2 == o2 % 2) {
      // compareTo gibt einen negativen Wert zurück, falls o1 < o2
      return o1.compareTo(o2);
    }
    if (o1 % 2 == 0) {
      return -1;
    } else {
      return 1;
    }
  };
};

SortedSet<Integer> set = new TreeSet<>(evenFirstComparator);
set.addAll(List.of(3,4,5,6,7,8,9,16));
System.out.println(set); // => [4, 6, 8, 16, 3, 5, 7, 9]
set.add(10);
System.out.println(set); // => [4, 6, 8, 10, 16, 3, 5, 7, 9]
set.add(13);
System.out.println(set); // => [4, 6, 8, 10, 16, 3, 5, 7, 9, 13]
```
`Comparator` ist ein funktionales Interface welches die Funktion `compare` implementiert, die zwei Instanzen `a` und `b` des zuvergleichenden Objekts übergeben bekommt. Die Methode gibt einen negativen Wert zurück, wenn `a` bezüglich der Sortierung kleiner ist als `b`, einen positiven im umgekehrten Fall und 0 wenn beide gleich sind.

### Map
Klassen die das `Map`-Interface unterstützen, erben nicht von `Collection`, werden aber auch zur Speicherung von Daten verwendet.
Es werden Schlüssel-Wert-Paare gespeichert.

Es gibt sortierte und unsortierte Maps wobei die Sortierung sich auf die Schlüssel bezieht.

![MapGraph](images/mapgraph.png)

`Map` enthält ähnliche Methoden wie `Collection`:
- `get` und `getOrDefault`, um Werte nachzuschlagen
- `put`, `putAll` und `putIfAbsent`, um Schlüssel-Wert-Paare in die Map einzufügen
- `remove` und `clear`, um Paare zu löschen
- `keySet`, `values` und `entrySet` um eine Kollektion der Schlüssel, Werte bzw. Schlüssel-Wert-Paare zu bekommen
- `of` um unveränderliche Maps zu erzeugen

`HashMap` garantiert keine bestimmte Reihenfolge.
`LinkedHashMap` kann verwendet werden wenn die Einfügereihenfolge beibehalten wird.
`SortedMap` ist ein Interface in dem die Schlüssel in sortierter Reihenfolge vorliegen.

Beispiel:
```java
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.TreeMap;

class Customer {

  private final String name;

  private Customer(String name) {
    this.name = name;
  }

  public String toString() {
    return name;
  }

  public static Customer customer(String name) {
    return new Customer(name);
  }

  public static void main(String[] args) {
    Map<Integer, Customer> customers = new HashMap<>();

    customers.put(1, customer("Bill Gates"));
    customers.put(3, customer("Jeff Bezos"));
    customers.put(2, customer("Elon Musk"));

    System.out.println(customers); // => {1=Bill Gates, 2=Elon Musk, 3=Jeff Bezos}

    System.out.println(customers.get(2)); // => Elon Musk
    System.out.println(customers.get(4)); // => null

    System.out.println(customers.getOrDefault(2, customer("Arno Nym"))); // => Elon Musk
    System.out.println(customers.getOrDefault(4, customer("Arno Nym"))); // => Arno Nym

    customers.putIfAbsent(3, customer("Karl Albrecht"));
    System.out.println(customers.values()); // => [Bill Gates, Elon Musk, Jeff Bezos]

    customers.put(3, customer("Karl Albrecht")); // => [Bill Gates, Elon Musk, Karl Albrecht]
    System.out.println(customers.values());

    customers.remove(2);
    System.out.println(customers); // => {1=Bill Gates, 3=Karl Albrecht}

    customers.put(16, customer("Warren Buffett "));
    System.out.println(customers); // => {16=Warren Buffett , 1=Bill Gates, 3=Karl Albrecht}
  }
}
```

### Utility-Klassen
In den zwei Hilfsklassen `Collections` und `Arrays` finden sich eine Reihe nützlicher Hilfsmethoden:

```java
List<String> liste = new ArrayList<>(List.of("Kartoffeln", "Tomaten", "Wasser", "Brot"));
System.out.println(liste); // => [Kartoffeln, Tomaten, Wasser, Brot]

Collections.reverse(liste); // Achtung: Die Originalliste wird verändert!
System.out.println(liste); // => [Brot, Wasser, Tomaten, Kartoffeln]

Collections.sort(liste);
System.out.println(liste); // => [Brot, Kartoffeln, Tomaten, Wasser]

Collections.swap(liste, 0, 2);
System.out.println(liste); // => [Tomaten, Kartoffeln, Brot, Wasser]

Collections.shuffle(liste);
System.out.println(liste); // => Die Liste in zufälliger Reihenfolge

Collections.sort(liste);
Collections.rotate(liste, 1);
System.out.println(liste); // => [Wasser, Brot, Kartoffeln, Tomaten]

Collections.rotate(liste, -2);
System.out.println(liste); // => [Kartoffeln, Tomaten, Wasser, Brot]

Collections.fill(liste, "Bier");
System.out.println(liste); //=> [Bier, Bier, Bier, Bier]
```

Die Klasse `Arrays` enthält viele analoge Funktionen, die den Umgang mit Arrays erleichtern.

### Externe Bibliotheken
Wir wollen Übungsgruppen verwalten und benötigen eine Datenstruktur, um Studierende auf Termine aufzuteilen. Wir können dazu eine Map verwenden, deren Schlüssel die Termine sind und jedem Termin ein Set von Studierenden zuordnen. Vor Java 8 war der notwendige Code ziemlich unangenehm. Wir müssen das zu einem Termin gehörende Set aus dem Map holen. Wenn das Set noch nicht existiert, müssen wir ein neues Set anlegen und können dann z. B. das GitHub-Handle speichern.

```java
public class AwkwardMap {

  private final HashMap<String, Set<String>> zuordnung = new HashMap<>();

  public void add(String termin, String githubHandle) {
    Set<String> handles = zuordnung.get(termin);
    if (handles == null) {
      handles = new HashSet<>();
    }
    handles.add(githubHandle);
  }
}
```

Mit `getOrDefault` wird der Code kompakter

```java
public class AwkwardMap {

  private final HashMap<String, Set<String>> zuordnung = new HashMap<>();


  public void add(String termin, String githubHandle) {
    Set<String> handles = zuordnung.getOrDefault(termin, new HashSet<>());
    handles.add(githubHandle);
  }
}
```
(Funktionen werden in Leifragen gefixed)

Besser ist eine fertige Implementierung einer `MultiMap` zu benutzen (z.B. von Google Guava oder Apache Commons Collection)

```java
public class BetterMap {

  // Verwendet die Bibliothek Apache Commons Collection
  // Wie Sie so eine Bibliothek nutzen, schauen wir uns in der kommenden Woche an
  private final HashSetValuedHashMap<String, String> zuordnung = new HashSetValuedHashMap<>();

  public void add(String termin, String githubHandle) {
    zuordnung.put(termin, githubHandle);
  }
}
```
