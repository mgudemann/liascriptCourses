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
