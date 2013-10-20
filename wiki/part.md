#this document is not up to date!


###addEvent()

Adds a midi event to the part.

```
#!javascript

// adds a single midi event
part.addEvent(event);

// adds 3 midi events to the part
part.addEvent(event, event, event);

// same as above
part.addEvent([event, event, event]);

```

If you add midi events to a part, by default the position of the midi event will be based on its `ticks` value. The part will be enlarged if the position of the newly added midi event extends the actual size of the part. This might result in overlapping parts.

There is an additional argument that you can use if you want to add midi events relatively. If the last argument of the arguments list is the boolean value true, the `ticks` value of the midi event will be interpreted as offset from the start of the part, instead as the offset from the start of the song.

```
#!javascript
// create a new NOTE_ON midi event at 480 ticks
var event = sequencer.createMidiEvent(480, sequencer.NOTE_ON, 60, 100);

// the position of the part is 120 ticks *)
part.getPosition(); //returns 120

// add the event, the position of the event is 480 ticks *)
part.addEvent();

// add the event relatively to the start of the part, the position of the event is now 120 + 480 = 600 ticks *)
part.addEvent(event, true);

```

*) calculated from the start of the song.


###addEvents()

Same as `addEvent()`. 


### copy()
Copies the part and all its events to a new part and return the new part. The name of the new part will be suffixed with '_copy'. You can set your own name by assigning it: `part.name = 'your_part_name';`

===========================================

should this be in part??

###copyTo()
Copies the part and adds it to the same track of the original part at the specified position and return the newly created part. If the part hasn't been added to a track, this method behaves like `copy()`.


### move(ticks)
If the part is added to a track: moves the part inside its track by the number of ticks provided. Both positive and negative values are accepted.

### moveTo()
If the part is added to a track: moves the part to the specified position. If the position exceeds the length of the track, the track will be enlarged.

You can provide the position in the same formats as [`setPosition()`](position).


========================================


### moveEvent(Event, ticks)
Moves the provided event(s) by the provided number of ticks. Both positive and negative values are accepted.

```
#!javascript
// moves a single event 120 ticks forward
part.moveEvent(event, 120);

// moves 3 events 120 ticks back; you can provide as many events as you like
part.moveEvent(event, event, event, -120);

// same as above
part.moveEvent([event, event, event], -120);

// moves all events before tick value 120 forward by 480 ticks
part.moveEvent(part.findEvent('ticks < 120'), 480);

```

### moveEvents(ticks)
Same as `moveEvent()` if you provide an argument, without arguments if moves all events inside the part by the provide number of ticks. Both positive and negative values are accepted.


### moveEventTo()
Moves event(s) to the specified position. 

You can provide a single event, any number of events or an array of events, just like you can with `moveEvent()` and `addEvent` (see above). 

You can provide the position in the same formats as [`setPosition()`](position).


### copyEvent()
Copies the specified event(s). You can provide a single event, any number of events or an array of events, just like you can with `moveEvent()` and `addEvent` (see above). You can also provide the event id(s) instead of the event(s).

If the last argument is a number, the provided event(s) will be copied the provided number of times.

The method returns an event if there is only one event copied, otherwise an array of events is returned.

```
#!javascript
// copies all sustain pedal events
part.copyEvent(part.findEvent('type = sequencer.CONTROL_CHANGE AND data1 = 64'));

// copies all event in bar 5, three times
part.copyEvent(part.findEvent('bar  5'), 5);
```

### copyEvents()
Same as `copyEvent()` if you provide arguments, without arguments it copies all events inside the part. Returns the copied event or an array containing all copied events.


### deleteEvent(Event)
Deletes the specified event(s). You can provide a single event, any number of events or an array of events, just like you can with `moveEvent()` and `addEvent` (see above). You can also provide the event id(s) instead of the event(s). 

Returns the deleted  event or an array containing all deleted events.


### deleteEvents(array)
Same as `deleteEvent()` if you provide arguments, without arguments it deletes all events inside the part. 

Returns the deleted event or an array containing all deleted events.


### transpose(semi | hertz)
Transposes all NOTE_ON and NOTE_OFF events and all audio events in this part. By default the argument is interpreted as semi tones but you can also transpose by a value in hertz. Both positive and negative values are supported.

```
#!javascript
// transpose all events up by an octave
part.transpose(12);

// transpose all events down by 2 semi tones
part.transpose(-2);

// same as above
part.transpose('semi', -2);

// transpose all events 40 Hertz
part.transpose('hertz', 20);

```

### transposeEvent()
Transposes the provided events. Transpose only has an effect on NOTE_ON and NOTE_OFF events, and on audio events.

You can provide a single event, any number of events or an array of events, just like you can with `moveEvent()` and `addEvent` (see above). 

Like `transpose` you can transpose both by semi tones and by hertz, and both positive and negative values are supported.


### transposeEvents()
Same as `transposeEvent()` when used with arguments, same as `transpose()` when used without arguments.

