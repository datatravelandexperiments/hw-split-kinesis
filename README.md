Split Keyboard
==============

This is the hardware for modifying a [Kinesis contoured keyboard](http://kinesis-ergo.com/contoured.htm) into two separated units.

**This is a work in progress, and the hardware/software described here has not been shown to work correctly.**

The replacement controller communicates by SPI to an I/O expander on each keywell. Each keywell board plugs in to the keywell using staggered pin headers replacing the original FFC connector, and has a separate connector for the thumb keys. The rubber function keys are abandoned; I intend to use a FN key on the thumb matrix instead.

The controller (kctlspi) uses a [Micropendous 32U2](http://code.google.com/p/micropendous/wiki/Micropendous_32U2) board, because I happened to have a few on hand. Modifying it to use a similar device like a Teeny, Pro Micro, etc. should be straightforward.

The controller board has two Mini-DIN 8 jacks for the keywells. The pinout of these connectors is chosen such that the controller board could be repurposed as a dual PS/2 converter by swapping in Mini-DIN 6 connectors.

The controller also has two 6p6c jacks. The middle 4 pins match the pinout of foot switches for current Kinesis contoured keyboards; the other two supply V<sub>CC</sub> and GND to allow the possibility of active devices. The foot connectors are wired as a 2×3 matrix.

The controller board is sized to fit (half) a [readily available project box](http://www.google.com/search?q=24+70+110+aluminum+project+box). (Note: Many 6p6c jacks are too tall to fit this enclosure.)

The keywell boards (lctlspi and rctlspi) each use an MCP23S17 I/O expander. An MCP23017 could be substituted directly to use I<sup>2</sup>C rather than SPI. The chip's <span style="text-decoration:overline">RESET</span> and <span style="text-decoration:overline">CS</span> pins are present on the connector, but can be pulled up/down on the board instead.

The appropriate INTx pin is also present on the connector, so it should be possible to set up the I/O expander and put the controller to sleep until any key is pressed.

Left and right keywell controllers are different because the Kinesis keywells have different matrices. The correspondence between keywell signals and I/O expander pins is arbitrary (i.e. determined by layout convenience); that is, column 1 on the keywell does not correspond to pin 1 on an I/O port, and so on. Similarly the thumb pad connectors have the same pattern (GND, four columns, three rows) but the specific arrangement of rows and columns is arbitrary.

Schematics and boards are in [Eagle CAD](http://www.cadsoftusa.com/download-eagle/) format.

<!-- vim:set et sts=4 sw=4 linebreak ft=ghmarkdown: -->
