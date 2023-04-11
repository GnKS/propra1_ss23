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
