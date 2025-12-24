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

[!] Make sure GNDs are connected

(Pushbuttons were not supposed to be there, so please ignore them)

#### Code:

- Blinks the 2 LEDs with different intervals.
- LED pins 1 and 2 are connected to PN2222 Base.

```
const int led1Pin = 4;
const int led2Pin = 5;

const unsigned long led1IntervalMs = 250;
const unsigned long led2IntervalMs = 350;

unsigned long lastLed1 = 0;
unsigned long lastLed2 = 0;

bool led1State = false;
bool led2State = false;

void setup() {
  pinMode(led1Pin, OUTPUT);
  pinMode(led2Pin, OUTPUT);
  digitalWrite(led1Pin, LOW);
  digitalWrite(led2Pin, LOW);
}

void loop() {
  unsigned long now = millis();

  if (now - lastLed1 >= led1IntervalMs) {
    lastLed1 = now;
    led1State = !led1State;
    digitalWrite(led1Pin, led1State ? HIGH : LOW);
  }

  if (now - lastLed2 >= led2IntervalMs) {
    lastLed2 = now;
    led2State = !led2State;
    digitalWrite(led2Pin, led2State ? HIGH : LOW);
  }
}
```


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

PN2222 Collector -> LED cathode  / 2x

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


## Project #4
### Implementing 1 bit of memory 

The "memory" is built on an SR latch using 2 NOR gates.

The two chips below implement NOR gates because I didn't have a single NOR chip). There are 2 NOR gates on the board, as needed to implement a single SR latch device.

- `SN74HC32N (7432)`  [SNx4HC32 Quadruple 2-Input OR Gates](docs/sn74hc32.pdf)
- `SN74HC04N (7404)`  [SNx4HC04 Hex Inverters](docs/sn74hc04.pdf)

SR latch is a type of memory device that remembers 1 bit. The SR latch has
two inputs: S (set) and R (reset), and an output Q, the single bit that is "remembered".

- The red LED represents Q
- The blue LED represents "not Q" to visualize circuit state
- When using an SR latch we typically only look at Q to determine whether the bit is true or false.


---



On the first picture below S is pressed, so the Q is HIGH, meaning that the bit is 1. The state is remembered.

![Image](attachments/ee-9.jpeg)


On the first picture below R was pressed, so the Q is LOW, and "not Q" is HIGH (the blue LED).

![Image](attachments/ee-10.jpeg)

![Image](attachments/ee-11.jpeg)

![Image](attachments/ee-12.jpeg)

![Image](attachments/ee-13.jpeg)


---



