# ProseLang - Esolang

Unless line beings with ">" or "*", ignore line.

Do logic processing on lines with ">".

Do string and number processing on "*" lines.

ProseLang Implementations should be *pipeable* under *nix systems, allowing you to embed its logic within other scripting languages.

## Logic Processing

### Functional Word

The first 3 characters, after the ">", are reserved for a key functional word's respresentation.

Possibilities:

* For
* If
* Whi(le)
* Set (Review?)
* Get (Review?)
* End (Review?)

End is used to close a previous loop.

### Variable Name

The first word after the first space occuring somewhere after the first 3 characters, is reserved for the variable name.

e.g. 

```
For something
Whilst blah
Settlers came
```

:. The variables are:

```
something
blah
came
```

### Test Type

The second word after the first space, occuring somewhere after the first 3 characters, is reserved for the test type.

Note: Get and Set both require "is" as the test type.

The possible test types are:

* is (equivalent to =)
* no (equivalent to !=)
* in (match in arrays or substrings)

e.g.
```
For something in
Whilst blah is
If blah not
Settlers came in
```

:. The test types are:

```
in
is
not
in
```

### Testing Value

The third word after the first space, occuring somewhere after the first 3 characters, is reserved for the testing value type.

The possibilities are:

* no (int)
* not (float)
* st (string)
* ar (array)
* ca (key-value pair)
* fu (function call)

e.g.
```
Whilst humans in North
For Victory in Nottingham!
If blah not stretched
Settlers came in aroused
Getrude smiled in funhouse
```

:. The testing value types are:

```
int
float
string
array
key-value pair
function call
```

## String and Number Processing

The number of strings or numbers that are processed are determined by the testing value type determined by the logic processing.

* An int expects 1 value, provided by summing the nouns in the third word of each "*" until the next ">", according to the map explained below.
* A float expects 5 values, or less, provided by extracting every noun in the first five words per "*", where each "*" represents a new placement in the float, as explained below.
* A string takes the second complete word at the first "*". All other "*" are ignored, until the next ">".
* An array takes the second complete word from every occuring "*", until the next ">".
* A key value pair takes the second complete word from the first and second "*". All other "*" are ignored, until the next ">".
* A function call takes the second word from the first "*" as the function, and the second word from all other "*" as arguments, until the next ">".

Numbers are represented quite simply, by mapping them as follows:

* a = +1
* e = -1
* i = +2
* o = -2
* u = 0

For example:

```
* The pink panther
```

If we were expecting an integer, then we would select the word ```panther```, and convert it to ```+1 -1```, which is equal to ```0```.

If we were expecting a float, then we would take every vowel present, equal to ```-1 +2 +1 -1```, which is equal to ```1```. As there are no more "*", we finish processing, with the resulting float being ```1.0000```.

However, if we had:

```
* The pink panther
* The crazy gorilla
```

The float would instead be equal to ```-1 +2 +1 -1``` and ```-1 +1 -2 +2 +1```, which is equal to ```1``` and ```1```, and the resulting float would be ```1.1000```

Notes:

Current thoughts would limit key value pairs to singular key-value pairing instances, making systems like dicts impossible and cumbersome.

## Function Calls

Function Calls are a vital part of the system, as all comparisons are simple only, and can't do something such as:

```python
if something != (somethingElse - 1):
```

In-built functions, which stand as reserved words, take care of these small things for us.

### In-Built Functions

Accessed by key "fu"

print to stdin is represented by "pri"

### Global Invariables

Accessed by key "glo"

True
False

### Writing Functions

Accessed by key "fut"

## Hello World

The below program, is designed to print ```Hello, World!``` to the stdin.

```ProseLang
> Whi tru fu
* ... glo
* ... tru
* ... pri
* ... Hello,
* ... World!
* ... end
```
or more realistically:

```ProseLang
> Whipped truthfully further than he could bear, the man cried out:
* For glory!
* I trust not thy oppresors!
* My princess shall await me, for I will triumph.
* Hello, Hello, my dear poor fools. Your deaths will come, and come quickly upon you.
* Pitiful World! How it burns my soul.
* For Ender's soul, shall we fight.
```
