<!--
author: Prof. Matthias Güdemann

icon: https://upload.wikimedia.org/wikipedia/de/thumb/e/e8/Hochschule_Muenchen_Logo.svg/320px-Hochschule_Muenchen_Logo.svg.png

comment: Fragen aus QA zu Kryptographie

logo: https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Orange_blue_public_key_cryptography_de.svg/640px-Orange_blue_public_key_cryptography_de.svg.png

email:  matthias.guedemann@hm.edu

import: https://raw.githubusercontent.com/LiaScript/CodeRunner/master/README.md

-->

# Kryptographie

Die Sammlung vieler Fragen aus den synchronen QA Veranstaltungen der Vorlesung
**Kryptographie**

## GPG / PGP

**Was ist PGP / GPG**

[[X]] Programme zum Verschlüsseln und Signieren von Emails
[[ ]] Eine Designerdroge sowie eine Variante davon
[[X]] Pretty Good Privacy - ein Programm von Phil Zimmermann
[[X]] GnuPG - eine Implementierung von Werner Koch
******

BGP steht für *pretty good privacy* und ist für Email Verschlüsselung und
Signaturen gedacht. GnuPG (in Form der Programms `gpg`) ist die GNU
Implementierung davon.

******

## Breaking RSA

Gegeben: eine Menge echter RSA public keys (1024 Bit)

Aufgabe: finde für einige davon die zugehörigen private keys

Ist das möglich?

[( )] Nein, zumindest nicht effizient weil Primfaktoren nicht effizient gefunden werden können.
[( )] Ja, weil Primfaktorzerlegung mittlerweile effizient zu lösen ist PRIMES is in P
[(X)] Ja, falls es public keys gibt, die sich einen Primfaktor teilen. Dann kann mit dem euklidischen Algorithmus schnell der ggT bestimmt werden.
******

Der ggT von `a` und `b` kann sehr schnell berechnet werden in `O(log (a +
b))`. Damit kann dieser Angriff tatsächlich realistisch durchgeführt werden und
wurde es auch http://www.loyalty.org/~schoen/rsa/.

******

## Hashfunktionen

### Hash-Kollisionen

Wir schreiben $M$ für eine Nachricht (also ein BitString beliebiger
Länge) und $H(M)$ für den Hashwert einer Nachricht (also ein BitString
mit fester Länge $n$).

Was ist dann einfacher zu finden?

[( )] Zu einer gegebenen Nachricht $M$ ein $M'$ mit $H(M) = H(M')$
[(X)] Zwei beliebige Nachrichten $M$ und $M'$ mit $H(M) = H(M')$
***

Es ist wesentlich einfacher, zwei *beliebige* Nachrichten zu finden, die zum
gleichen Wert gehashed werden, als zu einem gegebenen Hashwert eine weiter
Nachricht mit gleichem Hash zu finden.

***

### Geburtstagsparadox

Sei $H$ eine Hashfunktion mit $n$ Bits Ausgabelänge. Wie viele
$M$ und $M'$ muss man ungefähr testen, um wahrscheinlich (mit
$P > 0.5$) welche zu finden mit $H(M) = H(M')$?

[( )] ca. $2^n$
[( )] ca. $2^{n-1}$
[(X)] ca. $\sqrt{2^n}$
***

Das sog. *Geburtstagsparadox* besagt, dass bei 23 (ca. $\sqrt{365}$) Personen im
Raum die Wahrscheinlichkeit dass 2 am selben Tag Geburtstag haben größer ist,
als dass dies nicht so ist.

**Wichtig** es geht nicht um einen konkreten Tag, sondern nur dass 2 am gleichen
Tag Geburtstag haben, egal welches Datum das auch ist.

Das gleiche Prinzip gilt auch bei Hashwerten, wenn man
$\sqrt{2^n}=2^\frac{n}{2}$ Dokumente testet, dann findet man mit $P > 0.5$ eine
Kollision.

***
