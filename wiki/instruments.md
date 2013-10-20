### Using instruments in heartbeat   
>related methods:  
>addInstrument()  
>loadInstrument()  
>loadBank()  
>useBank()  
>addSamples()   

Instruments are considered not to be part of heartbeat. In other words: heartbeat doesn't come with any instruments so you have to provide them yourself in your project. Heartbeat does have the tools and methods to make it very easy for you to create and add your own instruments.
  
An instrument is basically a mapping of midi note numbers to samples. Samples can be separate audio files in any format that Chrome supports, see [this list](https://developer.mozilla.org/en-US/docs/HTML/Supported_media_formats). 

To save loading time, it is also possible to convert all samples to base64 format and store them in a single javascript file. You can add base64 encoded samples to heartbeat by using the method `sequencer.addSamples()`.

Instruments can be single- and multi-layered. Single-layered means that you have only one sample per midi note number and that the playback volume of the sample is dependent on the velocity value.

Multi-layered means that you provide samples per velocity range; for instance one sample for velocity range 0 to 40, one for 41 to 80 and one for velocity values from 81 to 127. Based on the velocity value of the midi note, the right sample will be played. 

The mapping of midi note number to samples is stored in an object:

```
#!javascript

var myInstrument = {
	name: 'my_instrument',
	bank: 'my_bank',
	url: 'my_samples/my_instrument',
	extension: 'ogg',
	mapping: {
		21: 'my_sample_A0',
		22: 'my_sample_Bb0', 
		23: 'my_sample_B0', 
		24: 'my_sample_C1', 

		...
		
		107: 'my_sample_B7', 
		108: 'my_sample_C8'
	}
};

// add the instrument to heartbeat's instrument storage 
sequencer.addInstrument(myInstrument);
```

`name` → The name of the instrument, this doesn't have to be an unique name, as long as the combination of bank name and instrument name is unique  
`bank` → The name of the bank that this instrument will be added to, if you omit this, the instrument will be added to the default bank  
`url` → The base url of the samples if you load the samples from separate audio files, or the path to the base64 encoded data in heartbeat's sample storage object, see `addSamples()` below  
`extension` → The extension of the samples, only needed if you load the samples from separate audio files  
`mapping` → Object that maps midi note numbers to sample names, the mapping doesn't have to be in numeric order, doesn't have to be successive, and also you don't have to provide samples for the full range of note numbers (midi note number 0 to midi note number 127). The name of the sample can either be the file name of the sample or the key in heartbeat's sample storage object, see `addSamples()` below.


### addInstrument()  

After you have created the mapping object, you can add the instrument to heartbeat's instrument and bank storage. This does not load the samples of the instrument, it only makes an entry in the storage that you can refer to for loading the samples, and that you can refer to for playing back after the samples have loaded.

This separation allows you to synchronize the loading of the samples with the loading of the rest of your application. 


### loadInstrument()  
Loads the samples of the instrument. 

This method is overloaded, you can use it in the following ways: 
```
#!javascript

// loads the samples of an instrument that has already been added to heartbeat's storage
sequencer.loadInstrument('my_instrument', callback);

// same as above
sequencer.loadInstrument('my_instrument', 'my_bank', callback);

// same as above but adds the instrument to another bank
sequencer.loadInstrument('my_instrument', 'other_bank', callback);

// loads several instruments
sequencer.loadInstrument(['my_instrument1', 'my_instrument2', 'my_instrument3'], callback);

```

### loadBank()  
Loads the default bank or the bank that is currently set by `useBank()`, see below. It is possible to have more than one bank loaded at the same time; in this case you have to prepend the name of the bank to the instrument id of the track, see [track](track.md), because the combination of bank name and instrument name is a unique identifier for an instrument.


### useBank()  
Sets the bank that heartbeat will use for playing midi notes. By default heartbeat uses the default bank; if you haven't added any instruments to the default bank, you won't be able to hear anything.


Code example of the 3 ways that you can use `loadBank()` to load an instrument:

```
#!javascript

// method 1

sequencer.loadBank('my_bank', callback);


// method 2

// set the default bank to 'my_bank'
sequencer.useBank('my_bank');

// now you don't have to provide a bank name 
sequencer.loadBank(callback);


// method 3

// load a number of banks
sequencer.loadBank(['my_bank1', 'my_bank2'], callback);

```


### addSamples()  

This method allows you to add base64 encoded samples to heartbeat's sample storage object.

```
#!javascript

var samples = {
		'my_sample1': 'CDB9gBKUgIEMGakCUiCAI0JWA ...',
		'my_sample2': 'EhGgAPgSqwJAVAIG7+qo/x0pn ...',
		'my_sample3': 'BASTRtILywY0BPYHPzSjHjqIc ...',
		
		...

		'my_sample44': 'ZJkU6C8+Bn4an2GA6HZ0SgeNB ...'
	};


	sequencer.addSamples('my_samples/my_sampled_piano', samples);

```

The samples object is a mapping of sample names to base64 encoded sample audio data. The names of the samples don't have to be unique outside the scope of the samples object, as long as the combination of the path and the sample name is unique. The path is the key in the sample storage object that contains the audio data.

If a path contains slash forwards, new objects will be created inside the heartbeat's main sample storage object. In the case of the example above the main sample storage object will look like:

```
#!javascript

// sequencer.sounds is the main object

sequencer.sounds = {
	
	'my_samples': {

		'my_sampled_piano': {

			'my_sample1': 'CDB9gBKUgIEMGakCUiCAI0JWA ...',
			'my_sample2': 'EhGgAPgSqwJAVAIG7+qo/x0pn ...',
			'my_sample3': 'BASTRtILywY0BPYHPzSjHjqIc ...',
			
			...

			'my_sample44': 'ZJkU6C8+Bn4an2GA6HZ0SgeNB ...'
		}
	}
}

```

In this example I use the name 'my_sampled_piano' but it is not mandatory to organize samples around an instrument. The sample storage is just a simple database that you can organize in any way you like.

Note that by separating samples and instruments you can use the same samples in multiple instruments.


### Tools

In the tools folder you'll find a file called sample_to_base64.js, this is very basic tool that allows you convert the samples of your instrument to an key-value object that contains the base64 encoded audio data, as described above.

You have to replace the instrument object in line 4 with your own code and then run the file in [Nodejs](http://nodejs.org/) on the command line:

`nodejs sample_to_base64.js > output.js`  

The output is piped to a file output.js but you can use a more descriptive name like for instance my_piano_samples.js. 

If you add the generated file to your html page (after you've added heartbeat.min.js) the samples will be automatically added to heartbeat's sample storage and can be accessed by your instruments using the path you've provided.

I will make the tool more user friendly and also create an online version of the tool. Josh: for the time being you can also send me your instruments and samples and I convert it for you.

Also it will be possible in the future to load soundfonts directly into heartbeat.