# Button

This Squirrel class implements debouncing for buttons connected to an imp. It requires one line of code in your device firmware: to instantiate the class. This involves passing callback functions that will be executed, respectively, when the button is pressed and then released. The class automatically handles bounces, ensuring your callbacks are only run when the button has been intentionally pressed and released.

## Class Usage

## constructor(*pin, pull, [polarity], [pressCallback], [releaseCallback]*)

The Button constructor has two required parameters - *pin*, and *pull* - and three optional parameters - *polarity*, *pressCallback*, *releaseCallback*.

- *pin* &ndash; the *unconfigured* impOS pin object the button is wired to (e.g. ```hardware.pin1```)
- *pull* &ndash; the impOS constant used to configure the digital input (either ```DIGITAL_IN```, ```DIGITAL_IN_PULLDOWN```, or ```DIGITAL_IN_PULLUP```)
- *polarity* &ndash; the unpressed button state (either ```Button.NORMALLY_HIGH``` or ```Button.NORMALLY_LOW```). If this parameter is not passed to the ctor, it will be infered based on the pull parameter:
    - ```DIGITAL_IN``` - ```Button.NORMALLY_LOW```
    - ```DIGITAL_IN_PULLDOWN``` - ```Button.NORMALLY_LOW```
    - ```DIGITAL_IN_PULLUP``` - ```Button.NORMALLY_HIGH```
- *pressCallback* &ndash; the callback function (no parameters) to be executed when the button is pressed.
- *releaseCallback* &ndash; the callback function (no parameters) to be executed when the button is released.

```squirrel
#require "button.class.nut:1.1.0"

button <- Button(hardware.pin7, DIGITAL_IN_PULLUP);
```

## button.onPress(callback)

The *onPress* method sets the callback for the button's onPress event (i.e. when the button is depressed). If an onPress callback function is already registered, it will be replaced with the new callback. Setting the callback to ```null``` will result in no action when the button is pressed (this is the default behavior).

```squirrel
button.onPress(function() {
  server.log("Button Pressed!");
});
```

## button.onRelease(callback)

The *onRelease* method sets the callback for the button's onRelease event (i.e. when the button is released). If an onRelease callback function is already registered, it will be replaced with the new callback. Setting the callback to ```null``` will result in no action when the button is released (this is the default behavior).

```squirrel
button.onRelease(function() {
  server.log("Button Released!");
});
```

## License

The Button library is licensed under the [MIT License](./LICENSE).
