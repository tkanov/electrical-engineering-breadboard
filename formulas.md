

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

