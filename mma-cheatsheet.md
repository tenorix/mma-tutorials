# MMA Cheatsheet


This cheatsheet presents a useful subset of the keywords and functionality of  **MMA - Musical MIDI Accompaniment**. MMA is a powerful MIDI accompaniment generator with lots of functionality giving you total control of the generated backing track, so be sure to refer to the [MMA online documentation](https://www.mellowood.ca/mma/online-docs/html/mma.html). MMA is created and maintained at [www.mellowood.ca/mma/](https://www.mellowood.ca/mma/) by Bob van der Poel. *Note: Playing MIDI files on a computer with a cheap on-board sound card will probably result in bad sound quality and frustration - that is not an MMA problem.*

# Writing a Backing Track in Bar by Bar Chord Notation

## Initial Groove, Tempo and Volume

```
Groove 8beat1
Tempo 80
Volume mf
```

**Groove** Select a groove defined in the library or current .mma file. An .mma library file (/lib subdirectories) typically contains several variants of a groove. See *[MMA library docs](https://www.mellowood.ca/mma/online-docs/html/lib/index.html).* \
**Tempo** e.g. 70 bpm `Tempo 70` \
**Volume**  e.g. `Volume mf` as in conventional score notation  `pp` `p` `mp` `m` `mf` `f` `ff`

## Chord Notation 
### without bar numbers
```
C Am / /    // a comment
F / G7 /
```
### with bar numbers
```
1 C Am / /
2 F / G7 /
```
One line per bar, one chord per beat. Use `/` or `-` to repeat the chord for a beat. Comments start with `//`\
*[MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node8.html)*

## Chords
**Chord roots** `A` `A#` `Ab` `B` `B#` `Bb` `C` `C#` `Cb` `D` `D#` `Db` `E` `E#` `Eb` `F` `F#` `Fb` `G` `G#` `Gb` \
**Chord types** major `7` `maj7` minor `m` `m7` `m7b5` diminished `dim7` suspended `sus2` and many more\
**Slash chords** e.g. A/F \
*[MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node36.html#SECTION003610000000000000000)*

## Muting
```
z     // works without chord
z!    // works without chord
C/zD  // only with a chord 
C/zB  // only with a chord 
C/zC  // only with a chord 

```
**Mute** all tracks except drums `z` all tracks `z!` drum tracks `zD` bass tracks `zB` chord tracks `zC`\
*[MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node8.html#SECTION00840000000000000000)*

## Bar Repeat
```
C Am / / * 2
```
## Lyrics

```
1 C Am / / [ohh I love]
2 F / G7 / [you so]
```

## Solo/Melody

### Single notes example
```
F 	/ 	G 	/	{ 4a ; 16r ; 16c+ ; 16 d+ ; 16e+ ; 4.d+ ; 8c+ ; }
```
**Length** `1` `2` `4` `8` `16` combined `4+8` equals `4.`
**Notes** `a` `a#` `a&` `b` `b#` `b&` `c` `c#` `c&` `d` `d#` `d&` `e` `e#` `e&` `f` `f#` `f&` `g` `g#` `g&` **Rest** `r` **Octave** up `+` or down `-` \
*[MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node10.html#chap-solo)*

### Multiple notes example
```
C5 	/ 	/ 	z	{ 8c+ g ; c ; 8c+ g ; c ; 8c+ g ; c ; }
```

## Repeat

### Simple repeat
```
Repeat
C / Am /
F / G7 /
RepeatEnd
```
Bars between `Repeat` and `RepeatEnd` are repeated.

### Repeat with alternative end
```
Repeat
C / Am /    // part 1
RepeatEnding
F / G7 /    // part 2
RepeatEnd
C / / /     // end
```
will result in: part 1 - part 2 - part 1 - end.

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
# Defining Your Own Grooves

A **groove** consists of a number of tracks played in parallel. A **track** is a single voice (e.g. AcousticBass) playing a pattern, like a musician. A **pattern** is a definition for a voice which describes what rhythm to play during the current bar. The actual notes selected for the rhythm are determined by the song bar data in the bar by bar chord notation. A groove is defined in the following way 
- specify the patterns* with `Drum Define`, `Bass Define` or `Chord Define`
- define a number of tracks  based on those patterns with `Sequence`
- 'freeze' the currently define tracks into a groove with the `GrooveDef` statement.

\*) MMA has different track types that model what a musician is doing in a band. Each track type has its own way of specification as a pattern. Only drum, chord and bass are currently described in this cheat sheet. Other MMA track types are walk, plectrum, arpeggio, scale, solo and melody, automatic melodies, see [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node3.html).

## Time Signature
```
SeqClear
SeqSize 1
Time 4/4
```
**SeqClear** clear all sequences, start afresh \
**SeqSize** number of bars for following sequences, keep it simple with `1`, specify longer sequences with `2` ... \
**Time signature** `2/4` `3/4` `4/4` `6/8`

## Drum Pattern
```
Drum Define D1  1 4 90 ; 3 4 90
Drum Define S1  3 4 90
Drum Define CH1 1 4 90
Drum Define H1  CH1 * 4
```
**Drum pattern format** per line `Drum Define <pattern name> <position> <duration> <volume> ; ... ; ...`.  \
**\<pattern name\>** whatever name you choose \
**\<position\>** `1` `1.5` `2` `2.5` `3` `3.5` `4` `4.5` triplets e.g. `4` `4.3` `4.6` \
**\<duration\>**  `1` `2` `4` `8` `16` combined `4+8` equals `4.`\
**\<volume\>** standard patterns in the library are based on initial value `90`

## Bass Pattern
```
Bass Define B1 1 4+8 1 60 ; 2.5 8 1 50 ; 3 8 1 50 ; 3.5 4 1 50 ; 4.5 8 1 50
Bass Define L1 1 2+4 1 90
```
**Bass pattern format** per line `Bass Define <pattern name> <position> <duration> <offset> <volume> ; ... ; ...`.  \
**\<pattern name\>** whatever name you choose \
**\<position\>** `1` `1.5` `2` `2.5` `3` `3.5` `4` `4.5`\
**\<duration\>**  `1` `2` `4` `8` `16` combined `4+8` equals `4.`\
**\<offset\>** is an integer giving the offset from the root note, root note `1` third `3` fifth `5`. Octave modifiers: one octave down e.g. `5-` one octave up e.g. `5+`  \
**\<volume\>** standard patterns in the library are based on initial value `90`

## Chord Pattern
```
Chord Define C1 1 1 80 ; 2 1 60 ; 3 1 60 ; 4 1 60
```
**Simple chord pattern format** per line `Chord Define <pattern name> <position> <volume> ; ... ; ...`  \
**\<pattern name\>** whatever name you choose \
**\<position\>** `1` `1.5` `2` `2.5` `3` `3.5` `4` `4.5`\
**\<volume\>** standard patterns in the library are based on initial value `90`

## Tracks
```
Begin Drum-Kick
   Sequence D1 
   Tone KickDrum1 
End
Begin Drum-Snare  
   Sequence S1 
   Tone SnareDrum1
End
Begin Drum-HH
   Sequence H1 
   Tone ClosedHiHat 
End
Begin Bass-Simple
	Sequence B1 
	Voice AcousticBass
End
Begin Bass-LeftHandPiano 
	Sequence L1 
	Voice Piano1
End
Begin Chord-RightHandPiano 
	Sequence C1
	Voice Piano1
End
```
**Drum Tone**  e.g. `KickDrum1` `SnareDrum1` `ClosedHihat`  \
**Bass Voice** e.g. `AcousticBass` `ContraBass` `FingeredBass` `FretlessBass` `PickedBass` `Piano1` \
**Chord Voice** e.g. `Piano1` `Piano2` `Piano3` `CleanGuitar` `NylonGuitar` `SteelGuitar` \
See the complete list of predefined values for MIDI voices, see [MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node36.html#SECTION003620000000000000000)

*[MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node5.html#SECTION00510000000000000000)*

### Defining a Groove
```
DefGroove myGroove
```
`DefGroove` defines a groove by freezing the currently defined tracks in the section *above*, starting from the `SeqClear` to `DefGroove`.  
*[MMA reference manual](https://www.mellowood.ca/mma/online-docs/html/ref/node6.html)*


### Accent
```
Bass Define X1 1 4 1 100 ; 2.5 8 1 50 ; 3 8 1 50 ; 3.5 4 1 50 ; 4.5 8 1 50
```
is the same as
```
Bass Define X1 1 4 1 80 ; 2.5 8 1 80 ; 3 8 1 80 ; 3.5 4 1 80 ; 4.5 8 1 80
Accent         1    +20 ; 2.5    -20 ; 3    -20 ; 3.4    -20 ; 4.5    -20
```


