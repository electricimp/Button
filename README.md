# Button

This Squirrel class implements debouncing for buttons connected to an imp. It requires one line of code in your device firmware: to instantiate the class. This involves passing callback functions that will be executed, respectively, when the button is pressed and then released. The class automatically handles bounces, ensuring your callbacks are only run when the button has been intentionally pressed and released.

## Class Usage

## Constructor:<br>Button(*pin, pull, polarity, pressCallback, releaseCallback*)

To instantiate a Button object, pass it the following parameters:

- *pin* &ndash; the *unconfigured* impOS pin object representing the pin to which the button is wired
- *pull* &ndash; an impOS constant, either *DIGITAL_IN_PULLDOWN*, *DIGITAL_IN* or *DIGITAL_IN_PULLUP*
- *polarity* &ndash; the unpressed button state, eg. 1 if the button is pulled up and the button shorts to GND
- *pressCallback* &ndash; the function to be called if the button is pressed, or `null` if you don’t want to monitor button presses)
- *releaseCallback* &ndash; the function to be called if the button is release, or `null` if you don’t want to monitor button releases)

The following code shows a typical example of the class’ use. A button is connected to an imp’s pin 7. The other side of the switch runs to GND. Single presses are best monitored by checking for button releases, so that the user’s action is not implemented if they press and hold the button. The button is used to switch an LCD display’s backlight on and off.

```squirrel
button <- Button(hardware.pin7, DIGITAL_IN_PULLUP, 1, null, function() {
  backlightFlag = !backlightFlag
  display.setBacklight(backlightFlag)
})
```

## License

The Button library is licensed under the [MIT License](./LICENSE).
