# Reverse engineering of the Saitek MX-130 vintage PC joystick
This is a reverse engineering of the Saitek MX-130 vintage PC joystick that I bought recently.

The only aim of this work is educational and because of its interest for retro-enthusiast to repair their old crap :)

<img width="30%" alt="Saitek joystick" src="https://github.com/user-attachments/assets/30c13bfa-e046-485f-8d49-e5d8b3d9c5d7" />

As it didn't work (classic _untested_ item in eBay), I thought that it'd be a good opportunity to reverse-engineer the small board that controls the switches, as anyway I had to open it.

The board itself is quite simple, with two PNP transistors and some resistors. A PC joystick is supposed to have potentiometers and provide an analog output, although it's easy to make a digital one by configuring fixed values for the resistors according to the switches pressed, as the  Saitek MX-130 does.

<img width="745" height="435" alt="board" src="https://github.com/user-attachments/assets/6ba124d7-22e0-46be-80ca-b6a45417a2f9" />

The connection of the two buttons is direct: they're connected between ground and the corresponding write in the connector.

For the paddle, it uses twice the same circuit with a PNP transistor and three resistors, for the horizontal and vertical directions.

<img width="471" height="388" alt="image" src="https://github.com/user-attachments/assets/bc4ed483-efab-4d0e-ac46-b68d4d746721" />


The principle is quite simple. Let's see it with the horizontal direction. It works equivantly for the vertical direction.

- When both switches SW3 and SW4 and open (the paddle is centered), Q1 is activated thus putting 5V between X_axis and R6. The current depends on the impedance after Y_axis, but we can see that the current goes through a single 50K resistor.
- When SW3 is closed, 5V are directly put on Y_axis
- When SW4 is closed, Q1 is open and therefore the current flows from R5 to R6 and arrives at Y_axis. The equivalent resistor is then 100K.

To summarize, depending on the direction, the current goes through 0, 1, or 2 resistors, and therefore we have three different levels of current according to the position of the paddle.
