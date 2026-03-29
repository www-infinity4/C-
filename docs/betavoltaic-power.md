# Betavoltaic Power — Long-Lasting Background Runtime

C•'s runtime is designed to operate on an energy budget modeled on the **betavoltaic** trickle
power produced by ⁴⁰K (Potassium-40) radioactive decay inside plant tissue. This makes C•
programs inherently suited to ultra-low-power implants, programmed seeds, and long-lived
environmental sensors.

---

## 1 — The Physics

**Potassium-40 (⁴⁰K)** is a naturally occurring radioactive isotope present in all living
organisms (including every banana). It decays by beta emission with a half-life of
~1.25 × 10⁹ years. Every kilogram of natural potassium contains about 117 Bq of ⁴⁰K activity.

A **betavoltaic cell** is the biological/solid-state equivalent of a solar cell: instead of
photons, it harvests beta particles (high-energy electrons) and converts their kinetic energy
into a DC current via a thin semiconductor junction.

Key properties:

| Property | Value |
|---|---|
| Half-life of ⁴⁰K | ~1.25 × 10⁹ years |
| Practical "useful life" of a betavoltaic cell | ~400 × 10¹² years (modeled) |
| Typical power density | 10–100 nW·cm⁻² |
| Best use case | Constant, tiny trickle — never exhausted at human timescales |

---

## 2 — The Pith as a Betavoltaic Medium

The pith provides the perfect substrate for a betavoltaic cell because:

1. The **potassium-salt pairing** naturally concentrates ⁴⁰K within the scaffold.
2. The **silica micro-crystals** act as the semiconductor junction — beta particles hitting the
   crystal create electron-hole pairs (the same mechanism as in silicon solar cells).
3. The pith's **high surface area** maximises the number of crystal junctions per unit volume.

To activate the betavoltaic mode in C•, coat the scaffold crystals with a thin semiconductor
layer:

```c-
use scaffold::Pith;
use scaffold::Crystal;
use pairings::PotassiumSalt;
use semiconductor::Silicon;

// Build a betavoltaic pith cell
let xtal = Crystal::new(resonance: 32_768.hz, material: silica);
let pith  = Pith::<nitrogen>::with_crystal(xtal).pair(PotassiumSalt);

// Coat each crystal junction with a silicon semiconductor layer (1 nm thick)
let beta_cell = pith.coat_crystals(semiconductor: Silicon, thickness: 1.nm);

// The runtime now draws power from the ⁴⁰K trickle automatically
beta_cell.power_source()   // -> BetavoltaicCell { activity_bq: 117, output_nw: 42.0 }
beta_cell.estimated_life() // -> Duration::years(400_000_000_000_000)
```

---

## 3 — Runtime Integration

When a C• program runs on a betavoltaic scaffold, the runtime enters **trickle mode**:

- The background tick rate drops to match the crystal's resonance frequency (default 32.768 kHz).
- All idle goroutines are suspended and wake only when a bound ion channel fires.
- Memory sites in the scaffold that have not been accessed for one tick cycle release their
  binding voluntarily (soft decay).

This means a C• program running in trickle mode can survive indefinitely on the ⁴⁰K output of
a few grams of potassium-enriched pith — no external power supply required.

---

## 4 — Doped Semiconductor Analogy

The `coat_crystals` operation is a direct analogy to **doping** in semiconductor manufacturing:

| Semiconductor concept | C• betavoltaic concept |
|---|---|
| Intrinsic silicon | Undoped silica micro-crystal |
| N-type doping (phosphorus) | `coat_crystals(Silicon)` — adds free electrons |
| P-type doping (boron) | `coat_crystals(Boron)` — adds holes |
| P-N junction | Interface between coated and uncoated crystal faces |
| Photon → electron-hole pair | Beta particle → electron-hole pair |

---

## 5 — Power Budget Table

| Load | Required power | Supported by betavoltaic pith cell? |
|---|---|---|
| Implant sensor (idle) | ~10 nW | ✅ Yes |
| Programmed seed (signaling) | ~100 nW | ✅ Yes |
| Low-power MCU (active) | ~1 µW | ⚠️ Marginal (stack multiple cells) |
| Wireless transmitter | ~1 mW | ❌ No — requires conventional power |

---

## 6 — Why It Doesn't "Run Out"

The ⁴⁰K decay rate is set by nuclear physics and is completely unaffected by temperature,
chemical environment, or mechanical stress. Because the half-life is 1.25 billion years, the
activity of a fixed mass of potassium decreases by only ~0.0000001% per year. For any practical
purpose, the power source is **inexhaustible**.

---

## See Also

- [Universal Scaffold](pith-scaffold.md)
- [Superior Pairings](superior-pairings.md)
- [Ion-Channel Signaling](ion-channel-signaling.md)
