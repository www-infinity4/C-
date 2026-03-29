# Superior Pairings — Amplifier Model

A **Superior Pairing** is the C• module composition primitive. When two modules are explicitly
paired, each amplifies the other's natural output — just as pairing a conductive mesh with plant
pith produces a biological capacitor that neither material could form alone.

---

## 1 — Why Pairings?

The pith's natural "matching stream" is weak on its own. To build a long-lasting power source
or an implantable data store, you must pair the scaffold with a substance whose atomic structure
resonates with — and therefore amplifies — the scaffold's inherent signal.

The table below summarises the three canonical pairings identified during the initial research
phase:

| Pairing | Atomic Reason | Result |
|---|---|---|
| **Pith + Silver / Copper** | Conductive "hairs" thread through the pith web | Biological Capacitor — stores the "spark" from a trigger event |
| **Pith + Phosphorus** | Phosphorus matches the hot tip of the radiation spectrum | Glow-Source — converts trace radiation into visible light |
| **Pith + Potassium Salts** | Boosts the "Banana Magnetism" (⁴⁰K signal) | Nutrient Battery — feeds a signal into a body or a seed |

---

## 2 — Pairing Syntax

```c-
use scaffold::Pith;
use pairings::{Silver, Copper, Phosphorus, PotassiumSalt};

// Biological Capacitor
let capacitor = Pith::<carbon>::new().pair(Silver);
capacitor.charge(trigger: lighter_spark);
capacitor.stored_energy()  // -> joules: f64

// Glow-Source
let glow = Pith::<hydrogen>::new().pair(Phosphorus);
glow.convert(source: trace_radiation);
glow.luminance()  // -> candela: f64

// Nutrient Battery
let battery = Pith::<nitrogen>::new().pair(PotassiumSalt);
battery.emit(frequency: 40.hz, signal: "nutrient_pulse");
battery.remaining_capacity()  // -> mol_K40: f64
```

---

## 3 — The Amplifier Contract

Every pairing module must implement the `Amplifier` trait:

```c-
trait Amplifier {
    // Returns the natural resonance frequency of this material
    fn resonance() -> Frequency;

    // Amplifies an incoming signal and returns the boosted output
    fn amplify(input: Signal) -> Signal;

    // Reports the gain factor at the scaffold's crystal frequency
    fn gain_at(freq: Frequency) -> f64;
}
```

The runtime will reject a pairing at compile time if `Amplifier::gain_at(scaffold.crystal.resonance())`
returns a value ≤ 1.0 — a pairing that does not amplify is not a *superior* pairing.

---

## 4 — Stacked Pairings

Pairings can be stacked. Each layer wraps the previous scaffold and must demonstrate a net gain
over the unwrapped version:

```c-
// Stack copper (conductor) on top of potassium (nutrient) on top of pith
let stack = Pith::<carbon>::new()
    .pair(Copper)          // layer 1 — conductive mesh
    .pair(PotassiumSalt);  // layer 2 — nutrient signal boost

stack.net_gain()  // -> f64: product of all layer gains
```

---

## 5 — Research Connections

- **Doped Semiconductors**: The `pair()` model mirrors how adding a "trace" element to a crystal
  lattice makes it semiconducting. Silicon doped with phosphorus gains a free electron; pith paired
  with phosphorus gains a photon emitter.
- **Bio-Batteries**: The potassium-salt pairing is the direct C• representation of using plant
  cellulose as a paper-thin electrode in a biological battery.

---

## See Also

- [Universal Scaffold](pith-scaffold.md)
- [Ion-Channel Signaling](ion-channel-signaling.md)
- [Betavoltaic Power](betavoltaic-power.md)
