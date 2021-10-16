MMA Cheatsheet
----

Initial Groove and Tempo
----

Select a defined **Groove** from the library, e.g. `Groove Ballad`. Several variants of a particular style are defined in each .mma library file in the /lib subdirectories. See *[MMA library docs](https://www.mellowood.ca/mma/online-docs/html/lib/index.html).*

**Tempo** `Tempo <bpm>` beats per minute

Bar by Bar Chord Notation
----
One line per bar, one chord per beat. Use `/` or `-` to repeat the chord for a beat. Comments start with `//`\
*see [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node8.html)*

**Chord notation without bar numbers** (example)
```
C Am / /    // a comment
F / G7 /
```
**Chord notation with bar numbers** (example)
```
1 C Am / /
2 F / G7 /
```
Chords
----
**Chord roots** `A` `A#` `Ab` `B` `B#` `Bb` `C` `C#` `Cb` `D` `D#` `Db` `E` `E#` `Eb` `F` `F#` `Fb` `G` `G#` `Gb` \
**Chord types** major `7` `maj7` minor `m` `m7` `m7b5` diminished `dim7` suspended `sus2` and many more\
**Slash chords** e.g. A/F \
*see [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node36.html#SECTION003610000000000000000)*

Muting
----
**Mute** all tracks except drums `z` all tracks `z!` drum tracks `zD` bass tracks `zB` chord tracks `zC`\
*see [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node8.html#SECTION00840000000000000000)*

**Bar repeat** (example)
```
C Am / / * 2
```
**Lyrics** (example)
```
1 C Am / / [ohh I love]
2 F / G7 / [you so]
```

Solo/Melody
----

*single notes example*
```
F 	/ 	G 	/	{ 4a ; 16r ; 16c+ ; 16 d+ ; 16e+ ; 4.d+ ; 8c+ ; }
```
**Length** `1` `2` `4` `8` `16` combined `4+8` equals `4.`
**Notes** `a` `a#` `a&` `b` `b#` `b&` `c` `c#` `c&` `d` `d#` `d&` `e` `e#` `e&` `f` `f#` `f&` `g` `g#` `g&` **Rest** `r` **Octave** up `+` or down `-` \
*see [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node10.html#chap-solo)*

*multiple notes example*
```
C5 	/ 	/ 	z	{ 8c+ g ; c ; 8c+ g ; c ; 8c+ g ; c ; }
```

Repeat
----


**Simple repeat** (example)
```
Repeat
C / Am /
F / G7 /
RepeatEnd
```
Bars between `Repeat` and `RepeatEnd` are repeated.

**Repeat with alternative end** (example)
```
Repeat
C / Am /    // part 1
RepeatEnding
F / G7 /    // part 2
RepeatEnd
C / / /     // end
```
results in part 1 - part 2 - part 1 - end.

Truncate
----

**Truncate** following bar to 2 beats `Truncate 2`

Tempo Change
----

Change tempo to 100 bpm over next 2 bars `Tempo 100 2` slow down by 20 beats over next 2 bars `Tempo -20 2`



…
