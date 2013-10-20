### sequencer.getStats(searchstring)

>related methods:  
>[sequencer.findEvent()](find event)  
>[sequencer.findNote()](find note)

You can get statistics of the events in a song, in a track or in a plain array of events.


```
#!javascript
// run statistics on a song
song.getStats('noteNumber max');

// run statistics on a track
track.getStats('velocity min noteName > D#4 < F5');
	
// run statistics on an array of events
sequencer.getStats(array, 'data2 avg type = CONTROL_CHANGE AND bar < 10');

```
The search string consists of three parts: 

1) The event property that you want to run the statistics on, this can be any of the following:  

`data1`  
`data2`   
`velocity`   
`noteNumber`   
`noteName`   
`frequency`  

2) The type of statistics that you want to run:

`min` → the minimum value  
`max` → the maximum value    
`avg` → the average value     
`all` → runs all above statistics   

3) A searchstring that filters events from the provided events, this is a search string as described at [sequencer.findEvent()](find event) 

The getStats method returns a single value when used with `min`, `max` or `avg`, and an object containing keys for all values when used with `all`, for instance:

```
#!javascript
// get all stats of the velocity values of NOTE_ON events
var stats = song.getStats('velocity all type = NOTE_ON');

console.log(stats.min); // prints 60
console.log(stats.max); // prints 99
console.log(stats.avg); // prints 76.42112986060161
```

Note that the average is not simply (60 + 99)/2 = 79.5. The average is a weighted average that takes into account how many notes have a certain velocity value.

If you perform statistics on non-numeric values such as note names, the returned values will be in the same format, for instance:  

```
#!javascript
// get the average note name on afterbeats between bar 3 and 40
var averageNote = song.getStats('noteName avg bar >= 3 < 40 AND beat % 2');
console.log(averageNote); // prints F#3
```

