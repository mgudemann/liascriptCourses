<!--
author: Prof. Matthias Güdemann

icon: https://upload.wikimedia.org/wikipedia/de/thumb/e/e8/Hochschule_Muenchen_Logo.svg/320px-Hochschule_Muenchen_Logo.svg.png

comment: Fragen aus QA zu Programmverifikation

logo: https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Orange_blue_public_key_cryptography_de.svg/640px-Orange_blue_public_key_cryptography_de.svg.png

email:  matthias.guedemann@hm.edu

version: 0.0.1

-->

# Programmverifikation

In der Vorlesung zur Prorammverifikation geht es um die Verifikation von C Programmen. Dabei wird deduktive Verifikation, Abstrakte Interpretation sowie SAT/SMT basiertes Bounded Model-checking genutzt

[ZPA](https://zpa.cs.hm.edu/public/module/185/)

## Prädikatenlogik

### Prädikatenlogik 1

Das Prädikat $bei(x, y)$ gilt gdw. Person $x$ sich bei Person $y$ aufhält.
$\forall x\, y, bei(x,y) \leftrightarrow bei (y, x)$ und $\forall x,
bei(x, x)$.

Welche Aussage formuliert *Es gibt eine Person, die alleine ist* ?

[(X)] $\exists p_1, \forall p_2, (p_1 \in Person \wedge p_2 \in Person \wedge p_1 \neq p_2) \rightarrow \neg bei(p_1, p_2)$
[( )] $\forall p_2, \exists p_1, (p_1 \in Person \wedge p_2 \in Person \wedge p_1 \neq p_2) \rightarrow \neg bei(p_1, p_2)$
[( )] keines
****

Es gibt eine Person $p_1$ so dass für alle $p_2$, die nicht gleich $p_1$ sind,
gilt dass $p_1$ nicht bei $p_2$ ist. Das heißt, $p_1$ ist alleine.

****

### Prädikatenlogik 2

Sei :math:`a` ein Array der Länge :math:`n`, :math:`a` ist aufsteigend
sortiert, gdw. wenn

[[X]] $\forall i\, j, (i\in\mathbb{N} \wedge j \in \mathbb{N} \wedge 0 \leq i < j < n) \rightarrow a[i] \leq a[j]$
[[X]] $\forall i, (i \in \mathbb{N} \wedge 0 \leq i < n - 1) \rightarrow a[i] \leq a[i + 1]$
[[ ]] keines von beiden
****

Beide Varianten sind logisch äquivalent. Die erste Variante redet **global** über alle Nachfolgeelemente, die zweite Variante redet **lokal** nur über den direkten Nachfolger.

****

### Induktionsregel

Schlussregel: $\underset{\forall n, P(n)}{\underline{P(0) \hspace{1cm} \forall n, P(n) \rightarrow P(n + 1)}}$

Was bedeutet die Schlussregel?

[[ ]] Das obere folgt aus dem unteren
[[X]] Wenn ich die beiden oberen Ziele zeige, habe ich das untere bewiesen
[[X]] Ich kann die unendlich vielen Aussagen $P(n)$ auf 2 Fälle reduzieren
****

Die Induktionsregel besagt, dass wenn man eine Aussage $P$ für eine natürliche Zahl $m$ (meistens 0) zeigen kann **und** wenn man zeigen kann dass für alle natürlichen Zahlen aus der Aussage $P(n)$ auch $P(n+1)$ folgt, dann hat man die Aussage für alle natürlichen Zahlen $\geq m$ gezeigt. Damit hat man den Beweis der unendlich vielen Fälle auf 2 Fälle reduziert (Basis und Induktionsschritt).

****

## Hoarelogik

```c
   {0 <= n}
   i := 0;
   s := 0;
   while (i < n)
     i := i + 1;
     s := s + i;
```

Was ist eine Schleifen**variante** für das Programm?

[( )] $i$
[( )] $n$
[(X)] $n - i$
[( )] $i \cdot n$
***

Eine Schleifenvariante beweist Terminierung. Dazu muss man eine Funktion definieren, die nach unten beschränkt ist und streng monoton fällt.

***

## C

### Unspecified Behavior

```c
   int f () {
   int x = 0;
   x = (x=1) + (x=2);
          return x;
   }
```

[( )] 0
[( )] eine tritt eine Exception auf
[( )] 3
[( )] 4
[(X)] kann man nicht sagen
***

Tatsächlich gibt es bei C neben **undefined** behavior auch **unspecified** behavior bei dem das Ergebnis je nach Implementierung unterschiedlich ausfallen kann.

Die Reihenfolge der Auswerungen von Parametern ist nicht vorgegeben, deswegen kann es hier tatsächlich zu unterschiedlichen Ergebnissen kommen.

***

### CFG

```c
   int f(int n) {
     int acc = 0;
     int i = 0;
     while (i < n) {
         acc = acc + 2;
         i++;
       }
     return acc;
   }
```

Wie viele Basic Blocks hat dieser Code?

[( )] 1
[( )] 2
[( )] 3
[( )] 4
[( )] mehr
***

Ein Basic Block ist ein linearer Codeabschnitt ohne Verzweigungen. Im Kontrollflussgraphen (CFG) sind Basic Blocks die Knoten und es gibt Kanten zwischen Knoten, wenn der Kontrollfluss sich von einem zum anderen Block bewegen kann.

Aufzweigungen des CFG gibt es immer bei Schleifen oder Bedingungen. Mit **CBMC** kann man den CFG im GraphViz Format unter Linux oder MacOS erstellen mit:

```
> goto-cc -c datei.c
> goto-instrument -dot datei.c | tail -n +2 | dot -Tpng > datei.png
```

***

### RTE

Was ist der Wertebereich eines C $int$?

[( )] dazu gibt es im Standard keine Aussage
[( )] $[-2^n, 2^n]$  z.B. für $n = 31$ oder $n = 63$
[( )] mindestens $[-(2^n - 1), 2^n -1]$ z.B. für $n = 31$ oder $n = 63$
[(X)] $[INT\_MIN, INT\_MAX]$ mit mindestens 16 Bit
[( )] $[INT\_MIN, INT\_MAX]$ mit mindestens 32 Bit
****

Viel wird im C Standard dazu nicht garantiert. Insbesondere ist nicht gesagt, dass es in 2er-Komplement Darstellung passiert (d.h. von $-2^n-1$ bis $2^)

****
