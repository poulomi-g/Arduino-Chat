# Arduino-Chat

### Description

A simple chat program between two Arduinos. Two people will type into separate serial monitors. The message typed into the serial monitor will be sent to one Arduino, encrypted, sent to the other Arduino using using the serial port pins, decrypted, and then displayed on the other person’s serial monitor. The encryption protocol we will use is RSA. This program is able to randomly generate its own public and private keys for both parties and utilize it for the RSA encryption technique.

Collaborated with: Charles Ancheta

### Included Files:
* encrypted_communication_part2.cpp
* README
* Makefile

### Accessories:
* 2 Arduino Mega Boards, one as client and one as server
* 2 560 Ohm (Green Blue Brown) resistors
* Wires

### Wiring Intructions:
	Client Arduino TX3 <--> Server Arduino RX3
	Client Arduino RX3 <--> Server Arduino TX3
	Any Arduino GND <--> Resistor <--> Client Arduino Pin 13
	Any Arduino +5V <--> Resistor <--> Server Arduino Pin 13
	Server Arduino GND <--> Client Arduino GND

### Running Instructions: 

1. Connect both the Arduinos to separate PCs using an A-B style USB cable. 
	Ensure that the Arduino is using the proper serial port (/dev/ttyACMO or -ACM1)

2. In the directory containing the files encrypted_communication_part1.cpp and 
	Makefile, use the command "make upload" and "serial-mon 0 0" respectively to 
	upload the code to the arduino and view the serial monitor.

### Notes and Assumptions:
	
#### Functions used:
* mulMod(): Takes in three unsigned 32-bit integer values, a, b and m to return 
	an unsigned 32-bit integer res that contains the mudular multiplied result 
	of the accepted variables.
* powMod(): Takes in three unsigned 32-bit integers x, pow and m and returns an 
	unsigned 32-bit integer ans. (Discussed in class)
* uint32_to_serial3(): Writes a uint32_t to serial3 starting from LSB to MSB
* uint32_from_serial3(): Reads a uint32_t to serial3 starting from LSB to MSB
* send_char(): Encrypts a given character and sends it to Serial3 and includes 
	special cases as needed
* receive_char(): Receives character and writes it to Serial (includes special 
	cases like backspace and return keys)
* random_num(): Returns a random uint32_t number based on a given number of bits, k
* prime_check(): Returns a bool value indicating if given number is prime.
* random_prime(): Generated a uint32_t prime number randomly k bits long.
* gcd(): GIVEN IN CLASS
* mod_inverse(): Returns multiplicative inverse of given uint32_t e.
* key_gen(): Generates public and private keys of Arduino and its modulus.
* wait_on_serial3(): GIVEN IN CLASS, function for finite state machines.
* server_exchange(): follows the state diagram for key exchange on server side.
* client_exchange(): follows the state diagram for key exchange on client side.
* key_exchange(): displays the randomly generated public key and modulus. 
	it also exchanges keys with the other Arduino. 


#### Assumptions: 
* The program assumes that the user types at a normal speed, as typing at extremely fast speeds or keyboard mashing overflows the serial buffer and causes the program to not work properly.
* It is possible that the Arduinos are rapidly sending NULL characters right after setting up, so it is recommended to wait for a few seconds before testing the program
* In the event that the serial buffer overflows, the program is coded such that it would clear any garbage bytes making communication still possible without resetting the Arduinos
* It could also be possible that one of the Arduinos is ready to chat while the other is not (e.g. one computer does not have serial monitor open yet). In this case, we assume that the Arduinos are reset while the serial monitors are both open.
