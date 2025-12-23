The projects below are a small lab log of breadboard experiments with 74xx logic ICs and an Arduino Nano (power distribution and NPN transistor LED drivers).

---

## Project #1
### OR, AND gates 

The breadboard contains an OR gate and AND gate.

Inputs are controlled with pushbuttons.

The outputs are connected to LEDs to easily observe their states. Gates act independently.

- Power: 5V
- 7408 QUADRUPLE 2-INPUT POSITIVE-AND 
- 7486 Quad EXCLUSIVE-OR Gate
- Red LED: 330Ω
- Red LED: 220Ω (probably)





---


![Image](attachments/ee-1.jpeg)

![Image](attachments/ee-2.jpeg)

![Image](attachments/ee-3.jpeg)


---


## Project #2
### Using Arduino Nano to power the Breadboard (5V)

- Nano pin 5V to Positive
- Nano pin GND to Negative/Ground on BB


![Image](attachments/ee-4.jpeg)


---


## Project #3
### Using Arduino Nano to blink a green and red LEDs

Make sure GNDs are connected.

Pushbuttons were not supposed to be there, so please ignore them.

Code:

[will paste here]


#### On the board:
- Transistor 1: PN2222 / T1
- Resistor 1: 2.0 kΩ
- Transistor 2: PN2222 / T2
- Resistor 2: 2.0 kΩ
- Green LED
- Green LED resistor 220Ω
- Red LED
- Red LED resistor 220Ω


#### Nano pins:
- D4 + 2.0 kΩ to Base of T1
- D5+ 2.0 kΩ to Base of T2
- GND to GND of the power source


#### Conditions and assumptions:
Arduino Nano pin is 5 V. 
A PN2222 base-emitter drop is about 0.7V ([PN2222 specs](docs/PN2222-D.pdf))


Given:
```
V_OUT ≈ 5.0 V
V_BE ≈ 0.7 V
R_B = 2 kΩ = 2000 Ω
```

Base current:
```
I_B ≈ (V_OUT - V_BE) / R_B
I_B ≈ (5.0 - 0.7) / 2000
I_B ≈ 4.3 / 2000
I_B ≈ 0.00215 A
I_B ≈ 2.15 mA
```

Collector current estimate using forced beta of 10:
```
beta_forced ≈ 10
I_C ≈ beta_forced * I_B
I_C ≈ 10 * 2.17 mA
I_C ≈ 21.7 mA
```


[Formulas](formulas.md)

---



![Image](attachments/ee-5.jpeg)
![Image](attachments/ee-6.jpeg)
![Image](attachments/ee-7.jpeg)
![Image](attachments/ee-8.jpeg)


---

