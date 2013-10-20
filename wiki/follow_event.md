### addEventListener(eventType, data, callback)
>methods:  
>sequencer.addEventListener();  
>sequencer.removeEventListener();  
>sequencer.startFollowEvent();  
>sequencer.stopFollowEvent();  

The first argument specifies the type of event that you want to listen for. There are 3 main types of event: `event`, `note` and `position`. 

Type `note` adds basically 2 event listeners in one go: one for the NOTE_ON event and one for the NOTE_OFF event. 

The data argument can be a midi event, an array of midi events or a condition, like for instance `bar = 3`.

Apart from the above mentioned types of events, you can also add listeners to transport events. You don't need to provide a data argument for transport events.

The callback argument is the function that gets called when the playhead passes the event or the position that the listener was added to. If you have added a listener to an event, that event will be passed as argument to the callback function. Likewise if you have added a listener to a position, that position will be the argument.

The update interval of the event listeners is limited by the frame rate of requestAnimationFrame(). The frame rate of requestAnimationFrame is in its turn limited by the refresh rate of your monitor. 

Since most screens have a refresh rate of 60Hz, the update interval of the event listeners is 1000/60 = 16.7 ms. This has an impact on when the callbacks are called:

If you add an event listener, the callback will be called as soon as the playhead reaches the position, or the event that the event listener is added to, or in the first update cycle after that situation. This means that there can be a delay of 16.7 ms or more before the callback method gets called.

The method addEventListener returns a listener id that you can use to remove the listener again:

```
#!javascript
var id = sequencer.addEventListener('play', callback);

sequencer.removeEventListener(id);
```




### add an event listener to a transport event
```
#!javascript
sequencer.addEventListener('play', callback);

sequencer.addEventListener('pause', callback);

sequencer.addEventListener('stop', callback);

// listener for the end of the song
sequencer.addEventListener('end', callback);

```



### add an event listener to an event or a note

```
#!javascript
// add event listener to a single event
sequencer.addEventListener('event', midiEvent, callback);

// add event listener to multiple events
sequencer.addEventListener('event', [midiEvent,midiEvent,midiEvent], callback);

// or with findEvent()
sequencer.addEventListener('event', sequencer.findEvent('noteName = B4 AND velocity > 40 < 80'), callback);

// or with a search string
sequencer.addEventListener('event', 'noteName = B4 AND velocity > 40 < 80', callback);

// add event listener to a note, so to the NOTE_ON and the NOTE_OFF event
sequencer.addEventListener('note', midiEvent,callback);

// add event listener to several notes
sequencer.addEventListener('note', sequencer.findEvent('velocity = 100'), callback);

// add event listener to several notes in a bar
sequencer.addEventListener('note', sequencer.findNote('bar = 45'), callback);

```

As you can see you can provide both a single midi event and an array of midi events for the data argument. Note that for event type `note` you can both provide events and notes for the data argument, see also [findNote()](find_note).

Instead of midi events you can also provide a search string as you would use in [findEvent()](find_event).


### add an event listener to a position

If you want to add event listeners of the type `position` you have to provide a search string for the data argument. This is the same kind of search string you use in [findEvent()](find_event).

As mentioned above there are two modes of event type `position`, namely bars and beats and time. The latter is the regular time format in hours, minutes, seconds and milliseconds, and the former is described in bars, beats, sixteenth and ticks.

There are also 2 subtypes: one-shot and repetitive position events. One-shot events fire only at a specific position and repetitive events fire every time a certain condition in the position is met, for instance every at every first beat.


**one-shot events**   
You can use one of the following search parameters:  

`barsbeats` → in combination with a position in bars, beats, sixteenths and ticks, or a number  
`barsandbeats` → same as above  
`time` → in combination with a position in hours, minutes, seconds and milliseconds, or a number  
`ticks` → number  
`millis`→ number  

You can only use the equal operators: `=`,`==` or `===`. These will all be interpreted strictly.  

**repetitive events**   
You can use one of the following search parameters:  

`bar`  
`beat`  
`sixteenth`  
`hour`  
`minute`  
`second`  

You can use these operators: 

`=`  
`==`  
`===`  
`!=`  
`!==`  
`%=`  
`>`  
`>=`  
`<`  
`<=`  

You can also use the search parameter without condition; in this case the callback will be called on every subsequent time unit. For instance on every beat, see examples below.



### examples

