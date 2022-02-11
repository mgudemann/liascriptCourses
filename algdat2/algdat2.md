<!--
author: Prof. Matthias Güdemann

icon: https://upload.wikimedia.org/wikipedia/de/thumb/e/e8/Hochschule_Muenchen_Logo.svg/320px-Hochschule_Muenchen_Logo.svg.png

comment: Fragen aus QA zu Kryptographie

logo: https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Orange_blue_public_key_cryptography_de.svg/640px-Orange_blue_public_key_cryptography_de.svg.png

email:  matthias.guedemann@hm.edu

version: 1.0.0

-->

# Algorithmen und Datenstrukturen 2

## Zugriffszeiten

**Wie groß ist der Unterschied zwischen einem L1 Cache Zugriff und RAM Zugriff?**

[( )] 0.5ns vs 10ns
[(X)] 0.5ns vs 100ns
[( )] 0.5ns vs 1000ns
****

Der Faktor zwischen den Zugriffszeiten ist in etwa 200 und liegt bei 0.5ns zu 100ns. Das kann sich natürlich je nach CPU / RAM / Computergeneration ändern. Das relative Verhältnis wird sich aber in dieser Größenordnung bewegen.

<http://norvig.com/21-days.html#answers>

****

## Laufzeitkomplexität

### Geschachtelte Schleifen

```c
   for (int i = 0; i < n; i++)
      for (int j = i; j < n; j++)

        ... eine einfache Operation ...
```

Was ist hier die Laufzeitkomplexität?

