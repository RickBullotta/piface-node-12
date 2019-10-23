About
=====
This is an interface to the Raspberry Pi Piface Digital 2 board using Node.js version 12.  It was adapted from the original piface-node module created by Darryl Hodgins and updated to support Node 12.X.  Darryl's original code is at:

https://github.com/darrylhodgins/piface-node

...and the updated version is at:

https://github.com/RickBullotta/piface-node-12


This addon shouldn't require any sudo or root privileges to run, as long as your user is in the "spi" group on your Pi (handled by the spidev-setup script).

Installation
============
Assuming a fresh Raspbian Stretch install, there are two steps to getting a project off the ground with piface-node.
  - Get Node.js
  - Get the Piface C libraries (if not already installed on your Raspian distribution)
  - Get the piface-node-12 module with NPM

Using piface-node-12
====================
Darryl (original author) intended this to be used with the full awesome power of Node's EventEmitter.  You can easily wire up the physical I/O on the Piface with pretty much anything.

Here's a basic example of the usage, in lieu of actual documentation.  There are also a few examples in the examples folder.
```js
var pfio = require('piface-node-12');
pfio.init();
pfio.digital_write(0,1); // (pin, state)
var foo = pfio.digital_read(0); // (pin; returns state)
pfio.deinit();
```

```js
var pfio = require('piface-node-12');
pfio.init();
var foo = pfio.read_input(); // bit-mapped
pfio.write_output(255); // that's binary 11111111, so it'll turn all outputs on.
pfio.deinit();
```

The Examples Folder
-------------------
Everything in the example application is modular and decoupled: most of the components don't even know that the other ones exist. They only communicate through the EventBus. All that example.js does is start up those modules.  The example application watches for changes on the input pins, and echoes them to the output pins.  Try it out by pressing the tactile switches.

```bash
$ cd node_modules/piface-node-12/examples
$ node example.js
````
