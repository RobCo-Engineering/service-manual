# `Pip` Library

### `#onknob1`

Contains a list of event handlers currently registered for the top knob, this
list updated whenever the main page changes.

### `#onknob2`

Contains a list of event handlers currently registered for the main mode switch.

### `#ontorch`

Contains a list of event handlers currently registered for the torch button.

### `addWatches()`

Watches are function handlers designed to watch pin states and execute a handler
function when state changes, eg. when a button is pressed, a knob is turned etc.
This method is part of the boot sequence of the Pip-Boy and registers a set of
watches with [`setWatch`](https://www.espruino.com/Reference#l__global_setWatch)
to bind handlers to all of the device inputs.

### `audioBuiltin()`

Returns a byte array for a built-in sound effect, ready to be used by
`audioStartVar()`.

#### Parameters

| Name   | Type                                                       | Default | Description                           |
| ------ | ---------------------------------------------------------- | ------- | ------------------------------------- |
| `name` | `"OK" \| "OK2" \| "PREV" \| "NEXT" \| "COLUMN" \| "CLICK"` | —       | Identifier for built-in sound effects |

#### Example

```js
const okSound = Pip.audioBuiltin("OK");
Pip.audioStartVar(okSound);
```

### `audioGetFree()`

Returns the number of samples left free in the audio ring buffer.

### `audioIsPlaying()`

Returns a boolean true if audio is currently playing.

### `audioRead()`

Read the given WAV file into RAM.

#### Parameters

| Name            | Type     | Default | Description                                                                                                     |
| --------------- | -------- | ------- | --------------------------------------------------------------------------------------------------------------- |
| `fileName`      | `string` | -       | Path to file on the SD card.                                                                                    |
| `returnOptions` | `object` | -       | If an object is supplied, it'll be filled with `encoding` and `blockAlign` fields ready for `Pip.audioStartVar` |

#### Example

```js
let rawInfo = {}; // Object to receive options
const raw = Pip.audioRead("UI/HOLO.wav", rawInfo); // Read audio file

print(a);
// return: { "encoding": 16 }
```

### `audioStart()`

Play a WAV audio file straight from the SD card.

#### Parameters

| Name             | Type      | Default | Description                                        |
| ---------------- | --------- | ------- | -------------------------------------------------- |
| `fileName`       | `string`  | -       | Path to WAV file on SD card                        |
| `options`        | `object`  | -       | Playback options                                   |
| `options.debug`  | `boolean` | `false` | Enables playback debug info                        |
| `options.repeat` | `boolean` | `false` | Continue to play the sound once it reaches the end |

### `audioStartVar()`

Play audio straight from a variable of raw WAV data - this adds everything to
the buffer at once so blocks

If `encoding:"adpcm"` you may need to specify a `blockAlign` value, but you can
populate this with `Pip.audioRead`.

#### Parameters

| Name                 | Type                 | Default | Description                                                |
| -------------------- | -------------------- | ------- | ---------------------------------------------------------- |
| `waveAudio`          | `raw`                | —       | Raw PCM or ADPCM audio data                                |
| `options`            | `object`             | `{}`    | Playback options                                           |
| `options.overlap`    | `boolean`            | `false` | Mix with existing audio in ringbuffer instead of replacing |
| `options.encoding`   | `16 \| 8 \| "adpcm"` | `16`    | WAV encoding type                                          |
| `options.blockAlign` | `number`             | `512`   | Required for ADPCM playback                                |
| `options.sampleRate` | `number`             | `16000` | Input sample rate                                          |

#### Example

```js
let rawInfo = {}; // Object to receive options
const raw = Pip.audioRead("UI/HOLO.wav", rawInfo); // Read audio file
Pip.audioStartVar(raw, rawInfo); // Play sample
```

### `audioStop()`

Immediately stop playing sounds via the codec.

### `blitImage()`

Render an image to screen.

#### Parameters

| Name                   | Type               | Default | Description                                                                                             |
| ---------------------- | ------------------ | ------- | ------------------------------------------------------------------------------------------------------- |
| `img`                  | `data`             | -       | Raw image data.                                                                                         |
| `x`                    | `number`           | `0`     | X coordinate for where to place top left corner of image                                                |
| `y`                    | `number`           | `0`     | Y coordinate for where to place top left corner of image                                                |
| `options`              | `object \| number` | -       | Additional options object or if only a number is specified, is used as `scale`                          |
| `options.scale`        | `number`           | `1`     | Scale up the image, if a scale of less than `1` is specified, it's rounded up to 1                      |
| `options.noScanEffect` | `boolean`          | -       | Hides the scanline effect                                                                               |
| `options.height`       | `number`           | -       | If `height` isn't specified the image height is used, otherwise only part of the image can be rendered. |

### `brightness`

Stores the current screen brightness value, eg. `20`.

### `btnDownPrev`

### `btnPlayPrev`

### `btnUpPrev`

### `clockVertical`

### `demoMode`

### `fadeOff()`

The function fades LED pins from an initial brightness down to off by repeatedly
multiplying by 0.65 until reaching 0.01, then resetting the pins.

#### Parameters

| Name                | Type     | Default    | Description                                                                       |
| ------------------- | -------- | ---------- | --------------------------------------------------------------------------------- |
| `pins`              | `array`  | `[LCD_BL]` | List of analog pins to fade out, by default will fade out just the LCD backlight. |
| `initialBrightness` | `number` | `1`        | Used as starting value for fade. Default is calculated from `Pip.brightness`      |

### `fadeOn`

The function fades LED pins on, functionally the opposite of `Pip.fadeOff()` it
multiplies by 1.46 each interval until reaching target brightness.

#### Parameters

| Name               | Type     | Default                        | Description                                                                                                                                                                    |
| ------------------ | -------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `pins`             | `array`  | `[LCD_BL, LED_RED, LED_GREEN]` | List of analog pins to fade on, by default will fade out LCD backlight and the red and green channels of the RGB, also conditionally will add `LED_TUNING` if the radio is on. |
| `targetBrightness` | `number` | `1`                            | Used as target final value for fade. Default is calculated from `Pip.brightness`                                                                                               |

### `getAudioWaveform()`

This copies the contents of the current I2S audio buffer out to an array
(`destinationArray`) that can be rendered to the screen with `drawPoly`.

Because the array is meant to be `x,y,x,y,x,y` only the second elements are
touched.

#### Parameters

| Name               | Type     | Default | Description                                           |
| ------------------ | -------- | ------- | ----------------------------------------------------- |
| `destinationArray` | `array`  | -       | Variable where resulting waveform data is copied into |
| `yMin`             | `number` | -       | Minimum Y coordinate for waveform display             |
| `yMax`             | `number` | -       | Maximum Y coordinate for waveform display             |

### `getDateAndTime()`

Returns a JS `Date` object with the current date/time.

### `getID()`

Returns the device serial number.

### `idleTimer`

### `initDAC()`

Part of the Pip-Boy boot sequence, this configures the ES8388 audio codec by
writing to the IC's configuration registers over I2C.

### `isSDCardInserted`

Returns a simple boolean showing the status of the SD card, read from the
`SDCARD_DETECT` pin.

### `kickIdleTimer()`

Clears and resets the device idle timeout set at `Pip.idleTimer`.

### `knob1Click()`

Event handler for handling top knob changes, configured to play click sound
based on direction.

#### Parameters

| Name        | Type     | Default | Description                   |
| ----------- | -------- | ------- | ----------------------------- |
| `direction` | `number` | -       | Direction the knob was turned |

### `knob2Click()`

Event handler for handling left knob changes, configured to play click sound
based on direction.

#### Parameters

| Name        | Type     | Default | Description                   |
| ----------- | -------- | ------- | ----------------------------- |
| `direction` | `number` | -       | Direction the knob was turned |

### `measurePin()`

The function enables measurement, takes averaged analog readings from a pin,
then scales the result by a factor. Used for things like reading battery voltage
where the VBAT is via a voltage divider, hence the default scaling being 2.

#### Parameters

| Name          | Type     | Default | Description                                        |
| ------------- | -------- | ------- | -------------------------------------------------- |
| `pin`         | `Pin`    | -       | Analog pin reference.                              |
| `sampleCount` | `number` | `10`    | Used as loop count for averaging multiple readings |
| `scaleFactor` | `number` | `2`     | Scales the averaged voltage reading                |

#### Example

```js
Pip.measurePin(VBAT_MEAS); // Returns battery voltage
```

### `mode`

Stores the current "mode" as an integer, where 1 = STAT, 2 = INV and so on.

### `off()`

Enter standby mode - should only be started by pressing the power button
(`PA0`).

### `offAnimation()`

Plays the screen off animation.

### `offButtonHandler`

Event handler attached to the power button.

### `offOrSleep()`

Puts the device either into a sleep or an off state, by default will show an
animation and LED states on the way off etc.

#### Parameters

| Name                | Type      | Default | Description                                                                           |
| ------------------- | --------- | ------- | ------------------------------------------------------------------------------------- |
| `options`           | `object`  | `{}`    | -                                                                                     |
| `options.forceOff`  | `boolean` | `false` | Instead of going to sleep with `Pip.sleep()` this forces off via `Pip.off()` instead. |
| `options.immediate` | `boolean` | `false` | Skip the animation on the way off an immediately power down.                          |

### `powerButtonHandler()`

Event handler tied to button pressed of the device power button, handles
wake/sleep based on power status etc.

### `readDACReg()`

Returns the current value of a DAC register.

#### Parameters

| Name       | Type     | Default | Description      |
| ---------- | -------- | ------- | ---------------- |
| `register` | `number` | -       | Register to read |

### `remove()`

Removes a currently active page, initially calls `Pip.removeSubmenu()` if
defined and then removes `knob2` and `torch` button listeners.

### `removeSubmenu()`

This method should be overriden by any page that is being displayed and contains
cleanup functions that should be run when the user navigates away from that
menu. This will for example remove any specific input event handlers that are
registered, clear any render intervals defined etc.

### `setDACMode()`

Puts the DAC into a specified mode.

#### Parameters

| Name   | Type             | Default | Description                                                                                                                        |
| ------ | ---------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `mode` | `"off" \| "out"` | `"off"` | Mode to set, `"off"` will disable the DAC audio output. `"out"` will enable output, if `mode` is undefined, it will assume `"off"` |

### `setDACPower()`

Enable/disable the DAC power supply (which also powers the audio amp and SD
card).

#### Parameters

| Name   | Type      | Default | Description |
| ------ | --------- | ------- | ----------- |
| `isOn` | `boolean` | `false` |             |

### `setDateAndTime()`

Sets the device date/time, will store the "century" to the settings file.

#### Parameters

| Name   | Type   | Default | Description                               |
| ------ | ------ | ------- | ----------------------------------------- |
| `date` | `Date` | -       | JS Date object with the date/time to set. |

### `setLCDPower()`

Enable/disable the LCD power supply.

#### Parameters

| Name   | Type      | Default | Description |
| ------ | --------- | ------- | ----------- |
| `isOn` | `boolean` | `false` |             |

### `setPalette()`

Set the colour palette used for rendering everything on PipBoy.

#### Parameters

| Name      | Type    | Default | Description                                                                       |
| --------- | ------- | ------- | --------------------------------------------------------------------------------- |
| `palette` | `Array` | -       | Palette is a 4 element array of 16 element arrays, as shown in the example below. |

#### Example

```js
const pal = [
  new Uint16Array(16),
  new Uint16Array(16),
  new Uint16Array(16),
  new Uint16Array(16),
];

// Orangey
for (let i = 0; i < 16; i++) {
  pal[0][i] = g.toColor(i / 15, i / 30, 0); // 0: even (bright line)
  pal[1][i] = g.toColor(i / 30, i / 60, 0); // 1: odd (dark line)
  pal[2][i] = g.toColor(i / 10, i / 20, 0); // 0: even scan effect
  pal[3][i] = g.toColor(i / 20, i / 40, 0); // 1: odd scan effect
}
Pip.setPalette(pal);
```

### `setVol()`

Sets the output volume of the DAC.

#### Parameters

| Name     | Type     | Default | Description                                                                            |
| -------- | -------- | ------- | -------------------------------------------------------------------------------------- |
| `volume` | `number` | -       | Value must be in the range `0` to `33`, anything outside those bounds will be clamped. |

### `sleep()`

Enter sleep mode - JS is still executed.

### `sleeping`

Simple boolean value showing if the device is currently in a sleep state or not.

### `statIndex`

Stores the index of the Vault Boy animation currently being displayed on the
**Status** page.

### `streamPlaying()`

"Returns `"video"` if a video is playing, or `"audio"` if audio is playing,
`"both"` for both, or `undefined` otherwise.

### `typeText()`

Prints some text on the screen in a typed effect under the Vault-Tec logo.

#### Parameters

| Name   | Type     | Default | Description                                            |
| ------ | -------- | ------- | ------------------------------------------------------ |
| `text` | `string` | -       | The text to display on the screen in the typing effect |

#### Example

```js
Pip.typeText("Hello World");
```

### `updateBrightness()`

Updates the state of LCD backlight and other LED's to the brightness specified
by `Pip.brightness`.

### `usbConnectHandler()`

Event handler for when USB is connected or disconnected. If USB is connected
device will wake from sleep.

#### Parameters

| Name    | Type      | Default | Description                         |
| ------- | --------- | ------- | ----------------------------------- |
| `state` | `boolean` | -       | The new state of the USB connection |

### `videoStart()`

Starts playback of an AVI video file.

#### Parameters

| Name             | Type      | Default | Description                                                            |
| ---------------- | --------- | ------- | ---------------------------------------------------------------------- |
| `fileName`       | `string`  | -       | Path to an AVI file on the SD card                                     |
| `options`        | `object`  | -       | Playback options                                                       |
| `options.x`      | `number`  | `0`     | Top left corner X coordinate where to place video                      |
| `options.y`      | `number`  | `0`     | Top left corner Y coordinate where to place video                      |
| `options.debug`  | `boolean` | `false` | Playback debug info                                                    |
| `options.repeat` | `boolean` | `false` | When video playback finishes, should it start again from the beginning |

#### Example

```js
Pip.videoStart("UI/THUMBUP.avi", { x: 150, y: 80 });
```

### `videoStop()`

Stops the playback of any currently playing AVI stream.

### `wake()`

Wake up the pipboy.

### `writeDACReg()`

Writes a DAC register with a value.

#### Parameters

| Name       | Type     | Default | Description                        |
| ---------- | -------- | ------- | ---------------------------------- |
| `register` | `number` | -       | The register to write to           |
| `value`    | `number` | -       | The value to write to the register |
