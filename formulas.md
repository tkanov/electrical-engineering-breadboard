

**Base current:**

* `I_B ≈ (V_OUT - V_BE) / R_B`

**Rule-of-thumb for saturation (forced beta):**

* `beta_forced ≈ 10`

**Collector current estimate (using forced beta):**

* `I_C ≈ beta_forced * I_B`

**Combined (collector current from base resistor directly):**

* `I_C ≈ beta_forced * (V_OUT - V_BE) / R_B`

**Solve for base (B) resistor:**

* `R_B ≈ beta_forced * (V_OUT - V_BE) / I_C`

Typical values to plug in:

* `V_OUT ≈ 5.0 V` (Arduino Nano HIGH)
* `V_BE ≈ 0.7 V` (rough on-state estimate)

---

## LED current with a series resistor

```
I = (V_supply - V_f) / R
I in amps (A)
V_supply = supply voltage (V)
V_f = LED forward voltage (V)

R = resistor value (Ω)
```

Example for `5 V supply, red LED V_f ≈ 2.0 V, R = 330 Ω`:

```
I = (5 - 2.0) / 330
I = 3.0 / 330
I = 0.00909 A ≈ 9.1 mA

R = (V_supply - V_f) / I
```

