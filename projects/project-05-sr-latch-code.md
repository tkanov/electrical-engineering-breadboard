# Project 5 — Implementing 1 bit of memory - Arduino code

This time the **SR latch** "memory" is built in code, using a C function that implements NOR gates instead of analog (hardware) logic gates.

```
const int button1vendD4 = 4;
const int button2coinD5 = 5;
const int ledPin = 6;

struct SRLatch {
  uint8_t Q;
  uint8_t Qbar;
};

uint8_t NOR_gate(uint8_t A, uint8_t B) {
  return !(A || B); // logical NOR
}

void SR_update(SRLatch &l, uint8_t S, uint8_t R) {
  uint8_t q = l.Q;
  uint8_t qb = l.Qbar;

  uint8_t nextQ = NOR_gate(R, qb); // Q depends on R and previous Qbar
  uint8_t nextQb = NOR_gate(S, q); // Qbar depends on S and previous Q

  l.Q = nextQ;
  l.Qbar = nextQb;
}

SRLatch latch = { 0, 1 }; // start reset-ish: Q=0, Qbar=1

void setup() {
  pinMode(button1vendD4, INPUT_PULLUP);
  pinMode(button2coinD5, INPUT_PULLUP);

  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, LOW);
}

void loop() {
  uint8_t r = (digitalRead(button1vendD4) == LOW) ? 1 : 0;
  uint8_t s = (digitalRead(button2coinD5) == LOW) ? 1 : 0;

  SR_update(latch, s, r);
  digitalWrite(ledPin, latch.Q ? HIGH : LOW);
}
```

![Image](../attachments/ee-14.jpeg)

![Image](../attachments/ee-15.jpeg)

---
