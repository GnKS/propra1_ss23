# Lösungen zu allen Leitfragen

## Woche 1

### Aufgaben/Leitfragen 1

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

#### Im obigen Beispiel zu sortierten Mengen findet sich folgende Zeile ``Set<Integer> ints = new TreeSet<>();`` 
Muss es auf der linken Seite nicht SortedSet heißen? Warum (nicht)?
- Lösung text

#### Schauen Sie sich den Comparator aus dem Beispiel ganz genau an und gehen Sie alle möglichen Eingaben durch (zwei unterschiedliche gerade Zahlen, zwei unterschiedliche ungerade Zahlen, eine gerade und eine ungerade Zahl, eine ungerade und eine gerade Zahl, zweimal dieselbe Zahl) und schreiben Sie auf, welches Resultat Sie erhalten.
- Lösung text

#### Angenommen, wir wollen eine statische compareTo-Methode für int schreiben. Ein Vorschlag für die Implementierung ist: ``public static int compareTo(int a, int b) { return a - b; }`` Die Methode liefert einen negativen Wert für a < b, einen positiven Wert für a > b und bei Gleichheit den Wert 0. Warum wäre eine solche Implementierung nicht korrekt? Geben Sie ein Beispiel für a und b an, bei dem die Methode versagt.
-Lösung text

#### Wir benötigen ein Wörterbuch, bei dem die Wörter der Länge nach durchlaufen werden. Verwenden Sie ein TreeSet und eine passende Implementierung von Comparator. In das Set sollen Wörter gespeichert werden und bei einem Durchlauf sollen die längsten Wörter zuerst rauskommen. Bei gleicher Wortlänge ist die Reihenfolge egal.
- Lösung text

#### Welchen Fehler haben die beiden Implementierungen von AwkwardMap? Beheben Sie das Problem.
- Lösung text
