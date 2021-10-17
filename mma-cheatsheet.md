MMA Cheatsheet
----

This cheatsheet presents a useful, but only small subset of the keywords and functionality of  **MMA - Musical MIDI Accompaniment** - a powerful MIDI accompaniment generator. Much more in the [MMA online documentation](https://www.mellowood.ca/mma/online-docs/html/mma.html). MMA is created and maintained at [www.mellowood.ca/mma/](https://www.mellowood.ca/mma/) by Bob van der Poel.

# Writing a Backing Track in Bar by Bar Chord Notation

## Initial Groove, Tempo and Volume
----

```
Groove Metronome4
Tempo 70
Volume mf
```

**Groove** Select a groove defined in the library or current .mma file. An .mma library file (/lib subdirectories) typically contains several variants of a groove. See *[MMA library docs](https://www.mellowood.ca/mma/online-docs/html/lib/index.html).* \
**Tempo** e.g. 70 bpm `Tempo 70` \
**Volume**  e.g. `Volume mf` as in conventional score notation  `pp` `p` `mp` `m` `mf` `f` `ff`

## Chord notation without bar numbers
```
C Am / /    // a comment
F / G7 /
```
## Chord notation with bar numbers
```
1 C Am / /
2 F / G7 /
```
One line per bar, one chord per beat. Use `/` or `-` to repeat the chord for a beat. Comments start with `//`\
*see [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node8.html)*

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

## Bar repeat
```
C Am / / * 2
```
## Lyrics

```
1 C Am / / [ohh I love]
2 F / G7 / [you so]
```

## Solo/Melody

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

## Repeat

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

## Truncate

**Truncate** following bar to 2 beats `Truncate 2`

## Tempo Change

Change tempo to 100 bpm over next 2 bars `Tempo 100 2` \
Slow down by 20 beats over next 2 bars `Tempo -20 2`

## Volume Change


**Crescendo** Increase volume to mezzoforte in the next 2 bars `Cresc mf 2` \
**Decrescendo** Decrease volume to mezzopiano in the next 3 bars `Decresc mp 3` \
Volume indications `pp` `p` `mp` `m` `mf` `f` `ff`

---
# Defining your own grooves

A **groove** consists of a number of tracks played in parallel. A **track** is a single voice (e.g. AcousticBass) playing a pattern, like a musician. A **pattern** is a definition for a voice which describes what rhythm to play during the current bar. The actual notes selected for the rhythm are determined by the song bar data in the bar by bar chord notation. A groove is defined in the following way 
- specify the patterns* with `Drum Define`, `Bass Define` or `Chord Define`
- define a number of tracks  based on those patterns with `Sequence`
- 'freeze' the currently define tracks into a groove with the `GrooveDef` statement.

\*) MMA has different track types that model what a musician is doing in a band. Each track type has its own way of specification as a pattern. Only drum, chord and bass are currently described in this cheat sheet. Other MMA track types are walk, plectrum, arpeggio, scale, solo and melody, automatic melodies, see [MMA Reference Manual](https://www.mellowood.ca/mma/online-docs/html/ref/node3.html).

## Time Signature
```
SeqClear
SeqSize 1
Time 4/4
```
**Time signature** `2/4` `3/4` `4/4` `6/8`


## Drum Pattern
```
Begin Drum Define
	D1 1 4 90
	S1 3 4 90
	CH1 1 4 90
	C1 CH1 * 4
End
```
x `<label> `

## Bass Pattern


```
Bass Define B1 1 4+8 1 60 ; 2.5 8 1 50 ; 3 8 1 50 ; 3.5 4 1 50 ; 4.5 8 1 50
Bass Define L1 1 2+4 1 90
```
**Bass pattern format** per line `Bass Define <pattern name> <position> <duration> <offset> <volume> ; ... ; ...`.  \
**\<pattern name\>** whatever name you choose
**\<position\>** `1` `1.5` `2` `2.5` `3` `3.5` `4` `4.5`\
**\<duration\>**  `1` `2` `4` `8` `16` combined `4+8` equals `4.`\
**\<offset\>** is an integer giving the offset from the root note, root note `1` third `3` fifth `5` fifth. Octave modifiers: one octave down `5-` one octave up `5+`  \
**\<volume\>** MIDI standard volume `80`

## Sequence
```
Begin Bass-Simple
	Sequence B1
	Voice AcousticBass
End
```
Bass Voice e.g. `AcousticBass` `ContraBass` `FingeredBass` `FretlessBass` `PickedBass` `Piano1` \ 
Chord Voice e.g. `Piano1` `Piano2` `Piano3` `CleanGuitar` `NylonGuitar` `SteelGuitar`
Drum Tone e.g. `KickDrum1` `SnareDrum1` `ClosedHihat`  \
See the complete list of predefined values for MIDI voices, see [MMA Reference Manual](https://www.mellowood.ca/mma/online-docs/html/ref/node36.html#SECTION003620000000000000000)

Sequences: https://www.mellowood.ca/mma/online-docs/html/ref/node5.html#SECTION00510000000000000000

### Defining a Groove
```
DefGroove myGroove
```
`DefGroove` defines a groove by freezing the currently defined sequences in the section *above*, starting from the `SeqClear` to `DefGroove`.  
See [MMA Reference Manual](https://www.mellowood.ca/mma/online-docs/html/ref/node6.html)


### Accent
```
Bass Define X1 1 4 1 100 ; 2.5 8 1 50 ; 3 8 1 50 ; 3.5 4 1 50 ; 4.5 8 1 50
```
is the same as
```
Bass Define X1 1 4 1 80 ; 2.5 8 1 80 ; 3 8 1 80 ; 3.5 4 1 80 ; 4.5 8 1 80
Accent         1    +20 ; 2.5    -20 ; 3    -20 ; 3.4    -20 ; 4.5    -20
```


https://www.mellowood.ca/mma/online-docs/html/ref/node19.html#SECTION001910000000000000000

more to come ...
