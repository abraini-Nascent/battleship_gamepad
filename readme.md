# Battleship Gamepad

A hand-wired 3d-printed mechanical keyboard intended for one hand with an analog thumbstick for movement.  The layout matches the left side of large "battleship" keyboards with their extra bank of 2x5 1u F keys.

Reference-style: 
![keyboard image][hero]

## Features
- 40 keys
- Swappable analog thumbsticks
- Low profile ( 1.50cm case height, 3cm from desk to keytop. 1cm bezel)
- [QMK firmware](https://qmk.fm/)
- [VIA integration](https://caniusevia.com/)

## Layout
From left to right  
2x5 ortho layout  
0.25u open space  
1x5 1.25u keys replacing the ~, tab, caps, shift, cntl keys  
5x5 ortho layout  
Analog thumbstick  

## BoM

- 6 3d printed parts ( at least 180mm print surface )
- 1 usb arduino pro micro
- Analog thumbstick + breakout board
- 50 cherry footprint switches
- 45 1u keycaps
- 5 1.25u keycaps
- 50 fast switching diodes
- Enameled Magnet Wire (30 or 32 awg)
- Ribbon cable
- M3 screws
- USB cable

## Construction
Decide on if you are going to use the large PS/XBOX style thumbstick or the mobile sliding style thumbstick.

1. Print out the [switch plate](./parts/keyplate.stl) and two ([front](./parts/proMicroMountFront.stl), [back](./parts/proMicroMountBack.stl)) arduino controller mounts  
![arduino stands][arduinoStands]  
2. Print the approriate thumbstick mount peices  
a. If you are using the large thumbstick print the [large stand](./parts/thumbStickMountA.stl), [mount](./parts/thumbStickMountB.stl), and [cover](./parts/thumbStickCover.stl)  
b. If you are using the sliding thumbstick print the [sliding stand](./parts/slideStickMount.stl)
3. Follow the [QMK guides for hand-wiring](https://beta.docs.qmk.fm/using-qmk/guides/keyboard-building/hand_wire "Hand Wiring Guide") a matrix  
For the diodes I chose wire wrap the diodes to the switch post and bend the legs so they hooked into the next diode.
![diodes wired][diodesWired]  
For the columns I chose to wire wrap the top and bottom most switch posts and alternate the side the wire made contact with the other switch posts. 
![enamel wire][enamelWire]  
For connecting the rows and columns to the arduino the ribbon cable is used and kept neat.  
![ribbon wire][ribbonWired]  
![arduino wire][arduinoWired]  
4. Wire the rows to the pro micro as follows:  
```
row 0 = pin 10, row 1 = pin 16, row 2 = pi 14, row 3 = pin 14, row 4 = pin 15
```  
(these are the pins in order from the edge furthest from the usb connector moving towards it)  

5. Wire the columns to the pro micro as follows:  
```
col 0 = pin 2, col 1 = pin 3, col 2 = pin 4, col 3 = pin 5, col 4 = pin 6, col 5 = pin 7, col 6 = pin 8, col 7 = pin 9
``` 
6. Epoxy or glue the arduino stand mounts in the correct location.
### Wiring the analog thumbstick
The analog thumbstick is wired to the arduino using the ribbon cable.  A connection can be placed in the middle of the cable to allow the thumbstick type to be swappable or the thumbstick can be wired directly to the arduino.  

1. Solder the wire the ground and vcc from the arduino to the thumbstick
2. Solder the wire the pro micro analog in pins  
```
x-axis to pin A1
y-axis to pin A2
click  to pin A3
```
![slide thumbstick][slideStick]  

3. Pass the ribbon through the channel of the 3d-printed stand  

4. Solder the GND, VCC, and analog input wires to the underside of the thumbstick breakout board's GND, VCC, x axis, y axis, and click pins.
![thumbstick wired][thumbStickWired]  

5. Screw the breakout board to the stand.  If using the large thumbstick place the cover on the thumbstick before screwing in the board.  
6. Screw the stand to the plate from the inside of the plate wall
![console thumbstick][thumbStick]

## Future improvements
1. The three analog pins can be used for more than just thumbsticks.  It could be also be wired to:
- An 8-way HAT using voltage dividers
- A rotery encoder knob and push button or mousewheel
- Linear potentiometer thumb sliders for throttle
- Ergodox style thumb cluster of hal effect swiches for analog values  

2. The thumbstick reports as an HID device for a DirectInput joystick.  Some games require XInput, some don't allow both XInput and mouse input.  A collection of other tools are required such as [Joystick Gremlin](https://whitemagic.github.io/JoystickGremlin/), [x360ce](https://www.x360ce.com/) and [antimicro](https://github.com/AntiMicro/antimicro) to manage the input.  
It would be nice to implement an analog to keypress map similar reWASD, antimicro, or the MAME input mapper.  

3. Easier swap thumb device? Right now the bottom cover needs to be unscrewed so the internal screws can be removed to replace the thumb device.  If possible having the screw mounts on the outside and the cable connector on the keyboard case wall would allow easier changing of the thumb device.


[hero]: ./images/case.jpg "Hero image of Battleship Gamepad"
[arduinoStands]: ./images/arduinoStands.png "Cad image of arduino stands"
[diodesWired]: ./images/diodesWired.jpg "The leg of one diode crossing to the leg of the diode to the right's leg"
[enamelWire]: ./images/enamelWire.jpg "Enamel wire is wrapped on the topmost switch. it alternates touching the sides of posts before wrapping the final switch"
[ribbonWired]: ./images/rowsWired.jpg "ribbon wire soldered to rows"
[arduinoWired]: ./images/arduinoWired.jpg "ribbon wire soldered to arduino"
[slideStick]: ./images/slidestick.png "mobile style sliding thumbstick mount assembly"
[thumbStick]: ./images/thumbstick.png "console style thumbstick mount assembly"
[thumbStickWired]: ./images/thumbstickWired.jpg "thumbstick wired to the arduino"