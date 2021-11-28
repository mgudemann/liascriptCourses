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
