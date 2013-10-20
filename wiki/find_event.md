### sequencer.findEvent(searchstring)

>related methods:  
>[sequencer.findNote()](find_note)

You can perform search actions on a song, a track or a plain array of events.


```
#!javascript

song.findEvent('noteNumber > 60');

track.findEvent('noteName > D#4 OR noteName < F5');
	
sequencer.findEvent(array, 'noteName > D#4 AND velocity > 100 < 127 OR bar < 10');

```
The search string can be a single condition or a number of conditions chained by logical operators.
   
  
### search operators:

`=` → equal  
`==` → equal  
`===` → equal  
`>` → greater then  
`<` → less then  
`>=` → greater then or equal  
`<=` → less then or equal  
`^=` → starts with (strings)  
`$=` → ends with (strings)  
`*=` → contains    
`!=` → does not contain (strings) or not equal (numbers)  
`!==` → does not contain (strings) or not equal (numbers)  
`%=` → modulo, see below for an example (numbers)  
`~=` → contains surrounded by white spaces (currently not in use)  
  
  
All equal and non equal operators are strict!  
  
  
### logical operators:  

`OR` → adds the result of the condition after the OR operator to the result of all conditions before the OR condition  
`XOR` → same as OR but filters out the events that exist in both result sets  
`AND` → applies the condition followed by the AND on the result of all conditions before the AND operator  
`NOT` → the inverse of AND  

It is not (yet) possible to use parentheses to group logical expressions. See advanced examples. 
  
   
### search properties:  

`id` → the unique event id that is assigned when the midi event was created  
`type` → midi event type  
`data1` → midi event data 1  
`data2` → midi event data 2  
`noteNumber` → same as data 1 in case of a note on or note off event  
`velocity` → same as data 2 in case of a note on or note off event  
`noteName` → name of note based on note name mode (sharp, flat, enharmonic-sharp, enharmonic-flat)  
`frequency` → frequency of note based on the current [pitch setting](note)  
  
`ticks` → position from start in ticks (eternal ticks)  
`millis` → position from start in milliseconds  
  
`barsbeats` → position of the event in bars and beats, e.g. [1,2,1,30] → bar 1, beat 2, sixteenth 1, tick 30  
`bar`  
`beat`  
`sixteenth`  
`tick`  
  
`time` → position of the event in time, e.g. [0,3,25,999] → hour 0, minute 30, second 25, millisecond 999  
`hour`  
`minute`  
`second`  
`millisecond`  
  
  
### examples:

`findEvent('noteName ^= C')` → finds all C, C# and Cb notes in all octaves  
`findEvent('noteName *= #')` → finds sharp notes in all octaves  
`findEvent('noteName $= 5')` → finds all notes in octave 5  
`findEvent('noteName = C')` → finds all C notes in all octaves 
   
`findEvent('noteName > C4')` → finds all notes higher then C4  
`findEvent('noteNumber > 60')` → finds all notes higher then note number 60, same as above  
  
`findEvent('noteName >= C4')` → finds all notes higher or equal then C4  
`findEvent('noteNumber >= 60')` → same as above with note numbers  

`findEvent('noteName > C4 < D5')` → finds all notes between C4 and D5  
`findEvent('noteNumber > 60 < 74')` → same as above with note numbers  
  
`findEvent('noteName >= C4 <= D5')` → finds all notes between and including C4 and D5  
`findEvent('noteNumber >= 60 <= 74')` → same as above with note numbers  
  
`findEvent('velocity >= 60 < 127')` → finds all notes with a velocity greater then or equal to 60 and less then 127  
    
`findEvent('bar = 3')` → finds all events in bar 3  
`findEvent('bar > 3')` → finds all events from bar 3 (not including bar 3)  
  
`findEvent('bar *= 3')` → finds all events in bars with a number that contains a 3, e.g. 131, 203, 32  
`findEvent('bar %= 4')` → finds all events in bars where (barnumber % 4) is 0, i.e. bar 4, 8, 12 and so on  
  
`findEvent('beat = 2')` → finds all events on beat 2 (in all bars)  
`findEvent('beat %= 2')` → finds all events on beat 2 (in all bars)  
  
`findEvent('barsbeats = [1,3,2,60]')` → finds all events on bar 1, beat 2, sixteenth 2 and tick 60  
`findEvent('barsbeats = 1,3,2,60')` → same as above  
  
