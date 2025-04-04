# Zane Lewis Final project proposal

- [X] I have reviewed the project guidelines.
- [X] I will be working alone on this project.
- [X] No significant portion of this project will be (or has been) used in other course work.

## Embedded System Description

This project will simulate a smart traffic light controller for a four-way intersection. The system will respond to simulated traffic conditions and mode changes, using RGB LEDs to display the traffic light colors, vehicle queue status with the LED lightbar, and current system status and queue data displayed on the LCD display.

Input 1 will be a keypad and will be used to simulate pedestrian requests and cars arriving. Input 2 will be a rotary encoder that is used to scroll through and select the operating modes. Optional modes will be Normal, Rush Hour, Night, and Manual.

The system process will manage light timing, queue management, and mode-specific logic. The green light duration will be adjusted based on traffic input and allow mode switching.

Output 1 will be two RGB LEDS simulating the NorthSouth and EastWest traffic lights. Output 2 will be the LED lightbar used to show traffic queue buildup or flow in the actively flowing direction. Output 3 will be an LCD display showing real-time system status including the mode, light timers, and traffic details.

## Hardware Setup

-MSP430FR2355
-MSP430FR2310 (x2)
-Keypad
-Rotary encoder
-RGB LEDs (x2)
-LED lightbar
-LCD display
-Pull-up resistors, wires, breadboard, and power supply

## Software overview

The master MCU will monitor inputs, manage traffic mode, and determine traffic light timing based on current mode and simulated vehicle flow. The master will send updates over I2C to the slave MCUs with commands that will set the RGB LEDs, update the LED lightbar indicating traffic buildup and flow, and refresh the LCD display with all pertinent traffic, mode and timer information.

Modes:
- **Normal:** Fixed light cycle with a standard green/yellow/red duration
- **Rush Hour:** Green light extended in direction with the most queued cars
- **Night:** Blinking yellow for EastWest unless traffic is detected in NorthSouth direction
- **Manual:** Keypad manually changes light states

## Testing Procedure

In order to test my system I will:
1. Power on, beginning in Normal mode.
2. Use the keypad to simulate number of vehicles arriving and which direction they are arriving.
3. Use the rotary encoder to scroll through modes and then confirm with a push.
4. Observe that the RGB LEDs simulate proper traffic light sequence based on mode.
5. Observe that the LED lightbar simulates the traffic queue of the direction with the green light.
6. Confirm the LCD displays the current mode, timer countdown, direction of traffic currently flowing, and queue data.

## Prescaler

Desired Prescaler level: 

- [ ] 100%
- [ ] 95% 
- [ ] 90% 
- [X] 85% 
- [ ] 80% 
- [ ] 75% 

### Prescalar requirements 

**Outline how you meet the requirements for your desired prescalar level**

**The inputs to the system will be:**
1.  Keypad - simulates traffic or input from pedestrian
2.  Rotary encoder pushbutton - selects and changes traffic mode

**The outputs of the system will be:**
1.   LCD display - shows both directions queue counts, current mode, and the light timer
2.   LED lightbar - shows the queue for the direction with the green light
3.   RGB LEDs - simulates NorthSouth/EastWest traffic lights

**The project objective is**

To simulate an adaptive traffic control system that responds to mode conditions and changing traffic, providing visual feedback with RGB LEDs, a queue display, and status output.

**The new hardware or software modules are:**
1. New hardware is the rotary encoder pushbutton.
2. New software will be a mode based traffic light controller using different timing logic.


The Master will be responsible for:

Reading the inputs, managing the state of the system, implementing timing based on mode, and sending I2C data.

The Slave(s) will be responsible for:

Displaying the traffic lights using RGB LEDs, updating LED light bar to reflect flow of vehicles, and displaying user feedback on LCD.


### Argument for Desired Prescaler

This project meets the 80% prescalar requirements:
-Have 2 inputs: The rotary encoder and the keypad
-Have 3 outputs: The LED lightbar, the LCD display, and 2 RGB LEDs
-Use a master/slave topology: Accomplished via I2C
-Have a "real objective": Implements a smart traffic light controller
-Include 1 new type of hardware or software module: The rotary encoder
-The new hardware is easy to implement and requires applying skills you have developed in class: This final requirement is met

I believe that this combination of using a new interaction method and serving a real world purpose justifies the 85% prescalar level. Additionally this reuses a single LED lightbar to display two directions by context-switching, while offloading continual display data to the LCD.
