# Ion-Channel Signaling — Frequency Programming Model

C• programs communicate not through traditional function calls or message queues, but through
**frequency-encoded ion channels** — an abstraction drawn directly from how plants transmit
information through their phloem and xylem networks.

---

## 1 — Biological Basis

Plants communicate through two mechanisms:

1. **Electrical pulses** — rapid voltage waves that travel along plasma membranes (analogous to
   action potentials in animal neurons).
2. **Chemical codes** — small organic molecules (sugars, hormones, peptides) that encode
   "instructions" for distant cells.

The phloem — the plant's sugar-transport highway — acts as an internal internet: it carries both
the nutrients *and* the signaling molecules that tell cells what to produce next.

To **program** this network, you do not use text commands; you use **frequency**. If you expose
the pith to an EM frequency matched to the resonant size of a target molecule (e.g. a sugar
molecule at ~10 GHz in the microwave range), the plant's cells receive a "prioritise this
molecule" instruction through their ion channels.

---

## 2 — Ion Channels in C•

An **ion channel** in C• is a typed, frequency-gated message bus:

```c-
use signals::IonChannel;
use signals::Frequency;

// Open a channel tuned to the sugar-molecule resonance frequency
let sugar_channel: IonChannel<hydrogen> = IonChannel::open(
    frequency: 10.ghz,
    molecule:  "amylase",
);

// Send a "prioritise citric acid" instruction on this channel
sugar_channel.send(Signal {
    instruction: "prioritise",
    target:      "citric_acid",
    suppress:    "amylase",
});
```

The runtime will only deliver the signal to receivers whose declared resonance frequency matches
the channel's tuned frequency (within a configurable tolerance band, default ±1%).

---

## 3 — Programming Flavours

The problem statement's example of "programming" a banana to produce citric acid (orange
flavour) instead of amylase (banana starch flavour) maps directly to ion-channel signaling:

```c-
use scaffold::Pith;
use signals::{IonChannel, FrequencyTable};
use pairings::PotassiumSalt;

// Step 1 — create a scaffold paired for nutrient signaling
let scaffold = Pith::<nitrogen>::new().pair(PotassiumSalt);

// Step 2 — look up the resonance frequency for the sugar molecule we want to suppress
let banana_freq: Frequency = FrequencyTable::lookup("amylase");       // -> ~9.8 GHz
let citrus_freq: Frequency = FrequencyTable::lookup("citric_acid");   // -> ~10.2 GHz

// Step 3 — open channels for each and send competing signals
let suppress = IonChannel::open(frequency: banana_freq, molecule: "amylase");
let boost    = IonChannel::open(frequency: citrus_freq, molecule: "citric_acid");

suppress.send(Signal::inhibit());
boost.send(Signal::amplify(gain: 2.0));

// Step 4 — bind both channels to the scaffold so they persist
scaffold.bind(suppress);
scaffold.bind(boost);
```

---

## 4 — The Frequency Table

C• ships with a built-in `FrequencyTable` that maps common bio-molecules to their EM resonance
frequencies. Users can extend it with custom entries:

```c-
FrequencyTable::register("vanillin", resonance: 11.4.ghz, element: carbon);
```

---

## 5 — Phloem Topology

The C• runtime models the phloem as a **directed acyclic graph (DAG)** of ion channels. Signals
flow from source nodes (roots, where energy enters) to sink nodes (leaves, where energy is
consumed). The scaffold's crystal frequency sets the **clock rate** of this DAG — analogous to
the quartz oscillator in a CPU.

```c-
// Inspect the current phloem topology
let phloem = runtime::phloem();
phloem.sources()   // -> Vec<Node>
phloem.sinks()     // -> Vec<Node>
phloem.path_from(source, sink)  // -> Option<Vec<Channel>>
```

---

## 6 — Security Model

Because channels are frequency-gated, an attacker cannot inject a signal on a channel without
knowing (or guessing) the exact resonance frequency. The default channel key space is 2⁶⁴
discrete frequencies in the range 1 Hz – 300 GHz, giving adequate brute-force resistance for
most implant or seed-programming use cases.

---

## See Also

- [Universal Scaffold](pith-scaffold.md)
- [Superior Pairings](superior-pairings.md)
- [Betavoltaic Power](betavoltaic-power.md)
