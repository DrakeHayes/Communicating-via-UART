# Communicating-via-UART
## Overview
In this project, we have connected a modern Arduino to a 6502 computer via a 6551 UART chip.  Doing so has allowed us to write messages to the Uno to be sent to our 6502 computer.  These messages are sent using asynchronous serial communication, and they are displayed on the 6502 computer's LCD screen.
## Important Features
Connecting an Arduino to our 6502 computer allows us to easily modify the messages displayed to its LCD screen.  For the sake of example, we've chosen the message "Hello World!", but one could change this message to whatever they wanted by making small changes to the Arduino code.  Without the Arduino, to change the message being displayed to the 6502 computer's LCD screen, one would have had to not only make changes to the 6502 assembly code, but also remove the EEPROM chip from the computer and burn their modified code to it using an EEPROM programmer, which is more time intensive and has the potential of damaging the EEPROM chip.  

Whatever the messages, we are using asynchronous serial communication to send them.  Asynchronous serial communication essentially means our messages are being broken down into their individual bytes and sent one-by-one.  In our circuit, these bytes are being sent from a transmitting UART (the Arduino) to a receiving UART (the 6551 chip).  When the 6551 UART chip receives a byte, the third bit of its status register is flipped from a 0 to a 1, indicating to the Arduino that it has received its transmission and is working on processing it.  This byte then gets loaded into the data register and sent to the versatile interface adapter, which tells the LCD to print this byte to its screen. When this byte is sent to the VIA, the receiver data register is emptied and the third bit of the status register is flipped back to a 0.  This indicates to the Arduino that it has finished processing its transmission and is ready for the next one. This process will repeat until the Arduino has finished sending its message, at which point it will enter a do-nothing loop.

## Step-by-Stp User Guide
1. Construct the Uno-paired 6502 computer according to the schematic, which can be found in the provided project report under section 5.2 "Circuit Shematic". 
2. Connect power and ground to the circuit. Be sure to use a 5V DC supply. The LCD should light up, and nothing besides solid black or white squares should appear on the screen.
3. Press the 6502 computer’s reset button, which is located nearest the 6502 microprocessor chip. The white or black squares should disappear, leaving nothing but the cursor.
4. If after several seconds nothing appears on the LCD screen, then this means that the Arduino has already transmitted all of its data. Simply press the reset button on the Arduino to restart its transmission. After a couple of seconds, the message should appear on the LCD screen.
5. Pressing the 6502 computer’s reset button again clears the LCD screen, and pressing the Arduino’s reset button reprints the message on the LCD screen.
6. To alter the message displayed to the LCD screen, open up the Arduino code and make changes to the variable: string[].  
7. Disconnect power and ground to shut off the circuit.
