Digital Door Access System Using
Combinational Logic
Course: Digital Design and Computer Architecture (DDCA), 26EC1202E
Institution: Koneru Lakshmaiah Education Foundation, Department of Freshman Engineering
Academic Year: 2026–27
Guide: Dr. Venkanna Isampalli
Team Members
Section: 5
Project Description
Mechanical keys can be lost, copied or picked, and many electronic locks are complex and costly for
simple needs. This project uses basic logic gates (AND, OR, NOT) to unlock a door only when the entered
4-bit digital code matches an authorised code.
The design is purely combinational: the output depends only on the present inputs, with no memory or
clock. It was designed using Boolean algebra, a truth table and a K-map, and simulated in Logisim. A
zone-power circuit is added to save energy by powering a zone only when it is needed.
Objectives
• Design a combinational circuit that unlocks only for authorised codes.
• Derive and minimise the Boolean expression.
• Verify the design with a truth table and K-map.
• Simulate correct, incorrect and edge cases in Logisim.
• Add zone-based control to save energy.
Inputs and Outputs
Signal Type Meaning
A, B, C, D Input 4-bit access code (A is the MSB)
E Input Enter key. E = 0 keeps the door locked with no alarm
P Input Presence sensor (1 = someone is in the zone)
Z Input Zone enable (1 = zone may be powered)
U Output Unlock (green LED / door lock)
W Output Access denied (red LED / buzzer)
L Output Zone power (zone loads)
Digital Door Access System | DDCA 26EC1202E | Page 1
Boolean Expressions
Authorised codes: 1011 (user) and 1111 (master).
1011 = A.B'.C.D
1111 = A.B.C.D
The K-map groups the two 1s, so B is a don't-care:
AB \ CD 00 01 11 10
00 0 0 0 0
01 0 0 0 0
11 0 0 1 0
10 0 0 1 0
Final equations:
Unlock (U): U = E . A . C . D
Denied (W): W = E . U'
Zone power (L): L = Z . (P + U)
Truth Table (E = 1)
Only 1011 and 1111 give U = 1. With E = 0, every code gives U = 0 and W = 0 (locked, no alarm).
A B C D U W
0 0 0 0 0 1
0 0 0 1 0 1
0 0 1 0 0 1
0 0 1 1 0 1
0 1 0 0 0 1
0 1 0 1 0 1
0 1 1 0 0 1
0 1 1 1 0 1
1 0 0 0 0 1
1 0 0 1 0 1
1 0 1 0 0 1
1 0 1 1 1 0
1 1 0 0 0 1
1 1 0 1 0 1
1 1 1 0 0 1
1 1 1 1 1 0
Components Required
Component Function
Input switches (A, B, C, D) Enter the 4-bit access code
Enter key (E) Triggers the code check
Digital Door Access System | DDCA 26EC1202E | Page 2
Component Function
Presence sensor (P) Detects whether someone is in a zone
Zone enable (Z) Allows a zone to be powered
AND / NOT / OR gates Compare the code with 1011 and 1111; produce U, W and L
Green LED / door lock Shows access granted (U = 1)
Red LED / buzzer Shows access denied (W = 1)
Zone loads, power supply Lights, fan, keypad; 5V DC supply
E Code ABCD U W
0 any 0 0
1 1011 1 0
1 1111 1 0
1 1000 0 1
1 1110 0 1
1 0000 0 1
Software: Logisim (circuit design and simulation).
Circuit Working
1. 2. 3. 4. 5. The user sets the 4-bit code on switches A, B, C, D and presses Enter (E = 1).
AND and NOT gates compare the code with the authorised codes 1011 and 1111.
Match: U = 1, so the door unlocks and the green LED turns ON.
No match: W = 1, so the door stays locked and the red LED / buzzer turns ON.
The zone logic L = Z.(P + U) powers a zone only when it is enabled and occupied, or when the door
has just unlocked.
How to Run the Simulation
1. 2. 3. 4. 5. Install Logisim (Logisim-evolution also works).
Open the circuit file from the logisim/ folder (door_access.circ).
Select the Poke tool (the hand) and click the input pins to toggle them between 0 and 1.
Set A, B, C, D and E, then check the LEDs U (unlock), W (denied) and L (zone power).
To see the full truth table, go to Project > Analyze Circuit.
Simulation Results
All 16 codes were tested with E = 1, then with E = 0. Near-miss codes such as 1000 and 1110 are denied.
Zone check, L = Z.(P + U):
• Z = 1 with P = 1 gives L = 1.
• Z = 1, P = 0, U = 0 gives L = 0.
• Z = 0 always gives L = 0.
Advantages
• Simple and easy to understand.
• Quick response, with no clock or memory delay.
Digital Door Access System | DDCA 26EC1202E | Page 3
• Low cost and simple hardware.
• Easy to simulate and verify with a truth table.
• Energy saving through zone control.
Limitations
• Authorised codes are fixed in hardware, so changing them needs rewiring.
• No memory, so wrong attempts cannot be counted and there is no lockout.
• Only 16 code combinations, so the code can be observed or guessed.
• The basic model controls a single door and a simple zone.
Applications
• Homes, offices, laboratories and server rooms.
• Educational demonstration of combinational logic design.
Future Scope
• Keypad encoder for easier code entry.
• Attempt lockout using flip-flops.
• Longer codes.
• Upgrade with Arduino, RFID or IoT for smart access control.
Repository Contents
digital-door-access-system/
|-- README.md
|-- logisim/
| |-- door_access.circ
|-- docs/
|-- Digital_Door_Access_Final_Project.pptx
|-- poster
|-- report
Team Contributions
Member Contribution
Greeshma Kolagotla [add contribution]
G.L.B. Ananya [add contribution]
Thanishka [add contribution]
Shritha [add contribution]
Conclusion
A digital door access system was designed and simulated using only combinational logic. The 4-bit code,
Enter key and zone inputs are combined with AND, NOT and OR gates to control the lock, the denied
indication and the zone power. The truth table and the Logisim simulation agree, so the design works as
intended. Boolean simplification reduced the unlock logic to a single AND gate.
