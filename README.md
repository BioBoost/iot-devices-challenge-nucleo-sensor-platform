# IoT Devices - Nucleo Sensor Platform

1. Setup the LoRaWAN example (find it at [https://github.com/BioBoost/lorawan-shield-example](https://github.com/BioBoost/lorawan-shield-example))
2. Create a TTN application and register the device
3. Send a message at startup (add firmware version)
4. Setup a payload decoder at the things network
5. Send a message containing the device uptime every 30s
6. Attach the led controller to the board
7. Send the firmware version of the led controller along with the firmware version of the main app at startup

## Payload Decoder

```js
function decodeUplink(input) {
  let message = {
    data: {},
    errors: [],
    warnings: []
  }

  if (input.fPort == 1) {
    message.data.counter = input.bytes[0]
  } else if (input.fPort == 3) {
    message.data.firmware_version = input.bytes[0]
  } else {
    message.data.bytes = input.bytes
  }

  return message;
}
```