[(X)] $O(n^2)$
[( )] $O(n)$
[( )** kann man nicht sagen weil $j$ ja bei $i$ beginnt
****

Es werden $n + (n - 1) + (n - 2) \cdots 1$ Durchläufe ausgeführt. Das liegt in $O(n^2)$.

****

### Komplexität

Was bedeutet $O(1)$?

[( )] geht nicht
[(X)] Aufwand bleibt gleich, egal was die Eingabe ist (**konstant**)
[( )] Ist beim ersten Mal ausführen linear, danach kommt das Ergebnis immer sofort
****

Der Aufwand bleibt immer gleich und ist nicht von der Eingabegröße abhängig, damit konstant.

****

### Komplexität

Was bedeutet $O(f(n) + g(n))$?

[( )] na ja, steht doch da, die Summer der beiden
[(X)] $O(\max(f(n), g(n)))$
[( )] kann man nicht sagen, kommt auf $f(n)$ und $g(n)$ an

### Komplexität

Angenommen, man hat einen Algorithmus der als Eingabe eine natürliche Zahl
hat. Mit der Eingabe $C$ hat der Algorithmus eine Laufzeit von
$O(C)$. Gilt dann

[(X)] Der Algorithmus hat exponentielle Laufzeit
[( )] Der Algorithmus hat polynomielle Laufzeit
[( )] Der Algorithmus hat konstante Laufzeit und es müsste eigentlich $O(1)$ heißen
****

Entscheidend ist die Darstellungsgröße der Eingabe. Die ist logarithmisch im Wert durch die Darstellung in einem Stellenwertsystem (z.B. zur Basis 2 oder 10).

****

### Komplexität

Sei $f(n) = \log_{10}(n)$ und $g(n) = \log_2(n)$ gilt dann auch
$f(n) \in O(g(n))$?

[(X)] ja
[( )] nein
****

Das gilt, da bei Logarithmen die Basis durch eine Multiplikation mit einer Konstanten getauscht werden kann.

****

## Graphen

## Arten von Graphen

Wie viele Kanten gibt es maximal in einem Graphen? ($n$ Knoten, $m$ Kanten)

[(X)] $m \in O(n^2)$
[( )] $m \in O(n)$
*****

In einem dichten Graphen kann jeder Knoten $n-1$ Nachbarn haben, damit $O(n^2)$.

*****

## Graphen

Gegeben sein ein Gitter / Grid / Stadtplan aus den USA

![Grid](http://mgu.cs.hm.edu/imgs/02/graphex3.png Grid Graph mit n-Spalten und m-Zeilen")


Wie groß wäre der Graph als Adjazenzmatrix?

[( )] 56 Einträge
[(X)] 784 Einträge
[( )] 28 Einträge
****

Es sind $28$ Knoten und damit $28\cdot28 = 784$ Einträge in einer Adjazenzmatrix.

****


### Graphen

**Wahr oder falsch** Ungerichtete Graphen können nicht zyklisch sein

[( )] wahr
[(X)] falsch
*****

Ungerichtete Graphen können ebenfalls Zyklen enthalten

*****

### Graphen

**Wahr oder falsch** In gewichteten Graphen bedeutet ein Kantengewicht von
0 dass die Kante nicht im Graphen liegt.

[( )] wahr
[(X)] falsch
******

Eine Kante kann durchaus das Gewicht 0 haben. Das muss nicht heißen, dass es keine Kante gibt.

******

### Graphen

**Wahr oder falsch** Man kann in $O(1)$ prüfen, ob für eine Kante $e \in E$ gilt.

[(X)] wahr
[( ] falsch
*******

Bei der Darstellung als Adjazenzmatrix kann man in konstanter Zeit prüfen, ob eine Kante im Graphen liegt.

*******

## Graph Traversal

### Graph Traversal

Angenommen ein zusammenhängender, ungerichteter Graph hat endlichen maximalen Grad (Anzahl ausgehende Kanten eines Knotens) aber unendlich viele Knoten. Welchen Algorithmus kann man dann ausführen?

[(X)] BFS
[( )] DFS
[( )] keinen von beiden
******

Die Breitensuche kann mit Graphen umgehen, die unendliche groß sind, so lange der maximale Grad der Knoten endlich ist. Das bedeutet ja, dass es jeweils nur endlich viele Nachbarn gibt, die besucht werden können.

******

### Datentyp

Für BFS benutzt man eine Queue, die wir als doppelt verkettete Liste implementiert haben. Was ist bei diesem Beispiel der Datentyp / was ist die Datenstruktur?

[( )] Datentyp: doppelt verkettete Liste / Datenstruktur: Queue
[(X)] Datenstruktur: doppelt verkettete Liste / Datentyp: Queue
[( )] Datentyp: doppelt verkettete Liste / Datentyp: Queue
[( )] Datenstruktur: doppelt verkettete Liste / Datenstruktur: Queue
*****

Ein Datentyp beschreibt abstrakt, welche Operationen unterstützt werden müssen. Eine konkrete Implementierung wird durch eine Datenstruktur realisiert.

*****

## MST

### MST

Ist der MST eines Graphen eindeutig?

[(X)] ja, wenn alle Gewichte unterschiedlich sind
[( )] nein, es gibt immer mehrere
[( )] ja, ist immer eindeutig, unabhängig vom Graphen und Algorithmus
*****

Der MST ist eindeutig, wenn alle Gewichte unterschiedlich sind. Im Allgemeinen kann es allerdings mehrere unterschiedliche MST geben.

*****

### MST

**Wahr oder Falsch** Ein Spannbaum eines zusammenhängenden Graphen hat ja $|V| - 1$ Kanten. Es kann nicht sein dass für das Gewicht eines MST $G=(V', E')$ gilt $\sum_{e\in E'} w(e) \leq |V'| - 1$.

[( )] wahr
[(X)] falsch
******

Das wäre nur erfüllt, wenn jede Kante mindestens Gewicht 1 hätte. Ansonsten muss das nicht gelten.

******


### Invariante

Algorithmus von Dijkstra
------------------------

 - **Invariante** für Dijkstra

   "Über die bisher abgearbeiteten Knoten ist $v$ mit höchstens $d(v)$
   erreichbar"

 - Was ist eine Invariante?

[( )] Ziel, was am Ende der Ausführung des Algorithmus gilt
[(X)] Muss immer und zu jedem Zeitpunkt des Ausführens erfüllt sein
[( )] Spezifikation eines Algorithmus
*****

Eine Invariante muss während der gesamten Zeit gelten, also eben invariant sein.

*****
