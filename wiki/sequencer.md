### load()  
>defined in [load_midi_file.js][load_midi_file]

Loads a midi file and creates a heartbeat song of it. Tempo and time signature events are all added to a tempo track. If the midi file does not contain any tempo or time signature events, the tempo track will default to a tempo of 120 bpm and a 4/4 time signature.

The PPQ value of the midi file is used in the heartbeat song. If the midi file doesn't have a PPQ value, the PPQ will default to 480. 

### play() 
>defined in [heartbeat.js][heartbeat]

Starts playing the currently loaded song at the current position of the playhead.

### pause() 
>defined in [heartbeat.js][heartbeat]

Stops playing and leaves the playhead at the current position. Sequential calls to pause() result in toggling between playing and pausing. 

### stop() 
>defined in [heartbeat.js][heartbeat]

Stops playing and set the playhead to the start position of the song.

### isPlaying() 
>defined in [heartbeat.js][heartbeat]

Returns true if the song is playing, else false.

### isPaused() 
>defined in [heartbeat.js][heartbeat]

Returns true if the song is paused, else false.


### getPosition() 
>defined in [heartbeat.js][heartbeat]

See [getPosition()](position).


### setPosition() 
>defined in [heartbeat.js][heartbeat]

See [setPosition()](position).


### getPositionFromGrid(song, x, y, width, height)
>defined in [song_grid.js][song_grid]  

Returns the position data as described at [sequencer.getPosition()](position) based on a coordinate `x`,`y` on an area with dimensions `width` and `height`. You can use this method for instance to map the user's mouseclicks to positions in the loaded song.


### findEvent() 
>defined in [find_event.js][find_event]  

See [findEvent()](find_event).

### findNote() 
>defined in [find_note.js][find_note]  

See [findNote()](find_note).

### addEventListener(eventType, data, callback)
>defined in [follow_event.js][follow_event]  

See [followEvent()](follow_event).

### getStats(searchstring)
>defined in [event_statistics.js][event_statistics]  

See [getStats()](event_statistics).


### getNote(param1, [param2, noteNameMode])
>defined in [note.js][note]  

See [getNote()](note).


### getNoteNumber(param1, [param2, noteNameMode])
>defined in [note.js][note]  

See [getNote()](note).


### getNoteOctave(param1, [param2, noteNameMode])
>defined in [note.js][note]  

See [getNote()](note).


### getFullNoteName(param1, [param2, noteNameMode])
>defined in [note.js][note]  

See [getNote()](note).


### getNoteFrequency(param1, [param2, noteNameMode])
>defined in [note.js][note]  

See [getNote()](note).


### getSong() 
>defined in [heartbeat.js][heartbeat]

Returns the currently loaded song. If you haven't loaded a song or a midi file, the default empty song is returned. You can start adding tracks, parts and so on right away.

See [song](song.md).


### createSong(config)
>defined in [song.js][song]    

Creates an empty song. The configuration object may be omitted: 

```
#!javascript

song.bpm = config.bpm || 120;
song.ppq = config.ppq || 480;
song.nominator = config.nominator || 4;
song.denominator = config.denominator || 4;	

```

### createTrack()  
>defined in [track.js][track]  

Returns a new track with no events. 

See [track](track.md).


### createPart()   
>defined in [part.js][part]  

Returns a new part with no events. 

See [part](part.md).


### createMidiEvent(ticks, type, data1, data2)   
>defined in [midi_event.js][midi_event]  

Returns a new midi event. 


### addInstrument()  
>defined in [instrument_manager.js][instrument_manager]

See [instruments](instruments)
 
### loadInstrument()  
>defined in [instrument_manager.js][instrument_manager]

See [instruments](instruments)


### loadBank()  
>defined in [instrument_manager.js][instrument_manager]

See [instruments](instruments)


### useBank()  
>defined in [instrument_manager.js][instrument_manager]

See [instruments](instruments)


### addSamples()  
>defined in [instrument_manager.js][instrument_manager]

See [instruments](instruments)



[audio_event]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/audio_event.js?at=master  "audio_event"

[close_module]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/close_module.js?at=master  "close_module"

[event_statistics]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/event_statistics.js?at=master  "event_statistics"

[find_event]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/find_event.js?at=master  "find_event"

[get_position]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/get_position.js?at=master  "get_position"

[follow_event]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/follow_event.js?at=master  "follow_event"

[heartbeat]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/heartbeat.js?at=master  "heartbeat"

[instrument]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/instrument.js?at=master  "instrument"

[instrument_manager]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/instrument_manager.js?at=master  "instrument_manager"

[load_midi_file]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/load_midi_file.js?at=master  "load_midi_file"

[locators]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/locators.js?at=master  "locators"

[metronome]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/metronome.js?at=master  "metronome"

[midi_event]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/midi_event.js?at=master  "midi_event"

[midi_event_listener]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/midi_event_listener.js?at=master  "midi_event_listener"

[midi_event_names]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/midi_event_names.js?at=master  "midi_event_names"

[midi_note]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/midi_note.js?at=master  "midi_note"

[find_note]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/find_note.js?at=master  "find_note"

[find_event]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/find_event.js?at=master  "find_event"

[note]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/note.js?at=master  "note"

[open_module]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/open_module.js?at=master  "open_module"

[parse_midi_events]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/parse_midi_events.js?at=master  "parse_midi_events"

[parse_time_events]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/parse_time_events.js?at=master  "parse_time_events"

[part]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/part.js?at=master  "part"

[process_events]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/process_events.js?at=master  "process_events"

[scheduler]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/scheduler.js?at=master  "scheduler"

[song]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/song.js?at=master  "song"

[song_grid]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/song_grid.js?at=master  "song_grid"

[track]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/track.js?at=master  "track"

[util]: https://bitbucket.org/abudaan/heartbeat/src/71c9b55bb685506bb13eb8fe048165078bdbfa6c/src/heartbeat/util.js?at=master  "util"

