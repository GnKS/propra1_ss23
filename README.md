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
