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

Wie groß ist der Unterschied zwischen einem L1 Cache Zugriff und RAM Zugriff?

[( )] 0.5ns vs 10ns
[(X)] 0.5ns vs 100ns
[( )] 0.5ns vs 1000ns
****

Der Faktor zwischen den Zugriffszeiten ist in etwa 200 und liegt bei 0.5ns zu 100ns. Das kann sich natürlich je nach CPU / RAM / Computergeneration ändern. Das relative Verhältnis wird sich aber in dieser Größenordnung bewegen.

http://norvig.com/21-days.html#answers

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
[( )] kann man nicht sagen weil $j$ ja bei $i$ beginnt
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

### Arten von Graphen

Wie viele Kanten gibt es maximal in einem Graphen? ($n$ Knoten, $m$ Kanten)

[(X)] $m \in O(n^2)$
[( )] $m \in O(n)$
*****

In einem dichten Graphen kann jeder Knoten $n-1$ Nachbarn haben, damit $O(n^2)$.

*****

### Graphen

Gegeben sein ein Gitter / Grid / Stadtplan aus den USA

![Grid](http://mgu.cs.hm.edu/imgs/02/graphex3.png "Grid Graph mit n-Spalten und m-Zeilen")


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
[( )] falsch
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

## Heap

### Heapsort


 - Heap Sort

   - Basierend auf Heaps kann man eine Sortiermethode implementieren

   - Idee: Füge alle Elemente in den Heap ein

   - Extrahiere dann der Reihe nach alle Minima

   - Diese Elemente sind dann aufsteigend (bzw. absteigend bei max-heap) sortiert. Komplexität?

[(X)] $O(n\log (n))$
[( )] $O(n^2)$
[( )] $O(n\cdot \log (n) + n\cdot \log (n^2))$
******

Es werden $n$ Elemente eingefügt in jeweils $O(\log(n))$ und anschließend $n$ Elemente in $jeweils $O(\log(n))$ entfernt.

******

## Binary Heap

Für einen Heap mit $n$ Einträgen, wann ist am Index $i$ ein Blatt des zugehörigen Baums?

[( )] $i = 2^n$
[( )] $2^n \geq i$
[( )] $2i + 2 \geq n$
[(X)] $2i + 1 \geq n$
******

Der erste Nachfolger eines Knoten am Index $i$ hat den Index $2n+1$. Wenn dieser außerhalb des Arrays liegt, muss an $i$ ein Blatt stehen.

******

### Bellman-Ford

Was ist die Laufzeitkomplexität des Algorithmus von Bellman-Ford?

[( )] $O(n^2)$
[( )] $O(m^2)$
[( )] $O(n^2 + m^2)$
[( )] $O((n + m)^2)$
[(X)] $O(m \cdot n)$
*****

Die äußere Schleife wird $n-1$ mal, die innere $m$ mal ausgeführt. Damit gilt $O(m \cdot n)$.

*****

### Bellman-Ford


Warum muss bei Bellman-Ford die äußere Schleife $|V| - 1$ mal ausgeführt
werden?

[(X)] Ein kürzester Weg hat maximal $|V| - 1$ Kanten
[( )] Das ist ein Fehler und muss $|V|$ heißen
[( )] Ein kürzester Weg hat mindestens $|V| - 1$ Kanten
[( )] Das ist ein Fehler und muss $|E| + 1$ heißen
*****

Ein kürzester Weg kann maximal $n-1$ Kanten haben, d.h. alle $n$ Knoten kommen auf dem Weg von $s$ nach $t$ vor. Damit muss die Schleife $n-1$ mal ausgeführt werden um alle Möglichkeiten sicher gefunden zu haben.

*****

### Heap Datenstruktur

Ist das ein vollständiger Binärbaum der als Heap dienen kann?

![heap](http://mgu.cs.hm.edu/imgs/07/binHeap1.png "Beispiel Baum")

[( )] ja
[(X)] nein
******

Es ist kein vollständiger Binärbaum

******


### Heap Datenstruktur

Ist dies ein vollständiger Binärbaum der als Heap dienen kann?

![heap](http://mgu.cs.hm.edu/imgs/07/binHeap2.png "Beispiel Baum")

[( )] ja
[(X)] nein
*****

Nein, da die Heapeigenschaft nicht erfüllt ist.

*****

## Hashverfahren

### Kryptographische Hashverfahren

**Wahr oder falsch** Kryptographische Hashfunktionen bilden unterschiedliche
Eingaben immer auf unterschiedliche Ausgabestrings ab.

[( )] wahr
[(X)] falsch
*****

Es gibt nur endlich viele Ausgabestrings. Damit muss es Eingaben geben, die auf gleiche Ausgaben abgebildet werden. Allerdings ist für aktuell verwendete Algorithmen keine solchen Kollisionen bekannt.

*****


### Blockchain

**Wahr oder falsch** Wenn ein Block einmal an die Blockchain an der Blockhöhe
$n$ angefügt wurde, dann kann sich das nicht mehr ändern

[( )] wahr
[(X)] falsch
****

Das ist deswegen nicht ganz richtig, da es bei den jeweils aktuellsten Blöcken dazu kommen kann, dass die Mehrheit sich anders entscheidet. Nach einer gewissen Anzahl von Bestätigungen bzw. Nachfolgeknoten ist ein Block aber sicher in der Chain und kann dann auch nicht mehr entfernt werden (außer bei 51% Attacke).

****


### Blockchain

**Wahr oder falsch** Transaktionen auf der Blockchain sind immer anonym.

[( )] wahr
[(X)] falsch
*****

Transaktionen auf einer Blockchain sind öffentlich einsehbar und erstmal nur pseudonym nicht anonym.

*****


### Blockchain

**Wahr oder falsch** Der Mempool ist zu jedem Zeitpunkt für alle Nodes des Netzwerks gleich.

[( )] wahr
[(X)] falsch
*****

Durch den beschränkten Durchsatz des Netzwerkes dauert es eine Weile bis eine neue Transaktion sich im Netzwerk als Information ausbreitet. Damit können Knoten unterschiedliche Einträge im Mempool haben. Der Großteil der Einträge ist jedoch für alle gleich.

*****

### Blockchain

**Wahr oder falsch** Eine Transaktion die bei einer Blockhöhe $n$ in den Mempool kommt wird immer in den nächsten ($n + 1$) oder übernächsten $(n+2)$ Block aufgenommen.

[( )] wahr
[(X)] falsch
*****

Es gibt keinen garantierten Zeitraum in dem eine Transaktion in einen Block aufgenommen wird.

*****


### Block Mining


Wozu wurde HashCash eigentlich entwickelt?

[( )] Test von effizienten Hardware Implementierungen von Hashalgorithmen
[( )] Ableitung von kryptographischen Schlüsseln ohne brute-force Möglichkeit
[(X)] Eindämmung von Spam Email
******

HashCash war original entwickelt, um Spam Emails einzudämmen. Die dabei war dass man zusätzlich den Proof-of-Work einträgt und nur Mails mit einem solchen Beweis akzeptiert. Da dabei Zeit verbraucht wird, wird das Versenden von Spam-Emails deutlich aufwändiger.

******


## UTxO

### UTxO 1

Sei $t_0 = (\emptyset, [0 \mapsto (a_0, 1000)])$ eine initiale
Transaktion, mit UTxO = $\{(t_0, 0) \mapsto (a_0, 1000)\}$. Danach
ist die folgende Transaktion ausgeführt worden

$t_1 = (\{(t_0, 0)\}, [0 \mapsto (a_1, 50), 1 \mapsto (a_0, 950)])$

Wie sieht die neue UTxO aus?

[( )] $\{(t_0, 0) \mapsto (a_0, 1000), (t_1, 1) \mapsto (a_0, 950), (t_1, 0)  \mapsto (a_1, 50)\}$
[( )] $\{(t_1,0) \mapsto (a_0, 950), (t_1, 1) \mapsto (a_1, 50)\}$
[(X)] $\{(t_1,1) \mapsto (a_0, 950), (t_1, 0) \mapsto (a_1, 50)\}$
******

Der Transaction Input $(t_0, 0)$ wird verbraucht und daraus werden in der Transaktion $t_1$ zwei neue Outputs erzeugt, $(t_1, 0) \mapsto (a_1, 50)$ und $(t_1, 1) \mapsto (a_0, 950)$, wobei der erste Output von $a_1$ und der zweite von $a_0$ ausgegeben werden kann.

******

### UTxO 2

Sei $t_0 = (\emptyset, [0 \mapsto (a_0, 1000)])$ eine initiale Transaktion, mit UTxO = $\{(t_0, 0) \mapsto (a_0, 1000)\}$. Danach ist die folgende Transaktion ausgeführt worden

$t_1 = (\{(t_0, 0)\}, [0 \mapsto (a_0, 950), 1 \mapsto (a_1, 50)])$

Wie sieht die neue UTxO aus?

[( )] $\{(t_0, 0) \mapsto (a_0, 1000), (t_1, 1) \mapsto (a_0, 950), (t_1, 0)  \mapsto (a_1, 50)\}$
[(X)] $\{(t_1,0) \mapsto (a_0, 950), (t_1, 1) \mapsto (a_1, 50)\}$
[( )] $\{(t_1,1) \mapsto (a_0, 950), (t_1, 0) \mapsto (a_1, 50)\}$
***

Die Transaktion konsumiert die Menge der Inputs $\{(t_0, 0)\}$, die UTxO enthält anfangs nur ein Element. Damit ist 1 Output mit Wert 1000 verfügbar. Es werden in $t_1$ 2 Outputs erzeugt, wobei der Index 0 auf $(a_1, 50)$ und der Index 1 auf $(a_0, 950)$ abgebildet wird.

Daraus entstehen dann 2 neue UTxO Einträge, $\{(t_1,0) \mapsto (a_0, 950), (t_1, 1) \mapsto (a_1, 50)\}$ beide referenzieren $t_1$, pro Index gibt es einen Eintrag und der entstandene Gesamtwert ist 1000 und damit zulässig.

***

### UTxO 3

Kann bei der UTxO $\{(t_1,1) \mapsto (a_0, 950), (t_1, 0) \mapsto (a_1, 50)\}$ jemand, der nur von $a_1$ den private key kennt, folgende Transaktion ausführen?

$t_2 = (\{(t_1, 0)\}, [0\mapsto (a_2, 50)])$

[( )] nein
[(X)] ja
****

Die Transaktion $t_2$ ist möglich. Es muss mit dem private key zu $a_1$ signiert werden, da diese UTxO nur von der Adresse $a_1$ ausgegeben werden kann. Die Transaktion erzeugt dann eine neue UTxO mit Wert 50, was dem Wert des Outputs von $(t_1,0)$ entspricht.

****

### UTxO 4

Sei die UTxO $\{(t_1,1) \mapsto (a_0, 950), (t_1, 0) \mapsto (a_1, 50)\}$ und es wird folgende Transaktion ausgeführt:

$t_2 = (\{(t_1, 0)\}, [0\mapsto (a_2, 50)])$

Wie sieht dann die resultierende UTxO aus?

[( )] $\{(t_1,1) \mapsto (a_0, 950), (t_1, 0) \mapsto (a_2, 50)\}$
[(X)] $\{(t_1,1) \mapsto (a_0, 950), (t_2, 0) \mapsto (a_2, 50)\}$
****

Die beiden Antworten unterscheiden sich nur im zweiten Element und dort nur in der Adresse des Outputs. Das es die Transaktion $t_2$ ist, die diese neue UTxO erzeugt, muss dort auch auf diese Transaktion verwiesen werden.

****

## Hashbasierte Datenstrukturen

### Bloom Filter

**Wahr oder Falsch** Bloom Filter können mit Sicherheit sagen dass ein Element
da ist und mit kleiner Fehlerwahrscheinlichkeit dass es nicht da ist

[( )] wahr
[(X)] falsch
*****

Es gilt genau umgekehrt.

*****

### Bloom Filter


Kann man Elemente aus Bloom Filter löschen?

[( )] Nein, nur eintragen
[( )] ja, einfach alle hashen und die entsprechenden Stellen mit 0 überschreiben
[(X)] ja, aber nur einmal
******

Mit einem 2. Filter kann man Elemente einmal löschen, indem man sie dort einträgt und dann testen kann ob ein Element auch dort verzeichnet ist. Allerdings sind damit nicht mehr die gleichen Eigenschaften erfüllt.

******
