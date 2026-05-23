# Physics Foundations for the Open-Thermal-Monolith

This document provides a clear, precise explanation of the key physical mechanisms that underpin the monolith’s TPV receiver and emitter design. It is written to help you understand *why* certain architectural choices were made and to give you the language needed to discuss the design confidently with people who work deeply in near-field TPV, 2D materials, and high-temperature semiconductors.

The goal is not to make you an expert in every sub-field, but to give you solid, defensible understanding of the mechanisms that actually matter for this system.

---

## 1. Near-Field Radiative Heat Transfer and Polariton Hybridization

### Core Concept
In conventional (far-field) radiative heat transfer, the maximum heat flux between two bodies is limited by the blackbody (Planck) limit. When two surfaces are brought much closer than the peak thermal wavelength (sub-micron gaps), **evanescent waves** can tunnel across the gap. This enables **super-Planckian** (greater than blackbody) heat transfer.

### Why It Matters in the Monolith
Your TPV operates in the **near-field regime** (target 50–300 nm gap). The dominant mechanism is not propagating photons but **evanescent-wave tunneling** mediated by surface polaritons.

### Key Polaritons in the Design

| Polariton Type                    | Where It Lives                  | Role in the Monolith |
|-----------------------------------|----------------------------------|----------------------|
| **Surface Plasmon Polariton (SPP)** | Graphene (top layer on receiver) | Launches from the graphene and reaches across the gap |
| **Surface Phonon Polariton (SPhP)** | SiC skin (emitter)              | Strong mid-IR response from the laser-reacted SiC skin |
| **Hyperbolic Phonon Polariton (HPhP)** | BCN domains / hBN spacers     | Highly directional; enhances coupling and can guide modes |

**Hybridization** occurs when the graphene SPPs couple with the SiC/BCN SPhPs/HPhPs across the vacuum gap. This coupling dramatically increases the density of states available for photon tunneling, which is the main reason near-field flux can be 5–50× (or more) higher than far-field.

**What to say confidently**:  
“The performance gain comes primarily from polariton hybridization across the sub-micron gap. Graphene SPPs on the receiver couple with SPhPs/HPhPs from the SiC/BCN emitter, enabling super-Planckian radiative transfer that would be impossible in the far field.”

**Common pitfall to avoid**: Do not claim the system is “beating the blackbody limit” in a way that sounds like it violates thermodynamics. The enhancement is only possible because we are operating in the *near-field regime*, where the blackbody limit no longer applies in the same way.

---

## 2. SEG (Semiconducting Epigraphene) — Why It Is n-Type

SEG is the semiconducting buffer layer that forms on the Si-terminated face of SiC. It opens a \~0.6 eV bandgap while retaining very high mobility.

**Important point**: SEG is **natively n-type** even though both silicon and carbon are group IV elements. This is **not** conventional substitutional doping.

### Mechanism
When the first carbon layer grows on SiC, electrons spontaneously transfer from the polar SiC surface into the graphene buffer layer to help satisfy dangling bonds and screen the surface dipole. This leaves the SEG layer with excess electrons — i.e., **n-type** behavior.

This is an **interface-induced** doping effect, not impurity doping. It is reproducible and built into the growth on SiC.

**Why this matters for the TPV receiver**:
- It pairs naturally with **p-type (boron-doped) graphene** on top.
- The resulting Schottky barrier height can be tuned by doping the top graphene layer.
- No extra dopants are needed to make SEG n-type — it comes “for free” from the substrate interface.

**What to say confidently**:  
“SEG is n-type due to spontaneous charge transfer from the SiC substrate at the interface, not because of any difference in valence between silicon and carbon.”

---

## 3. Recombination, Collection Efficiency, and Spin Effects

In the graphene/SEG Schottky junction under high near-field flux:

- The dominant recombination mechanism is **Shockley-Read-Hall (SRH)** via defects and interface states.
- Radiative recombination is secondary because SEG is indirect-bandgap.
- **Spin selection rules** exist in principle for radiative recombination, but they have only a **minor secondary effect** in this system.

**Why spin is not a major factor**:
- SRH recombination (the main loss channel) is generally spin-independent or only weakly affected.
- SEG’s high mobility and thin active layer already enable efficient collection.
- At the high carrier generation rates present in near-field TPV, other effects (Auger, screening, defect density) dominate over spin considerations.

**Practical takeaway**:  
You do not need to engineer spin explicitly in the current design. The bigger levers are interface quality, barrier height tuning (via p-type graphene on top), and maintaining low defect density.

---

## 4. Mechanical Stability at Small Gaps (Casimir Forces)

At gaps below \~100–200 nm, the **Casimir force** (attractive quantum vacuum pressure) becomes measurable and can risk stiction.

**Why the monolith design remains stable**:
- Both the emitter (SiC skin) and receiver (graphene + SEG on SiC) are mechanically stiff materials.
- SiC has a very high Young’s modulus. Graphene is one of the stiffest materials known.
- The combination provides good resistance to local deformation or snap-in, even at 50–100 nm gaps.
- hBN-rich spacers (via EHD spray + shrinkage) can further help by adding repulsive or tunable Casimir-Lifshitz components in certain frequency ranges.

**What to say confidently**:  
“The stiff SiC substrate on the receiver and the laser-reacted SiC skin on the emitter, combined with graphene’s intrinsic stiffness, provide good mechanical robustness against Casimir forces at the target gap sizes.”

---

## 5. Why SEG + Boron-Doped Graphene on Top Is the Logical Combination

| Property                        | SEG (n-type)                     | Top Graphene (p-type, boron-doped) | Benefit |
|--------------------------------|----------------------------------|------------------------------------|---------|
| Bandgap                        | \~0.6 eV                         | —                                  | Good spectral match to 1414 °C emitter |
| Native doping                  | n-type (interface-induced)      | p-type (intentional)               | Creates useful Schottky barrier |
| Mobility                       | Very high                       | High                               | Efficient carrier collection |
| Work function tuning           | —                               | Tunable via boron doping           | Optimizes barrier height |

This combination gives:
- Better spectral matching than plain silicon (0.6 eV vs 1.12 eV)
- High collection efficiency from SEG’s mobility
- Tunable barrier height from doping the top graphene

---

## Summary — What Actually Moves Performance

For the TPV receiver, the highest-leverage physical mechanisms are:

1. **Polariton hybridization** across the near-field gap (biggest single gain).
2. **Spectral matching** via SEG’s 0.6 eV bandgap.
3. **High carrier mobility + quasi-ballistic transport** in SEG.
4. **Barrier height optimization** via p-type doping of the top graphene.
5. **Low defect density** at the graphene–SEG interface.
6. **Mechanical stiffness** of SiC + graphene for gap stability.

Spin effects, while physically real, are secondary compared with the above in this architecture.

---

