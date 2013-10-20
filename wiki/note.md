##getNote(parameter1, [parameter2, noteNameMode])
>related methods:  
>sequencer.getNoteName();  
>sequencer.getNoteOctave();  
>sequencer.getFullNoteName();  
>sequencer.getFrequency();  

Note is basically a data container that has the following properties:  
  
`name` → the name of the note, a letter from A to G  
`octave` → the octave, a number from -1 to 9  
`fullName` → the name and the octave, e.g. C4 for central C  
`number` → the midi note number  
`frequency` → the frequency of the note 
  
###standards:
The naming of the note is according to the [scientific pitch notation](http://en.wikipedia.org/wiki/Scientific_pitch_notation), and the numbering and the frequency of the notes follows the [Midi Tuning Standard](http://en.wikipedia.org/wiki/MIDI_Tuning_Standard). The frequency is based on the pitch set for A4; the standard pitch is 440 Hz but you can change it by setting the value `sequencer.pitch`. The [central C](http://en.wikipedia.org/wiki/Middle_C) is C4 and has with A4 = 440 Hz a frequency of 261.626 Hz.

###usage:
You can create a note by calling `sequencer.getNote()` in one of the following ways:  
  
  
`getNote(noteNumber)`  
`getNote(noteNumber, noteNameMode)`  
  
`getNote(noteName)` → actually this is wrong because no value for octave is given; octave will default to 0  
`getNote(noteName, noteNameMode)`  
    
`getNote(fullNoteName)`  
`getNote(fullNoteName, noteNameMode)`  
    
`getNote(noteName, octave)`  
`getNote(noteName, octave, noteNameMode)`    
  
  
All methods return a note object where all the above mentioned properties have the correct value. For instance if you want to know the note number of C#3 you could do this:    
  
`console.log(sequencer.getNote('C#3').number);`  
    
But there are also special methods for getting a property of a note based on another property:  
  
`getNoteName()`   
`getNoteOctave()`   
`getFullNoteName()`   
`getNoteNumber()`   
`getFrequency()`  
  
These methods can be called with the same parameters as `getNote()`. For instance:  
  
`getNoteOctave(0)` → returns -1 because 0 is interpreted as the note number which is the note C-1.  

###note name mode:

There are 4 note name modes that you can chose from:  
  
`sharp` →  C, C#, D, D#, E, F, F#, G, G#, A, A#, B  
`flat` →  C, Db, D, Eb, E, F, Gb, G, Ab, A, Bb, B  
`enharmonic-sharp` → B#, C#, C##, D#, D##, E#, F#, F##, G#, G##, A#, A##  
`enharmonic-flat` → Dbb, Db, Ebb, Eb, Fb, Gbb, Gb, Abb, Ab, Bbb, Bb, Cb  
  
The default note name mode is `sharp`.  
  
In the near feature scales will be added to place the use of accidentals within a more or less harmonic context:  
  
`D-major` → D, E, F#, G, A, B, C# and for chromatic notes the accidental # will be used: D#, E#, G#, A#, B#
  
This isn't of course a very musical harmonic context; for instance IV moll-dur in D is G, Bb, D and not G, A#, D.


  
##examples:

`getFullNoteName('C#3', 'flat')` → returns Db3  
`getFullNoteName('C#', 3, 'flat')` → same as above  
`getFullNoteName('C#', '3', 'flat')` → same as above  
    
`getNoteName('Bb', 'sharp')` → returns A#  
`getNoteName('C', 'enharmonic-sharp')` → returns B#  
`getNoteName('C', 'enharmonic-flat')` → returns Dbb  
  
`getNoteOctave(60)` → returns 4  
  
`getFrequency('A4')` → returns 440  
`getFrequency('C4')` → returns 261.626  

`sequencer.pitch = 432` → Verdi tuning  
`getFrequency('A4')` → returns 432  
`getFrequency('C4')` → returns 256.869  
  
`getNote(102)` → returns {name: "F#", octave: 7, fullName: "F#7", number: 102, frequency: 2959.955}  
`getNote(102, 'flat')` → returns {name: "Gb", octave: 7, fullName: "Gb7", number: 102, frequency: 2959.955}  
  
`getNote('E7')` → returns {name: "E", octave: 7, fullName: "E7", number: 100, frequency: 2637.020}  
`getNote('e7')` → same as above  
`getNote('E', 7)` → same as above  
`getNote('E', '7')` → same as above  
`getNote('E', '7', 'sharp')` → same as above  
