# ioBroker.type-detector

This is not the adapter. This is help function to detect devices from ioBroker states and channels.

## How to use
You can use this module in Browser and in Node.js projects. 

Just now this module used in material adapter to detect devices and to visualize them.

Following code detect devices in some state's tree.

```javascript
// 
const ChannelDetector = require('iobroker.type-detector');
const detector = new ChannelDetector();

const keys = Object.keys(objects);				// For optimization
const usedIds = [];                 			// To not allow using of same ID in more than one device
const ignoreIndicators = ['UNREACH_STICKY'];    // Ignore indicators by name
const supportedTypes = ['button', 'rgb', 'dimmer', 'light'];	// Supported types. Leave it null if you want to get ALL devices.

const options = {
	objects:            this.props.objects,
	id:                 'hm-rpc.0.LEQ1214232.1',
	_keysOptional:      keys,
	_usedIdsOptional:   usedIds,
	ignoreIndicators:   ignoreIndicators
};

let controls = detector.detect(options);
if (controls) {
	controls = controls.map(function (control) {
		const id = control.states.find(state => state.id).id;
		if (id) {
			console.log(`In ${options.id} was detected "${control.type}" with following states:`);
			control.states.forEach(state => {
				if (state.id) {
					console.log(`    ${state.name} => ${state.id}`);
				}
			});

			return {control, id};
		}
	});
} else {
	console.log(`Nothing found for ${options.id}`);
}
```


## Description
Following devices can be detected:


### Media player

### Weather forecast

### RGB color

### Warnings

### Thermostat

### Blinds

### Motion detector

### Window

### Window with tilted position

### Fire alarm

### Door

### Dimmer

### Light

### Volume

### Group volume

### Level slider

### Socket

### Button

### Temperature

### Info


## Changelog
### 0.1.1 [2019-05-24]
* (bluefox) add PRECIPITATION to weather
* (bluefox) add location detection

### 0.1.0 [2018-08-14]
* (bluefox) initial commit



## License

Copyright (c) 2018-2019 bluefox <dogafox@gmail.com>

MIT License
