# Universal Scaffold — Pith Structure

The **Universal Scaffold** is the foundational metaphor and data model of the C• language.
It is modeled directly on plant pith: a lightweight, highly porous biological substrate with
enormous atomic-level surface area, capable of simultaneously holding energy, information,
and nutrients.

---

## 1 — What is the Pith?

Plant pith is not "just carbon." It is a layered composite:

| Component | Role in the Scaffold |
|---|---|
| **Cellulose** | Structural fibers — the rigid "rails" of the scaffold |
| **Lignin** | Cross-linking polymer — the "glue" between rails |
| **CHON** | The four atomic building blocks (see §2) |
| **Calcium / Magnesium** | Mineral "bones" — rigid, magnetically active anchors |
| **Silica micro-crystals** | Piezoelectric "glass" that can vibrate and hold an EM charge |

The key insight is that the pith's **massive surface-to-volume ratio** means it can interact with
an enormous number of "strings" — energy quanta, information packets, or nutrients — at once.
In C•, this maps directly to the scaffold's ability to bind an arbitrary number of typed signals
simultaneously without contention.

---

## 2 — The CHON Elements

C• exposes four scalar primitive types named after the four principal atoms of the pith:

```c-
// Carbon — dense, stable, long-lived storage
type carbon  = scalar<density: high, stability: high>;

// Hydrogen — mobile, reactive, fast-moving carrier
type hydrogen = scalar<density: low,  mobility: high>;

// Oxygen  — oxidising agent; triggers state transitions
type oxygen  = scalar<reactivity: high, trigger: true>;

// Nitrogen — slow, structural, load-bearing backbone
type nitrogen = scalar<density: medium, structure: true>;
```

These are the **only** scalar types in C•. All composite types are built from them, just as all
organic matter is built from CHON atoms.

---

## 3 — Silica Micro-Crystals

Certain plant piths (notably Indian gum and some grasses) pull microscopic silica from the soil
into their cellular walls. This creates **literal micro-crystals** that:

- Vibrate at a resonant frequency proportional to their size.
- Accumulate and hold an electromagnetic (EM) charge (piezoelectric effect).
- Act as a natural quartz-oscillator inside the biological structure.

In C•, this is represented by the `Crystal` type, which is always embedded inside a `Pith`
scaffold and provides the **resonance frequency** for that scaffold's ion channels:

```c-
use scaffold::Pith;
use scaffold::Crystal;

// A silica crystal tuned to 32.768 kHz (quartz-watch frequency)
let xtal: Crystal = Crystal::new(resonance: 32_768.hz, material: silica);

// Embed it in a pith scaffold — this "tunes" the scaffold's ion channels
let pith: Pith<carbon> = Pith::with_crystal(xtal);
```

---

## 4 — Atomic Surface Area Model

The scaffold's surface area is expressed in C• as its **binding capacity**: the number of
distinct signal channels it can hold open simultaneously.

```c-
// Surface area grows with depth — each layer multiplies binding sites by the branch factor
pith.surface_area()   // -> u64: total number of open binding sites
pith.binding_sites()  // -> Iterator<Site>: enumerate every open site
pith.bind(signal)     // -> Site: attach a signal to the next available site
```

Because the pith is "airy," the default branch factor is `8` — analogous to the eight-connected
atomic lattice of a cellulose microfibril.

---

## 5 — Relationship to the Language Runtime

The Universal Scaffold **is** the C• runtime heap. Every allocation returns a `Site` within the
global pith. Deallocation releases the site back to the scaffold for re-binding. There is no
traditional garbage collector; instead, sites decay back to the scaffold when their bound signal
has no remaining references — analogous to how spent nutrients are reabsorbed by the pith.

---

## See Also

- [Superior Pairings](superior-pairings.md) — pairing a scaffold with a conductor or mineral amplifier.
- [Ion-Channel Signaling](ion-channel-signaling.md) — how the scaffold routes frequency-tagged messages.
- [Betavoltaic Power](betavoltaic-power.md) — powering the scaffold from the ⁴⁰K trickle source.
