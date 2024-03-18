# Flint
A Budget (and Currently Sketchy) Full Arduino EEPROM Programmer for 28Cx EEPROMs

NOTE: Still Editing This .md

## What does Flint do?
Flint is a really sketchy way to use an Arduino to program an EEPROM fully. This sketch uses a Makefile to generate 6KB chunks of binary data and imports them to the sketch directory. This allows you to flash the Aurdino with the data without relying on the Serial Bus to send data (which I had problems using - I will be looking into using this in future versions, but this works currently). I created this project because I didn't want to pay £70 for an EEPROM programmer at the current time of building my project.

## Using the Programmer
1. Build the circuit using the Schematic by Ben Eater. 
2. Download the Makefile and run `make proj`. This will download any other files required by this project to work. It will also create a project workspace.
3. cd into `/src` from the project direcory and edit `main.s` to your liking (there will be some placeholder code). Note, if you wish to change the name of `main.s` you must change this also in the Makefile!
4. Return back to the project directory and run `make`. This will build files in `/src` using `vasm` and split `rom.out` located in `/bin` into 6KB chunks. These chunks will then be converted to seperate C++ header files so that the Arduino can read it. They will be then copied over to `/flint`.
5. Open `flint.ino` located in `/flint` and edit `"chunk_0*.hpp"` and `CHUNK_NUM *` where `*` is the number of the chunk you wish to flash to the EEPROM. Remember, the first file will be `0`. If you are using the Aurdino IDE you will see a list of `.hpp` files at the top.
6. Check pin-outs on your Arduino if they match up, else edit them to your liking. Suggested pins will be listed in another section.
7. Flash the code to the Arduino.
8. All Set! Repeat from 5 - 7 until all your code has been flahed to your EEPROM.

## Dependencies
- `make`
- `vasm`
- `split`
- `xxd`
- `wc`

### Ben Eater
Flint is heavly based on Ben Eater's EEPROM Programmer code. Thanks to Ben Eater, else I would never have started!

- EEPROM Programmer: https://github.com/beneater/eeprom-programmer/blob/master/eeprom-programmer/eeprom-programmer.ino
- Schematic: https://github.com/beneater/eeprom-programmer/blob/master/schematic.png
