# Digital Door Access System Using Combinational Logic

Course: Digital Design and Computer Architecture (DDCA), 26EC1202E
Institution: Koneru Lakshmaiah Education Foundation, Department of Freshman Engineering
Academic Year: 2026-27
Guide: Dr. Venkanna Isampalli
Section: 5

## Team Members

- Greeshma Kolagotla - 2620040163
- G.L.B. Ananya - 2620040168
- Thanishka - 2620090077
- Shritha - 2620030424

## Project Description

Mechanical keys can be lost, copied or picked, and many electronic locks are complex and costly for simple needs. This project uses basic logic gates (AND, OR, NOT) to unlock a door only when the entered 4-bit digital code matches an authorised code.

The design is purely combinational: the output depends only on the present inputs, with no memory or clock. It was designed using Boolean algebra, a truth table and a K-map, and simulated in Logisim. A zone-power circuit is added to save energy by powering a zone only when it is needed.

## Objectives

- Design a combinational circuit that unlocks only for authorised codes.
- Derive and minimise the Boolean expression.
- Verify the design with a truth table and K-map.
- Simulate correct, incorrect and edge cases in Logisim.
- Add zone-based control to save energy.

## Inputs and Outputs

Inputs:
- A, B, C, D: the 4-bit access code (A is the most significant bit)
- E: the Enter key. With E = 0 the door stays locked and no alarm sounds
- P: presence sensor (1 = someone is in the zone)
- Z: zone enable (1 = the zone may be powered)

Outputs:
- U: unlock (green LED / door lock)
- W: access denied (red LED / buzzer)
- L: zone power (zone loads such as lights, fan and keypad)

## Boolean Expressions

The authorised codes are 1011 (user) and 1111 (master):

- 1011 = A.B'.C.D
- 1111 = A.B.C.D

In the K-map, the two 1s sit next to each other (cells 1011 and 1111) and can be grouped together. B changes inside that group, so B is a don't-care and drops out of the expression.

Final equations:

- Unlock: U = E . A . C . D
- Denied: W = E . U'
- Zone power: L = Z . (P + U)

## Truth Table (E = 1)

Only 1011 and 1111 give U = 1. Every other code gives U = 0 and W = 1. With E = 0, every code gives U = 0 and W = 0 (door locked, no alarm).

- ABCD = 0000: U = 0, W = 1
- ABCD = 0001: U = 0, W = 1
- ABCD = 0010: U = 0, W = 1
- ABCD = 0011: U = 0, W = 1
- ABCD = 0100: U = 0, W = 1
- ABCD = 0101: U = 0, W = 1
- ABCD = 0110: U = 0, W = 1
- ABCD = 0111: U = 0, W = 1
- ABCD = 1000: U = 0, W = 1
- ABCD = 1001: U = 0, W = 1
- ABCD = 1010: U = 0, W = 1
- ABCD = 1011: U = 1, W = 0
- ABCD = 1100: U = 0, W = 1
- ABCD = 1101: U = 0, W = 1
- ABCD = 1110: U = 0, W = 1
- ABCD = 1111: U = 1, W = 0

## Components Required

- Input switches A, B, C, D to enter the 4-bit access code
- Enter key (E) to trigger the code check
- Presence sensor (P) to detect whether someone is in a zone
- Zone enable (Z) to allow a zone to be powered
- AND, OR and NOT gates to compare the code with 1011 and 1111 and to produce U, W and L
- Green LED / door lock to show access granted (U = 1)
- Red LED / buzzer to show access denied (W = 1)
- Zone loads and a 5V DC power supply
- Software: Logisim, for circuit design and simulation

## Circuit Working

1. The user sets the 4-bit code on switches A, B, C, D and presses Enter (E = 1).
2. AND and NOT gates compare the code with the authorised codes 1011 and 1111.
3. Match: U = 1, so the door unlocks and the green LED turns ON.
4. No match: W = 1, so the door stays locked and the red LED / buzzer turns ON.
5. The zone logic L = Z.(P + U) powers a zone only when it is enabled and occupied, or when the door has just unlocked.

The circuit has three parts:
- A 4-input AND gate (inputs A, C, D, E) produces U.
- A NOT gate and a 2-input AND gate (inputs NOT U and E) produce W.
- An OR gate (inputs P and U) followed by a 2-input AND gate (with Z) produces L.

## How to Run the Simulation

1. Install Logisim (Logisim-evolution also works).
2. Open the circuit file from the logisim folder (door_access.circ).
3. Select the Poke tool (the hand) and click the input pins to toggle them between 0 and 1.
4. Set A, B, C, D and E, then check the LEDs U (unlock), W (denied) and L (zone power).
5. To see the full truth table, go to Project > Analyze Circuit.

## Simulation Results

All 16 codes were tested with E = 1, then with E = 0.

- Code 1011 with E = 1: U = 1, W = 0 (green LED on, door unlocks)
- Code 1111 with E = 1: U = 1, W = 0 (green LED on, door unlocks)
- Code 1000 with E = 1: U = 0, W = 1 (red LED on, door stays locked)
- Code 1110 with E = 1: U = 0, W = 1 (red LED on, door stays locked)
- Code 0000 with E = 1: U = 0, W = 1 (red LED on, door stays locked)
- Any code with E = 0: U = 0, W = 0 (door locked, no alarm)

Zone check, L = Z.(P + U):
- Z = 1 with P = 1 gives L = 1.
- Z = 1, P = 0, U = 0 gives L = 0.
- Z = 0 always gives L = 0.

## Advantages

- Simple and easy to understand.
- Quick response, with no clock or memory delay.
- Low cost and simple hardware.
- Easy to simulate and verify with a truth table.
- Energy saving through zone control.

## Limitations

- Authorised codes are fixed in hardware, so changing them needs rewiring.
- No memory, so wrong attempts cannot be counted and there is no lockout.
- Only 16 code combinations, so the code can be observed or guessed.
- The basic model controls a single door and a simple zone.

## Applications

- Homes, offices, laboratories and server rooms.
- Educational demonstration of combinational logic design.

## Future Scope

- Keypad encoder for easier code entry.
- Attempt lockout using flip-flops.
- Longer codes.
- Upgrade with Arduino, RFID or IoT for smart access control.

## Repository Contents

- README.md: this file
- logisim.circ: the Logisim circuit for the project
- Project.pdf
- Poster.png

## Conclusion

A digital door access system was designed and simulated using only combinational logic. The 4-bit code, Enter key and zone inputs are combined with AND, NOT and OR gates to control the lock, the denied indication and the zone power. The truth table and the Logisim simulation agree, so the design works as intended. Boolean simplification reduced the unlock logic to a single AND gate.