**midi events**  
You can use any search string that is supported by [findEvent()](find_event).

```
#!javascript

// listen for all NOTE_OFF events
addEventListener('event', 'type = NOTE_OFF', callback) ; 

// listen for all sustain pedal on events, very useful if you want to add a pedal animation 
addEventListener('event', 'type = CONTROL_CHANGE AND data1 = 64 AND data2 = 1', callback) ; 

```


**positions in bars and beats (one-shot)**  
```
#!javascript

// callback at the start of bar 5
addEventListener('position', 'barsandbeats = 5,1,1,0', callback)  

// same as above
addEventListener('position', 'barsandbeats = [5,1,1,0]', callback)  

// same as above
addEventListener('position', 'barsbeats = [5,1,1,0]', callback)  

// same as above
addEventListener('position', 'barsandbeats = 5', callback)  

```


**positions in time (one-shot)**  
```
#!javascript

// callback after 1 hour, 2 minutes, 30 seconds and 450 milliseconds
addEventListener('position', 'time = [1,2,30,450]', callback)  

// callback after 3 minutes
addEventListener('position', 'time = 0,3,0,0', callback)

// same as above
addEventListener('position', 'time = 3', callback)

```


**positions in ticks or millis (one-shot)**
```
#!javascript

// callback on number of ticks from start of song
addEventListener('position', 'ticks = 99360', callback)  

// callback on number of milliseconds from start of song
addEventListener('position', 'millis = 65740', callback)  

```


**position in bars and beats without condition (repetitive)**  
```
#!javascript

// callback on every a bar
addEventListener('position', 'bar', callback);

// callback on every a beat
addEventListener('position', 'beat', callback);

// callback on every a sixteenth
addEventListener('position', 'sixteenth', callback);

// not supported because the update interval is too coarse → see above
addEventListener('position', 'tick', callback);
```



**position in time without condition (repetitive)**  
```
#!javascript

// callback on every hour
addEventListener('position', 'hour', callback);

// callback on every a minute
addEventListener('position', 'minute', callback);

// callback on every a second
addEventListener('position', 'second', callback);

// not supported because the update interval is too coarse → see above
addEventListener('position', 'millis', callback);

```


**position in bars and beats with assignment condition (repetitive)**
```
#!javascript

// note that this is not a repetitive event because there is only one third bar 
addEventListener('position', 'bar = 3', callback);

// callback on every third beat in a bar
addEventListener('position', 'beat = 3', callback);


// callback on every third sixteenth in a bar
addEventListener('position', 'sixteenth = 3', callback);

// not supported because the update interval is too coarse → see above
addEventListener('position', 'tick = 3', callback);

```



**position time with assignment condition (repetitive)**  
```
#!javascript

// note that this is not a repetitive event → callback is called once after 3 hours
addEventListener('position', 'hour = 3', callback); 

// callback on 1 hour and 3 minutes, 2 hours and 3 minutes, and so on
addEventListener('position', 'minute = 3', callback); 

// callback every time second has value 3, i.e. when position is 1 minute and 3 seconds, 2 minute and 3 seconds, and so on
addEventListener('position', 'second = 3', callback);


// not supported because the update interval is too coarse → see above
addEventListener('position', 'millis = 3', callback);


```


**position with condition (repetitive)**    
```
#!javascript

// callback on every second between second 2 and second 10
addEventListener('position', 'second > 2 < 10', callback);  

// beginning in bar 6, callback gets called on every new bar
addEventListener('position', 'bar > 5', callback); 

// beginning in bar 6, callback gets called on every event 
addEventListener('event', 'bar > 5', callback);  

// callback gets called on every event in bar 5
addEventListener('event', 'bar = 5', callback);  

// callback gets called on every note in bar 5 → a note is considered to be inside a bar if it both starts and ends in that bar
addEventListener('note', 'bar = 5', callback);  

// callback gets called on every after beat (in a 4/4 measure)
addEventListener('position', 'beat % 2', callback); 

```


**not yet supported conditions**  
Compound conditions with `AND`,`OR`,`NOT` and `XOR` are not yet supported
```
#!javascript

// callback gets called on the second beat in every other bar
addEventListener('position', 'bar %= 2 AND beat = 2', callback);  

// in bar 5 to 10, callback gets called on the second beat
addEventListener('position', 'bar >= 5 < 10 AND beat = 2', callback);  


```
