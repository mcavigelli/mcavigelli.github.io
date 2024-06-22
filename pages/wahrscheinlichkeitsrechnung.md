<!--
.. title: Wahrscheinlichkeitsrechnung
.. slug: wahrscheinlichkeitsrechnung
.. date: 2024-05-27
.. tags: Mathe
.. type: text
.. has_math: true
-->

# Quellen

Bronstein, Semendjajew, Musiol, Mühlig: Taschenbuch der Mathematik, 1993,
Seiten 498-500.

## Permutationen

\\[P_n \\] mit n verschiedenen Elementen

### ohne Wiederholungen

\\[P_n = n! \\]

* Ordne drei T-Shirt der Farben rot, grün blau an: (rgb,rbg,grb,gbr,brg,bgr) 

\\[P_3 = 3! = 6 \\]

Englische Aussprache: "3 factorial".

### mit Wiederholungen

\\[{P_n}^{(k)} = \frac{n!}{k!} \\]

* Eine Reihe von 10 Sitzplätzen wird von 10 Schüleretuis belegt. 4
Schüleretuis sind identisch. Wieviele Möglichkeiten gibt es?

\\[{P_{10}}^{(4)} = \frac{10!}{4!} = 15'120 \\]

## Kombinationen

Bei Kombinationen spielt die Reihenfolge keine Rolle.

### ohne Wiederholungen

\\[{C_n}^{(k)} = \binom{n}{k} = \frac{n!}{k!(n-k)!} \\]

* Ein Salatbuffet besteht aus 5 Salaten. Du musst 3 verschiedene Salate
wählen: Wieviele unterschiedliche Salatteller kannst du zusammen stellen?

\\[{C_5}^{(3)} = \binom{5}{3} = \frac{5!}{3!(5-3)!} = 10\\]

Mögliche Aussprache: "C index 5 von 3"

* Für den Skiclub soll ein 4 köpfiger Vorstand gewählt werden. Die
Funktionen der Personen sind gleichgültig. Es stehen 21 Personen zur
Verfügung. Wie viele Kombinationen gibt es?

\\[{C_{21}}^{(4)} = \binom{21}{4} = \frac{21!}{4!(21-4)!} = \frac{21 * 20 * 19 * 18}{24}= 5'985\\]

### mit Wiederholungen

\\[{C_n}^{(k)} = \binom{n + k -1}{k} \\]

* Wieviele verschiedene Würfe können mit 2 Würfeln geworfen werden?

\\[{C_6}^{(2)} = \binom{6 + 2 -1}{2} = \binom{7}{2} = \frac{7!}{2! * 5!} = 21 \\]

## Variationen

Bei Variationen ist die Reihenfolge signifikant.

### ohne Wiederholungen

Eine Person steht nur 1x zur Verfügung, oder eine Kugel aus einem Topf
wird nicht mehr zurückgelegt.

\\[{V_n}^{(k)} = {k!}\binom{n}{k} = k!\frac{n!}{k!(n-k)!} = \frac{n!}{(n-k)!} \\]

* Für den Skiclub soll ein 4 köpfiger Vorstand mit unterschiedlichen
Funktionen gewählt werden. Es stehen 21 Personen zur
Verfügung. Wie viele Kombinationen gibt es?

\\[{V_{21}}^{(4)} = \frac{21!}{17!} = 143'640 \\]

Englische Aussprache: "21 factorial divided by 17 factorial".

### mit Wiederholungen

\\[{V_n}^{(k)} = \{n}^{k} \\]

* Ein Handy ist durch einen vierstelligen Zahlencode geschützt. Wie 
viele Variationen gibt es?  

\\[{V_{10}}^{(4)} = \{10}^{4} = 10'000 \\]

Englische Aussprache: "10 to the power of 4".

