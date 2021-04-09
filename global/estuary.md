# estuary view functions 

  1. open a new browser tab at https://estuary.mcmaster.ca
  2. go to solo mode
  3. enter into the terminal: 

```
!presetview default (return to the default view)
!localview audiomap (list all samples)
!localview [] (show visuals only)
```

# JSoLang reuse vars example

## What is it?

A way to define a new livecoding meta-language on the fly (live) in estuary(!)

It uses peg.js as a parser (peg.js provide an online parser for debugging too)

## How to

This example is like a replacement for `let` in tidal - define reusable code referenced via variables

eval in a low number panel

```
##JSoLang simple-text-replacement

// an example JSoLang that takes provided text
// and applies some number of rules to replace text
// with alternate text. Basic idea: repeatedly try
// to match specific rules that return something
// different than the text they match, and whenever
// that fails simply match and return the next character

main = x:allRules* { return "##tidal\n" + x.join("") }
allRules = chords / anyCharacter
anyCharacter = .

// specific replacement rules, the i makes the find operation
// case insensitive
chords = "chords"i { return "<[c4'm9'8@1.5 af'maj9@1 g4'dom7@1.5 ] c4'm9'16 c'm9'12>" }
```

use the `chords` var in another panel

```
##simple-text-replacement 

note (arp "<[up down thumbup] down down>" "chords")
# s "sid"
```