`findEvent('barsbeats = [3]')` → finds all events on bar 3, beat 1, sixteenth 1 and tick 0  
`findEvent('barsbeats = 3')` → same as above  
  
Please note that the 2 examples above are *not* the same as `findEvent('bar = 3)`; they will return less results because the pattern only matches events on position 3,1,1,0!     
  
`findEvent('time > [0,3,34,899]')` → finds all events from time position 3 minutes, 30 seconds and 899 milliseconds   
`findEvent('second = 30')` → finds all events on time position 30 seconds  
`findEvent('time = 30')` → same as above: if no position array is supplied the argument will be interpreted as seconds, i.e. [0,argument,0,0] 
`findEvent('time = [0,30]')` → same as above   
`findEvent('time = [0,30,0]')` → same as above   
`findEvent('time = [0,30,0,0]')` → same as above   
`findEvent('time = 0,30,0,0')` → same as above   
`findEvent('time = [30]')` → finds all events on time position 30 hours (!!), 0 minutes, 0 seconds and 0 milliseconds  
  
`findEvent('type = PROGRAM_CHANGE')` → finds all program change events    
`findEvent('type = 0xC0')` → same as above  
`findEvent('type = 192')` → same as above  
`findEvent('type = ' + sequencer.PROGRAM_CHANGE)` → same as above  

`findEvent(song, 'type = CONTROL_CHANGE AND data1 = 64')`→ finds all damper pedal events  
`findEvent(song, 'type = CONTROL_CHANGE AND data1 = 64 AND data2 = 0')`→ finds all damper pedal off events  
  
### advanced examples:

`findEvent('noteName = C OR velocity < 100')` → all events that match pattern 1 plus all events that match pattern 2  
`findEvent('noteName = C OR velocity < 100')` → same as above  
    
`findEvent('noteName = C AND velocity < 100')` → all event that match both pattern 1 and pattern 2  
`findEvent('noteName = C NOT velocity < 100')` → inverse of above  
`findEvent('noteName = C AND velocity >= 100')` → same as above  

`findEvent('velocity > 60 < 66 OR noteName = B4')` → finds all events that have a velocity between 61 and 65 and all events that have the noteName B4  
`findEvent('velocity > 60 < 66 XOR noteName = B4')` → finds all events that have a velocity between 61 and 65 and all events that have the noteName B4, but not the events that have both noteName B4 and a velocity between 61 and 65  
   
`findEvent('noteName ^= C AND noteName != # AND noteName != b')` → finds all C notes in all octaves, same as:   
`findEvent('noteName = C')` 

`findEvent('velocity > 60 XOR noteName = B4 AND beat = 2')` → finds all events on the second beat of a bar but not the events that have a velocity value of more then 60 and a note name B4. This clearly shows that the condition after the AND operator has filtered the results of the 2 conditions before the AND operator.
  
You may have thought that the result would have been:  
 - all events with a velocity value greater then 60  
 - all events with note name B4 on the second beat of a bar  
 - minus the events that are common in both result sets  
  
To get this result we need to use parantheses like so:  
`findEvent('velocity > 60 XOR (noteName = B4 AND beat = 2)')`  
  
But the use of parentheses is not yet supported, but you can get the same result by using the method `sequencer.removeMutualEvents()`

```
#!javascript
var events = song.getEvents(),	// the array of events that you want to search in
	resultSet1,
	resultSet2,
	result;

resultSet1 = sequencer.findEvent(events, 'noteName = B4 AND beat = 2');
resultSet2 = sequencer.findEvent(events, 'velocity > 60');

result = sequencer.removeMutualEvents(resultSet1, resutlSet2);

// or in one line:

result = sequencer.removeMutualEvents(
	sequencer.findEvent(events, 'noteName = B4 AND beat = 2'),
	sequencer.findEvent(events, 'velocity > 60')
);

```



You might have noticed that for instance:   
`findEvent('velocity > 60 < 100')`   
is actually a shorthand for:      
`findEvent('velocity > 60 AND velocity < 100')`  



Also you rewrite:    
`result = findEvent(events, 'noteName = B4 AND beat = 2')`    
like so:  
```
#!javascript
var events = song.getEvents(),	// the array of events that you want to search in
	resultSet,
	result;

resultSet = sequencer.findEvent(events, 'noteName = B4');

result = findEvent(resultSet, 'beat = 2');

//or with nested findEvent calls like so:

result = findEvent(findEvent(events, 'noteName = B4'), 'beat = 2');

```   
