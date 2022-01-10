<!--
author: Prof. Matthias Güdemann

icon: https://upload.wikimedia.org/wikipedia/de/thumb/e/e8/Hochschule_Muenchen_Logo.svg/320px-Hochschule_Muenchen_Logo.svg.png

comment: Fragen aus QA zu Kryptographie

logo: https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Orange_blue_public_key_cryptography_de.svg/640px-Orange_blue_public_key_cryptography_de.svg.png

email:  matthias.guedemann@hm.edu

version: 0.0.2

-->

# Kryptographie

In der Vorlesung zu Kryptographie geht es um moderne Anwendungen kryptographischer Operationen. Insbesondere wird das Rechnen auf elliptischen Kurven und das zugehörige Probleme des diskreten Logarithmus (DLP) betrachtet.

[ZPA](https://zpa.cs.hm.edu/public/module/356/)

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

## Public Key Kryptographie

Bei Public key Kryptograhpie gibt es ein Schlüsselpaar zum Austausch von
Nachrichten. Der öffentliche (**public key**) Schlüssel kann beliebig publiziert
werden und dient zum **Verschlüsseln**, der private (**private key**) Schlüssel
dient zum **Entschlüsseln**. Der private Schlüssel muss unbedingt geheim
bleiben.

Es gibt mehrere Verfahren zur public key Kryptographie. Alle basieren auf einer
sogenannten **Falltürfunktion** die einfach zu berechnen aber schwierig zu
invertieren ist. Das vermutlich bekannteste Beispiel dazu ist das RSA (Rivest,
Shamir, Adleman) Verfahren welches auf der Primfaktorzerlegung sehr großer
ganzer Zahlen basiert.

### Breaking RSA

Gegeben: eine Menge echter RSA public keys (1024 Bit)

Aufgabe: finde für einige davon die zugehörigen private keys

Ist das möglich?

[( )] Nein, zumindest nicht effizient weil Primfaktoren nicht effizient gefunden werden können.
[( )] Ja, weil Primfaktorzerlegung mittlerweile effizient zu lösen ist **PRIMES is in P**
[(X)] Ja, falls es public keys gibt, die sich einen Primfaktor teilen. Dann kann mit dem euklidischen Algorithmus schnell der ggT bestimmt werden.
******

Der ggT von `a` und `b` kann sehr schnell berechnet werden in `O(log (a +
b))`. Damit kann dieser Angriff tatsächlich realistisch durchgeführt werden und
wurde es auch http://www.loyalty.org/~schoen/rsa/.

******

### Weiterführende Links

[Common factor attack on RSA](http://www.loyalty.org/~schoen/rsa/#challenge)

[Not playing randomdly: ecDSA hack](https://medium.com/asecuritysite-when-bob-met-alice/not-playing-randomly-the-sony-ps3-and-bitcoin-crypto-hacks-c1fe92bea9bc)

## Hashfunktionen

Hashfunktionen sind ein wesentlicher Bestandteil vieler moderner Anwendungen von
Kryptographie. Sie dienen in der Regel dazu, dass *Prüfsummen* von Dateien
bzw. Nachrichten berechnet werden.

Es gibt verschiedene standardisierte Hashfunktionen. Einige sind als Tools auf
der Kommandozeile verfügbar.

ein paar Beispiele:

```
>  echo "Kryptographie" | md5sum
f9300c33c0082e60e8850073081d1d62  -

>  echo "Kryptographie" | shasum
83a67d1760ef5ef6adbdff1a00009dd8124d872c  -

> echo "Kryptographie" | sha256sum
e93c804373c3ea62767a9cc82a78ad69012a6e9c474a93ce6a8f5a3f6f0885a8  -

> echo "Kryptographie" | rhash --sha3-512 -
04e5071bc6e54ccf174e2b10b843e264182c07eb6fc889210486d4104ec9a413baef63fc2259122d8544ba06f38ee539b36652eeacd7901183a4677c47aa3611  (stdin)
```

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

## Blockchain

### UTxO 1

Sei $t_0 = (\emptyset, [0 \mapsto (a_0, 1000)])$ eine initiale
Transaktion, mit UTxO = $\{(t_0, 0) \mapsto (a_0, 1000)\}$. Danach
sie die folgende Transaktion ausgeführt worden

$t_1 = (\{(t_0, 0)\}, [0 \mapsto (a_1, 50), 1 \mapsto (a_0, 950)])$

Wie sieht die neue UTxO aus?

[( )] $\{(t_0, 0) \mapsto (a_0, 1000), (t_1, 1) \mapsto (a_0, 950), (t_1, 0)  \mapsto (a_1, 50)\}$
[( )] $\{(t_1,0) \mapsto (a_0, 950), (t_1, 1) \mapsto (a_1, 50)\}$
[(X)] $\{(t_1,1) \mapsto (a_0, 950), (t_1, 0) \mapsto (a_1, 50)\}$
******

Der Transaction Input $(t_0, 0)$ wird verbraucht und daraus werden in der Transaktion $t_1$ zwei neue Outputs erzeugt, $(t_1, 0) \mapsto (a_1, 50)$ und $(t_1, 1) \mapsto (a_0, 950)$, wobei der erste Output von $a_1$ und der zweite von $a_0$ ausgegeben werden kann.

******

### UTxO 2

Sei $t_0 = (\emptyset, [0 \mapsto (a_0, 1000)])$ eine initiale Transaktion, mit UTxO = $\{(t_0, 0) \mapsto (a_0, 1000)\}$. Danach sie die folgende Transaktion ausgeführt worden

$t_1 = (\{(t_0, 0)\}, [0 \mapsto (a_1, 50), 1 \mapsto (a_0, 950)])$

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

## PFS

### KES

Was bringt eine Unterscheidung zwischen Hot / Cold Keys?

[( )] Der cold key nützt sich nicht ab
[( )] Geringere Wahrscheinlichkeit dass Kollisionen bei Signaturen entstehen
[(X)] Geringere Angriffsfläche zur Kompromittierung des cold keys
****

Der Vorteil eines hot/cold Key Schemas ist, dass die Angriffsfläche auf den cold-key verkleinert wird. Dieser muss i.d.R. nicht auf einem Rechner vorliegen, der auch online ist. Damit muss ein Angreifer deutlich mehr Aufwand betreiben, um den Key kompromittieren zu können.

****

### Cold Keys

Was sind weitere Varianten von cold keys?


[[X]] Paper Wallets
[[X]] 2FA key (z.B. U2F oder FIDO2 Standard)
[[X]] Hardware Wallets
[[ ]] Verschlüsselte PGP/GPG Keyrings
*****

Mit Ausnahme des PGP Keyrings sind alles Beispiele für Cold keys, in dem Sinn dass die keys nicht auf einem Rechner der online ist im Arbeitsspeicher vorhanden sind.

*****

## Commitments

### Pedersen Commitment

Pedersen Commitments sind eine Möglichkeit, ein Commitment Schema zu realisieren. Seien $g$ und $h$ Generatoren einer zyklischen  Gruppe. Dann kann man $Commit$ definieren als $Commit(m, r) = g^m\cdot h^r$

Wäre es nicht ausreichend wenn man nur $g^m$ nutzt ?

[( )] ja
[(X)] nein, kein hiding
[( )] nein, kein binding
*****

Insbesondere wenn die Message $m$ nur aus einer kleinen Menge möglicher Nachrichten stammt, liegt hier kein hiding vor. Ein Angreifer könnte alle Nachrichten enumerieren und somit herausfinden zu welcher Message das Commitment angelegt wurde.

*****

### Pedersen Commitment 2

Pedersen Commitments sind eine Möglichkeit, ein Commitment Schema zu realisieren. Seien $g$ und $h$ Generatoren einer zyklischen  Gruppe. Dann kann man $Commit$ definieren als $Commit(m, r) = g^m\cdot h^r$

Der Faktor $r$ heißt auch **Verblindungsfaktor**.

Wäre es nicht ausreichend wenn man nur $g^(r + m)$ nutzt, also keinen zweiten
Generator?

[( )] ja
[( )] nein, kein hiding
[(X)] nein, kein binding
*****

Hier ist das Problem, dass der Prover einfach ein anderes $r$ bei der Öffnung präsentieren könnte. Sei z.B. $m=1$ und initial $r=4$. Wenn nun $m=0$ von Vorteil wäre könnte der Prover $m=0$ und $r=5$ präsentieren, was das Commitment validieren würde.

*****



# Haskell Referenzen


Im folgenden eine Zusammenstellung an Code-Referenzen / Code-Schnippseln. Diese sollen helfen mit dem Typsystem von Haskell klar zu kommen.

## ToInteger

Umwandlung von **natürlichen Zahlen** in einen **Integer** <br/>
(P256K1._q ist eine Konstante vom Typ Natural)

```haskell
-- Fehler
    * Couldn't match expected type `Integer'
                  with actual type `GHC.Natural.Natural'
    * In the expression: _q
      In an equation for `demo': demo = _q
   |
22 | demo = P256K1._q
   |        ^^^^^^^^^
```

```haskell
-- Umwandlung
demo :: Integer
demo = toInteger P256K1._q
```

## P256K1 Koordinaten lesen

Folgendes Beispiel liest die Koordinaten aus einem gegebenen Punkt und gibt diese als Tupel zurück. Hierfür wird der Punkt mit einem `as Pattern` geöffnet um dessen Inhalte zu lesen und diese zu einem Integer zu konvertieren.

```haskell
-- Umwandlung
demo :: P256K1.PA -> (Integer, Integer)
demo point@(A x y) = ((toInteger x), (toInteger y))
```

## P256K1 in REPL erstellen

Mit folgenden Vorgehen kann man Punkte in der REPL **erstellen** um mit diesen zu testen. In folgenden werden zwei Punkte x und y erstellt, welche dann als Parameter im weiteren verlauf verwendet werden können um Methoden zu testen. Auch wird ein Point at infinity angelegt.

```haskell
-- Haskell repl
:m +Data.Curve.Weierstrass.SECP256K1       -- Bibliothek laden sodass diese in der repl zur verfügung steht
x = Data.Curve.Weierstrass.SECP256K1.A 1 3 -- Punkt x erstellen
y = Data.Curve.Weierstrass.SECP256K1.A 1 3 -- PUnkt y erstellen
z = Data.Curve.Weierstrass.SECP256K1.O     -- Point at infinity
```

## Integer zu Punkte uwandeln

`Disclaimer. Das folgende ist nur so in etwa mein eigenens verständniss. Keine Ahnung ob das wirklich so funktioniert ¯\_(ツ)_/¯`

Um einen Integer in einen Punkt eines Galois Körpers umzuwandeln bedarf kann folgendes verwendet werden. GF.toP überträgt einen Integer in einem Punkt. Ich vermute dass GF.Prime R hier den Galois - Körper bestimmt.
 ```haskell
demo :: Integer -> GF.Prime
demo input = GF.toP s :: GF.Prime R
```

## Inverse / Reziproke berechnen

Folgende Wege habe ich gefunden um eine Inverse zu berechnen.

```haskell
-- Schöne schreibweise
demo :: Fractional a => a -> a
demo input = recip input
```

eine Annäherung mit float / double:

```haskell
-- Technische Schreibweise.
demo :: Float -> Float
demo input = input**(-1)
```
