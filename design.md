# Hangman

A simply GUI and console based hangman game written in Python.

## Design

The application(s) are made up of the following modules

* Phrases Library
* Game Engine
* Console UI
* GUI

## Phrases Library

A module that returns (at random) a word or phrase.

It requires a local phrase file. This is called phrases.txt

There is one phrase per line.

The phrases modules has two methods:

* `load` which will fetch the file into memory
* `getPhrase` which will return a phrase at random

Future enhancements:

* Allow the file to be specified in `load` method rather than 
  be hard-coded
* Find an online resource to use as a source of phrases and
  fetch it from online
* Minimize the chances of repeats: during a given session keep track
  of seen phrases and when `getPhrase` is called check the randomly
  selected phrase against the session list. Pick another phrase if
  it's a dupe. Could also record the seen phrases to a suitable location
  so that a given user on a given machine will never see a duplicate
  phrase (assuming there is a large enough library to choose from)

## Game Engine

The game engine is responsible for implementing the rules of the game.
It has the following methods/properties:

* `newGame` which puts the engine in a new game mode: selects a new phrase, resets the available letters back full aphabet, etc.
* `phrase` A property which returns the given phrase except with `*`
  characters in place of any letters not already chosen. So initially this property will return a string composed completely of `*` characters.
* `usedLetters` A property which returns the list of already chosen letters.
* `chooseLetter` A method that chooses a specific letter. If the chosen
  letter is in the current phrase then those letters will be come visible
  in the `phrase` property.
* `bodyParts` A property that returns an array of body parts that have been
  "hung". The array will contain enums from the BodyPart enumeration.
  
Body Part Enum should have the members: `HEAD`, `NECK`, `LEFT_ARM`,
`RIGHT_ARM`, `TORSO`, `LEFT_LEG`, `RIGHT_LEG`.

Alternatively, the game engine could replace the `bodyParts` property
with `incorrectGuesses` which is a numeric property that indicates how many guesses have been made for letters that do not appear in the phrase.
This would allow a client to construct whatever user interface is deemed 
appropriate for bad guesses.

## Console App

The console app is a client of the Game Engine used to test the engine
and offer a simple hangman game on the command line.

An example session would look like this

```text
$ hangman
Welcome to Hangman

Word: *******
Guess? A

'A' is in the word
Word: A*a*a*a
Guess? M

'M' is not in the word
  O
Word: A*a*a*a
Guess? N

'N' is not in the word
  O
  |
Word: A*a*a*a
Guess? l

'L' is in the word
Word: Ala*a*a


```

The finished hangman should look like this

```
'M' is not in the word
  O
 \|/
  |
 / \

 You lose!
 Play again? (Y/N)
```

The win scenario would look like this

```text

Word: Alaba*a
Guess? m

'M' is in the word
You successfully guessed the word "Alabama"
Play again? (Y/N)
```

## GUI

A gui allows us to present a nicer looking screen.