node-bleacon
============

A node.js lib to interact with iBeacons

Install
-------

    npm install bleacon

Usage
-----

    var Bleacon = require('bleacon');

__Start scanning__

    var uuid = 'E2C56DB5DFFB48D2B060D0F5A71096E0';
    var major = 0; // 0 - 65535
    var minor = 0; // 0 - 65535

    Bleacon.startScanning([uuid], [major], [minor]);

 Examples

    Bleacon.startScanning(); // scan for any bleacons

    Bleacon.startScanning(uuid); // scan for bleacons with a particular uuid

    Bleacon.startScanning(uuid, major); // scan for bleacons with a particular uuid and major

    Bleacon.startScanning(uuid, major, minor); // scan for bleacons with a particular uuid. major, and minor

__Stop scanning__

    Bleacon.stopScanning();

__Events__

    Bleacon.on('discover', function(bleacon) {
        // ...
    });

```bleacon``` properties:
 
 * uuid
   * advertised uuid
 * major
   * advertised major
 * minor
   * advertised minor
 * measuredPower
   * advertised measured RSSI at 1 meter away
 * rssi
   * current RSSI
 * accuracy
   * +/- meters, based on measuredPower and RSSI 
 * proximity
   * current proximity ('unknown', 'immediate', 'near', or 'far')

Experimental
------------

More support will come when [noble](https://github.com/sandeepmistry/noble) supports peripheral mode

__Soft iBeacon___

Linux

    sudo node linux-bleacon.js

iBeacon Advertisement format
----------------------------

__Note:__ not official, determined using [noble](https://github.com/sandeepmistry/noble), and the [AirLocate](http://adcdownload.apple.com/wwdc_2013/wwdc_2013_sample_code/ios_airlocate.zip) example.

Following data is in the ```manufacturer data``` section of the advertisment data

    <header (4 bytes)> <uuid (16 bytes)> <major (2 bytes)> <minor (2 bytes)> <RSSI @ 1m>

Example:

    4C000215 585CDE931B0142CC9A1325009BEDC65E 0000 0000 C5

 * header: ```4C000215```
 * uuid: ```585CDE931B0142CC9A1325009BEDC65E```
 * major: ```0000```
 * minor: ```0000```
 * meaured power at 1 meter: ```0xc5``` = ```-59```
