<!--
.. title: Wahrscheinlichkeitsrechnung
.. slug: wahrscheinlichkeitsrechnung
.. date: 2024-05-27
.. tags: Latte
.. category: 
.. link: 
.. description: 
.. type: text
.. has_math: true
-->


# Quellen

Bronstein, Semendjajew, Musiol, Mühlig: Taschenbuch der Mathematik, 1993,
Seiten 498-500.

## Kombinationen

Bei Kombinationen spielt die Reihenfolge keine Rolle.

### ohne Wiederholungen

\\[{C_n}^{(k)} = \binom{n}{k} = \frac{n!}{k!(n-k)!} \\]

#### Beispiele

* Ein Salatbuffet besteht aus 5 Salaten. Du musst 3 verschiedene Salate
wählen: Wieviele unterschiedliche Salatteller kannst du zusammen stellen?

\\[{C_5}^{(3)} = \binom{5}{3} = \frac{5!}{3!(5-3)!} = 10\\]

* Für den Skiclub soll ein 4 köpfiger Vorstand gewählt werden. Die
Funktionen der Personen sind gleichgültig. Es stehen 21 Personen zur
Verfügung. Wie viele Kombinationen gibt es?

\\[{C_{21}}^{(4)} = \binom{21}{4} = \frac{21!}{4!(21-4)!} = \frac{21 * 20 * 19 * 18}{24}= 5'985\\]

## Variationen

Bei Variationen ist die Reihenfolge signifikant.

### ohne Wiederholungen

Eine Person steht nur 1x zur Verfügung, oder eine Kugel aus einem Topf
wird nicht mehr zurückgelegt.


\\[{V_n}^{(k)} = {k!}\binom{n}{k} = k!\frac{n!}{k!(n-k)!} = \frac{n!}{(n-k)!} \\]


#### Beispiele

* Für den Skiclub soll ein 4 köpfiger Vorstand mit unterschiedlichen
Funktionen gewählt werden. Es stehen 21 Personen zur
Verfügung. Wie viele Kombinationen gibt es?

\\[{V_{21}}^{(4)} = \frac{21!}{17!} = 143'640 \\]

### mit Wiederholungen

\\[{V_n}^{(k)} = \{n}^{k} \\]

Aussprache "n hoch k"

#### Beispiele

* Ein Handy ist durch einen vierstelligen Zahlencode geschützt. Wie 
viele Variationen gibt es?  

\\[{V_{10}}^{(4)} = \{10}^{4} = 10'000 \\]
