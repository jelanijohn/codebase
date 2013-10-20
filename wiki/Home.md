# heartbeat.js


[**sequencer**](sequencer) global variable that contains all sequencer related methods.

[**song**](song) object with song related methods. 

By calling `sequencer.getSong()` you get a reference to the song that is currently loaded in the sequencer. If you haven't loaded a song yourself, the default empty song will be returned.

By calling `sequencer.createSong()` you get a new song that is not loaded in the sequencer. 

[**track**](track) object with track related methods.
```
#!javascript

// create new empty track
sequencer.createTrack();

// get an existing track from a song
song.getTrack(index | id | name);

// get an array containing all tracks from a song
song.getTracks();
```

[**part**](part) object with part related methods.

```
#!javascript

// create new empty part
sequencer.createPart();

// get an existing part from a track
track.getPart(index | id | name);

// get an array containing all parts from a track
track.getParts();
```
