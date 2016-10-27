# rfswitch Module
| Since  | Origin / Contributor  | Maintainer  | Source  |
| :----- | :-------------------- | :---------- | :------ |
| 2016-10-27 | [Roman Fedorov](https://github.com/ffedoroff) | [Roman Fedorov](https://github.com/ffedoroff) | [rfswitch.c](../../../app/modules/rfswitch.c)|


Module for operate 433/315Mhz devices like power outlet sockets, relays, etc.
This will most likely work with all popular low cost power outlet sockets
with a SC5262 / SC5272, HX2262 / HX2272, PT2262 / PT2272, EV1527,
RT1527, FP1527 or HS1527 chipset.

This module using some code from original [rc-switch](https://github.com/sui77/rc-switch/) arduino lib
but NodeMCU and Arduino are not fully compatible, and it cause
for full rewrite **rc-switch** into this new **rfswitch** lib for NodeMCU with Lua support.

Connection of transmitter:

| Transmitter  | ESP8266  | comments                        |
| :----------- | :------- | :------------------------------ |
| vin or + | 3V3 | 3.3 - 5 volts on ESP8266 or other power source |
| ground or - | GND | ground should be connected to ESP8266 and to power source |
| data pin | 6 | almost any pin on ESP8266 |

You can read more about connection, [here](https://alexbloggt.com/wp-content/uploads/2015/10/nodemcu_433_transmitter.png) or [here](https://alexbloggt.com/funksteckdosensteuerung-mit-esp8266/).

## rfswitch.send()
Transmit value ising radio module.

#### Syntax
`rfswitch.send(protocol_id, pulse_length, repeat, pin, value, length)`

#### Parameters
- `protocol_id` positive integer value, from 1-6 (see [rfswitch.c](../../../app/modules/rfswitch.c))
- `pulse_length` length of one pulse in microseconds, usually from 100 till 650
- `repeat` repeat value, usually from 1 till 5
- `pin` IO index of pin, example 6 is for GPIO12 [see more](../modules/gpio/)
- `value` positive integer value, this is the primary data which will be sent
- `length` bit length of value, if value length is 3 bytes, then length is 24

#### Returns
`nil`

#### Example
```lua
-- lua transmit radio code using protocol #1
-- pulse_length 300 microseconds
-- repeat 5 times
-- use pin #7 (GPIO13)
-- value to send is 560777
-- value length is 24 bits (3 bytes)
rfswitch.send(1, 300, 5, 7, 560777, 24)
```
