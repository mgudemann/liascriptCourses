<!--
author: Prof. Matthias Güdemann

icon: https://upload.wikimedia.org/wikipedia/de/thumb/e/e8/Hochschule_Muenchen_Logo.svg/320px-Hochschule_Muenchen_Logo.svg.png

comment: Fragen aus QA zu Theoretische Informatik 2

logo: https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Orange_blue_public_key_cryptography_de.svg/640px-Orange_blue_public_key_cryptography_de.svg.png

email:  matthias.guedemann@hm.edu

version: 0.0.1

-->

# Theoretische Informatik 2

In der Vorlesung zur theoretischen Informatik 2 geht es um das
Erfüllbarkeitsproblem (SAT), allgemein um Entscheidungsprozeduren sowie die
Erweiterung zum Satisfiability Modulo Theory (SMT) Problem.

[ZPA](https://zpa.cs.hm.edu/public/module/247/)

## Aussagenlogik

### Interpretation

**Disjunktion** $F \vee G$ ist *True*, gdw. $F$ **oder** $G$ als *True*
interpretiert werden.

Wenn $A$ als *False* und $B$ als *True* interpretiert
werden, hat dann

[(X)] $\neg A \vee B$ den Wert *True*
[( )] $\neg A \vee B$ den Wert *False*
****

$\neg A$ wird dabei als *True* interpretiert und somit wird $\neg A \vee B$
sogar unabhängig von $B$ ebenfalls als *True* interpretiert.

****

### Basis von Operatoren

**Basis** eine Teilmenge von logischen Operatoren heißt *Basis* wenn diese
Teilmenge ausreichend ist, alle anderen Operatoren äquivalent darzustellen.

Welche Menge von Operatoren reicht aus, um alle aussagenlogischen Formeln
darstellen zu können?

[[X]] Es reichen $\neg, \wedge$
[[X]] Es reichen $\neg, \vee$
[[ ]] Keines der beiden oben reicht aus
*****

Mit der Negation und Disjunktion bzw. auch mit der Negation und Konjunktion
kann man alle anderen logischen Operatoren äquivalent darstellen.

Oft ist es allerdings besser lesbar, wenn man weitere Operatoren zulässt.

Eine möglichst kompakte Basis wird in der Regel für interne Darstellungen von
Tools genutzt, da dort effiziente Verarbeitung wichtiger ist als Lesbarkeit.

*****


## Normalformen

### NNF

Ist $\neg (x1 \vee x2) \leftrightarrow \neg (x1 \rightarrow x2)$ in NNF?

[( )] ja
[(X)] nein
****

Bei der Negationsnormalform (NNF) dürfen nur Konjunktion, Disjunktion und
Negation vorkommen, wobei die Negation auch nur als innerster Operator erlaubt
ist!

Da hier eine Implikation vorkommt, kann keine NNF vorliegen.

****

### CNF

Ist $(x1 \vee x2) \vee (x1 \wedge x2)$ in CNF?

[( )] ja
[(X)] nein
****

In konjunktiver Normalform ist eine aussagenlogische Formel genau dann, wenn sie
in NNF ist und sie eine Konjunktion von Disjunktionen ist.

CNF ist wohl die am weitesten verbreitete der Normalformen und wird so in SAT
Solvern verwendet, realisiert als DIMACS CNF Format.

****


### DNF

Eine Formel ist in **CNF** wenn es eine **Konjunktion von Disjunktionen**
ist. Welche Formel ist dann analog in disjunktiver Normalform (**DNF**)?

[[X]] $A \vee B$
[[X]] $A \vee (B \wedge C)$
[[X]] $A$
[[X]] alle
[[ ]] keine


### Tseitin Transformation


Ist die folgende Aussage wahr?

  Sei `T(F)` die Tseitintransformierte der aussagenlogischen Formel `F`. Dann
  sind `F` und `T(F)` **äquivalent** und `T(F)` ist in CNF.

[( )] ja
[(X)] nein
****

Die Transformation von Tseitin erzeugt ebenfalls eine CNF, allerdings garantiert
in linearer Zeit.

Es werden allerdings zusätzliche *Hilfsvariablen* eingefügt, so dass das
Resultat nur **erfüllbarkeitsäquivalent** ist. Das heißt: $F$ ist erfüllbar
gdw. $T(F)$ erfüllbar ist.

****


## Erfüllbarkeit (SAT)

### SAT 1

Ist folgende aussagenlogische Formel erfüllbar?

$(\neg A \vee u \vee \neg l) \wedge(\neg A \vee \neg u \vee \neg l) \wedge(A \vee \neg U \vee \neg L) \wedge(\neg A\vee u \vee l) \wedge(A \vee U \vee \neg L) \wedge(\neg A \vee \neg u \vee l) \wedge(A\vee U \vee L) \wedge(A \vee \neg U \vee L)$

[( )] ja
[(X)] nein
****

Die Formel ist die erfüllbarkeitsäquivalente 3-SAT Form von $A \wedge \neg A$
und ist damit nicht erfüllbar.

****

### SAT 2

Zu was ist die Klausel $A \vee \neg B \vee \bot \vee C$
äquivalent?

[( )] $True$
[( )] $False$
[(X)] $A \vee \neg B \vee C$
[( )] nichts davon
*****

Wenn innerhalb einer Klausel die Konstante $\bot$ auftaucht, dann ist die
Klausel logisch äquivalent zur Klausel ohne die Konstante. Das liegt daran, dass
$\bot$ das neutrale Element von $\vee$ ist

*****

### SAT 3

Zu was ist die Klausel $A \vee \neg B \vee \top \vee C$ äquivalent?

[(X)] $True$
[( )] $False$
[( )] $A \vee \neg B \vee C$
[( )] nichts davon
*****

Wenn innerhalb einer Klausel die Konstante $\top$ auftaucht, dann ist die
Klausel trivialerweise wahr.

*****
