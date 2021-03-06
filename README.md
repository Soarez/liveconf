## liveconf

A very simple and barebones configuration module. Just allows runtime configuration objects to be synced with JSON configuration files.

**For a much more solid module on cofiguration, check out [node-config](https://github.com/lorenwest/node-config). **

### Install

    npm install liveconf

### Use

Have a configuration file with some configuration. e.g. `config.json`

```json
{
   "a":8,
   "b":"foo"
}
```

```javascript
var liveconf = require('liveconf');

// get the configuration from a file
var config = liveconf('config.json');

console.log(config.b); // foo 
```

The configuration object will be cached and will always be the same for the same configuration file. The configuration file is watched so any changes are reflected on the object.

While the code is running you can change the configuration.

```json
{
   "b":"bar",
   "c":42
}
```

```javascript
console.log(config.b); // bar
```

#### Events

Each configuration object exposes an [EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter) through a non-enumerable readonly property `ee`. There is only one event `changed`, fired when the configuration object is changed.

```javascript
var liveconf = require('liveconf');
var config = liveconf('config.json');

config.ee.on('changed', function() {
    // config file has changed
});
```

### License

MIT