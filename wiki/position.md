### sequencer.getPosition()

>related methods:  
>[song.getPosition()](song_position)

This method can be used in 2 ways. If you use it without arguments it returns a data object containing all information about the current position of the playhead in the sequencer. 

If you use it with arguments, it will behave like `[song.getPosition()](song_position)` and act upon the currently loaded song.


`millis` → time in milliseconds calculated from the start of the song  
`ticks` → time in ticks calculated from the start of the song  

`timeAsString` → position as a time string, for instance `1:03:30:099` for 1 hour, 3 minutes, 30 seconds and 99 milliseconds  		
`hour`  
`minute`  
`second`  
`millisecond`  
		
`barsAsString` → position as a bars and beats string, for instance `77:4:3:078` for bar 77, 4th beat, 3rd sixteenth and 78 ticks  
`bar` → number in bars zero based, so in the example above, the value of bar would be 76  
`beat` → beat zero based  
`sixteenth` → sixteenth zero based  
`tick` → tick is always zero based 

`bpm` → tempo in beats per minute (as float)  
`nominator` → nominator of the time measure  
`denominator` → denominator of the time measure  
		
`ticksPerBar` → number of ticks per bar, for instance if PPQ is 480 and the measure is 4/4, there are 4 * 480 = 1920 ticks in a bar  
`ticksPerBeat`  
`ticksPerSixteenth`  
		
`numSixteenth` → number of sixteenth per beat, if the beat is a quarter note like in a 4/4 measure, the beat has 4 sixteenths but if the beat is an eighth note, like in a 3/8 measure, the beat has only 2 sixteenths.  

`millisPerTick` → duration of a tick in millis, for instance measure is 4/4, PPQ is 480 and bpm is 120 the duration of a tick is (60 / 120 / 480) * 1000  = 1.041667 millisecond  
`secondsPerTick`  


### sequencer.setPosition()

Sets the position of the playhead in the sequencer. The first argument is usually the format in which you provide the position and the rest of the arguments describe the position in that format. If you don't provide a position format the format will default to barsandbeats.

`barsandbeats` → specify position in bar, beat, sixteenth and tick  
`barsbeats` → same a above  
`time` → specify position in hour, minute, second and millisecond  
`ticks` → specify position in ticks from the start of the song  
`millis` → specify position in milliseconds from the start of the song  


#### examples:
```
#!javascript
// move playhead to bar 5, 2nd beat, 1st sixteenth and 67 ticks
sequencer.setPosition(5,2,1,67);

// same as above
sequencer.setPosition([5,2,1,67]);

// same as above
sequencer.setPosition('5,2,1,67');

// same as above
sequencer.setPosition('barsbeats','5,2,1,67');

// same as above
sequencer.setPosition('barsandbeats','5,2,1,67');

```

```
#!javascript
// move playhead to the start of bar 5: 1st beat, 1st sixteenth 0 ticks
sequencer.setPosition(5,1,1,0);

// same as above
sequencer.setPosition(5);

```

```
#!javascript

// move playhead to 15360 ticks from start
sequencer.setPosition('ticks', 15360);

// move playhead to 26855 milliseconds  from start
sequencer.setPosition('millis', 26855);

// move playhead to 0 hours, 2 minutes, 18 seconds and 879 milliseconds
sequencer.setPosition('time', 0, 2, 18, 879);

```

```
#!javascript
// move playhead to 0 hours, 2 minutes, 0 seconds and 0 milliseconds
sequencer.setPosition('time', 0, 2, 0, 0);

// same as above
sequencer.setPosition('time', 2);

```
