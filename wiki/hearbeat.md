### createSong(config)

Creates an empty song. The configuration object may be omitted: 

```
#!javascript

song.bpm = config.bpm || 120;
song.ppq = config.ppq || 480;
song.nominator = config.nominator || 4;
song.denominator = config.denominator || 4;	

```
