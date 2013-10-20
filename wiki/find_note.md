### sequencer.findNote(searchstring)

>related methods:  
>[sequencer.findEvent()](find_event)


You can perform search actions on a song, a track or a plain array of events.


```
#!javascript

song.findNote('noteNumber > 60');

track.findNote('noteName > D#4 OR noteName < F5');
	
sequencer.findNote(array, 'noteName > D#4 AND velocity > 100 < 127 OR bar < 10');

```

Works the same as [sequencer.findEvent()](find event), the only difference is that it returns notes instead of events. A note is basically a note on midi event that has some extra properties:

`endEvent` → the matching note off event  
`durationSeconds` → difference in seconds between the position of the note of and the note on event  
`durationMillis` → difference in millis between the position of the note of and the note on event  
`durationTicks` → difference in ticks between the position of the note of and the note on event  
`endTicks` → tick position of the note off event  
`endMillis` → millis of the note off event  
  
This method is particularly handy for searching inside a certain time span, for instance a bar. The search action will only return the notes that have both the note on and the note off event inside the given time span.