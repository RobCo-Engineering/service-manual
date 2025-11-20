# Input Handling

The Pip-Boy 3000 Mk.V has three input knobs, and two buttons. Namely these are:

| Name         | Ref             | Description                                 |
| ------------ | --------------- | ------------------------------------------- |
| Left Knob    | `knob1`         | The left hand side up/down knob, with click |
| Top Knob     | `knob2`         | The top left/right scroller                 |
| Mode Switch  | `MODE_SELECTOR` | The mode selection switch on the right      |
| Torch Button | `torch`         | Top button used for toggling torch mode     |
| Power Button | `power`         | The power button located under the display  |

## Attaching Input Handlers

Handlers for the above inputs are attached via
[`Pip.on()`](/docs/pipboy-3000-mkv/reference/pip) event handlers, inputs can
have multiple event handlers attached so you may want to ensure exclusivity
depending on your use case.

### Example

```js
// Remove all existing event handlers on knob1
Pip.removeAllListeners("knob1");

// Create a new function for handling knob 1 events
function myKnob1Handler(direction) {
  if (direction > 0) console.log("UP");
  else if (direction < 0) console.log("DOWN");
  else console.log("CLICK");
}

// Attach the custom handler function to 'knob1' events
Pip.on("knob1", myKnob1Handler);

// When the app closes you should call to remove the specific handler you registered
Pip.removeListener("knob1", myKnob1Handler);
```
