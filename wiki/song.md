### addTrack(Track)   

Adds a track to a song. You can create a track by `sequencer.createTrack()` or `Track.copy()`, see [track](track.md).


### removeTrack(index)   

Removes the track with the specified index.


### getTrack(index)

Returns the track at the specified index.


### getTracks()

Returns the array that contains all tracks.


### deleteTracks()

Removes and deletes all tracks, you will be left with a song without any tracks or data. 


### getTrackCount()   

Returns the number of tracks of the currently loaded song. You can also query the number of tracks directly on a song: `song.numTracks`.


### getEvents()

Returns an array containing all midi events in all tracks of the song. All events will be in the correct chronological order.


### getTimeEvents()

Returns an array containing all TEMPO and TIME_SIGNATURE events.
	
### addTimeEvents()

Add TEMPO and/or TIME_SIGNATURE events to the timeEvents array of the song. Other types of midi events will be ignored.
	
```
#!javascript
// add a single time event
sequencer.addTimeEvents(timeEvent);

// add multiple time events
sequencer.addTimeEvents(timeEvent, timeEvent, timeEvent);

// add multiple time events as array
sequencer.addTimeEvents([timeEvent, timeEvent, timeEvent]);

```

### addTimeEvent(timeEvent)

Adds the TEMPO or TIME_SIGNATURE event to the timeEvents array of the song. Other types of midi events will be ignored.

### update()

Forces the song to update all events. It shouldn't be necessary to call this method from your code; all changes in events, parts and tracks in the song are automatically propagated.


### getPositionFromGrid(x, y, width, height)

>related methods:  
>[sequencer.getPositionFromGrid()](sequencer)

Returns the position data as described at [sequencer.getPosition()](position) based on a coordinate `x`,`y` on an area with dimensions `width` and `height`.


### getPosition()

>related methods:  
>[sequencer.getPosition()](position)  
>[sequencer.setPosition()](position)  

This method can be used to query the position data on a specific position in the song. You can use this for instance if you want to know the bar and beat at a certain position in ticks.

The returned position data object is described in detail at [sequencer.getPosition()](position).

This method is overloaded and you can call this method in the same ways as you [sequencer.setPosition()](position).


### findEvent()

see [findEvent()](find_event.md)
	

### findNote()

see [findNote()](find_note.md)


### getStats()

see [getStats()](event_statistics.md)









