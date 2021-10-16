MMA Cheatsheet
----

This cheatsheet presents a useful, but only small subset of the keywords and functionality of  **MMA - Musical MIDI Accompaniment** - a powerful MIDI accompaniment generator. Much more in the [MMA online documentation](https://www.mellowood.ca/mma/online-docs/html/mma.html). MMA is created and maintained at https://www.mellowood.ca/mma/ by Bob van der Poel.

Initial Groove, Tempo and Volume
----

```
Groove Metronome4
Tempo 70
Volume mf
```

**Groove** Select a groove defined in the library or current .mma file. An .mma library file (/lib subdirectories) typically contains several variants of a groove. See *[MMA library docs](https://www.mellowood.ca/mma/online-docs/html/lib/index.html).* \
**Tempo** e.g. 70 bpm `Tempo 70` \
**Volume**  e.g. `Volume mf` as in conventional score notation  `pp` `p` `mp` `m` `mf` `f` `ff`

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

Change tempo to 100 bpm over next 2 bars `Tempo 100 2` \
Slow down by 20 beats over next 2 bars `Tempo -20 2`

## Volume Change


**Crescendo** Increase volume to mezzoforte in the next 2 bars `Cresc mf 2` \
**Decrescendo** Decrease volume to mezzopiano in the next 3 bars `Decresc mp 3` \
Volume indications `pp` `p` `mp` `m` `mf` `f` `ff`

---
# Defining your own grooves

Grooves are defined in X steps. ...

## Time Signature
```
SeqClear
SeqSize 1
Time 4/4
```
**Time signature** `2/4` `3/4` `4/4` `6/8`

## Patterns


Types of patterns: `Bass` `Chord` `Drum` . For Arpeggio, Walk, Scale, Aria, Plectrum, Drum Tone see the [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node4.html#SECTION00410000000000000000).

### Drum Patterns
```
Begin Drum Define
	D1 1 4 90
	S1 3 4 90
	CH1 1 4 90
	C1 CH1 * 4
End
```
x `<label> `

### Bass Patterns

**Bass pattern format** per line `Bass Define <pattern name> <position> <duration> <offset> <volume> ; ... ; ...`.  

```
Bass Define B1 1 4+8 1 60 ; 2.5 8 1 50 ; 3 8 1 50 ; 3.5 4 1 50 ; 4.5 8 1 50
Bass Define L1 1 2+4 1 90
```
**\<position\>** `1` `1.5` `2` `2.5` `3` `3.5` `4` `4.5`\
**\<duration\>**  `1` `2` `4` `8` `16` combined `4+8` equals `4.`\
**\<offset\>** is an integer giving the offset from the root note, root note `1` third `3` fifth `5` fifth. Octave modifiiers: one octave down `5-` fifth one octave up `5+`  \
**\<volume\>** MIDI standard volume `80`

more to come ...
