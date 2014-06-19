# _Attiny 1634 serial boot loader based on TinySafeBoot_

_Description: This project is based on TinySafeBoot http://jtxp.org/tech/tinysafeboot_en.htm. It contains little modification especially for Attiny1634._

## Project Setup

_How do I, as a developer, start working on the project?_

_Development environment_

* TinySafeBoot software from http://jtxp.org/tech/tinysafeboot_en.htm
* Atmel Studio 6.2
* AVR writer (e.g. USBtinyISP from adafruit)
* FreeBasic
* Ruby (for formatting hex codes)

_How can I see the project working before I change anything?_

1. Open tsb1634.atsln and build project by Atmel Studio.
2. Format hex codes. E.g. >ruby -i.bak -pe '$_.gsub!(/(.+)/,"data \"\\1\"")' tsb1634.hex
3. Replace tn1634 section of TinySafeBoot data.bas file with the formatted hex codes.
4. Compile TSB software (a host side tool) with FreeBasic. E.g. >fbc tsb.bas
5. Make bootloader codes (.hex file) by TSB software. E.g. >tsb tn1634 a7b0
6. Write the bootloader into target flash by an AVR writer. E.g. >avrdude -c usbtiny -p t1634 -U flash:w:tsb_tn1634_a7b0_20140619.hex
7. Connect USB (or bluetooth) UART converter TX/RX to target PA7:RX/PB0:TX.
8. Verify TSB connection. E.g. Reset target and >tsb com5 i
9. Write App. E.g. Reset target and >tsb com5 fw MI100R6.cpp.hex

## License
GPLv3

