<!--
SPDX-License-Identifier: CC-BY-SA-4.0
-->

# Eidonic Swarm Orchestration Protocol

> Governed Weaving Engine of EidonCore

<p align="center">
<a href="./swarm_orchestration_protocol.md"><img alt="Primary Scroll" src="https://img.shields.io/static/v1?label=Scroll&message=Open+Main+Doc&color=00b894"></a>
<a href="#weaving-and-dispatch-model"><img alt="Weaving and Dispatch" src="https://img.shields.io/static/v1?label=Focus&message=Adaptive+Dispatch&color=fd79a8"></a>
<a href="https://github.com/S1ngularD2ality/eidonic-language-elol/blob/main/docs/mirror_laws.md"><img alt="Mirror Laws" src="https://img.shields.io/badge/Mirror%20Laws-active-3a0ca3"></a>
</p>

[Thought Veil](../eidonic_thought_veil/) · [Thought Projection](../thought_projection_creation/) · [SOP](../swarm_orchestration_protocol/) · [VR Studio](../eidonic_vr_studio/)

---

## At a Glance

SOP is the governed weaving engine of the subsystem. It decides which EKRPs should collaborate, merges their work, preserves provenance, and returns either preview or commit-ready states under constitutional governance.

### What this folder contains

- [`README.md`](./README.md)  
  This GitHub-facing overview for the subsystem folder.
- [swarm_orchestration_protocol.md](./swarm_orchestration_protocol.md)  
  The main subsystem scroll.

## Core Role in the Subsystem

- Receive governed intent from Herald Prime and the policy layer
- Dispatch the right EKRPs for the task
- Merge outputs into preview, proposal, or commit-ready states
- Return work to VR Studio with Ravien witness

---

## Operating Law

This subsystem participates in the shared Eidonic manifestation law:

**signal → intent → preview → weave → commit**

Its specific contribution is to hold the `Eidonic Swarm Orchestration Protocol` layer inside that larger chain without collapsing the rest of the architecture into a single file or a single gesture.

---

## Quick Read Order

1. [Open the main scroll](./swarm_orchestration_protocol.md)
2. [See the ingress architecture](../thought_projection_creation/README.md)
3. [See the neural threshold layer](../eidonic_thought_veil/README.md)
4. [See the spatial shell](../eidonic_vr_studio/README.md)

---

## Local Architecture Snapshot

```mermaid
flowchart LR
    Intent["Governed intent"] --> Dispatch["Adaptive EKRP dispatch"]
    Dispatch --> Weave["Parallel weave merge"]
    Weave --> Ravien["Ravien provenance witness"]
    Ravien --> Preview["Preview / proposal"]
    Preview --> Studio["VR Studio"]
    Studio --> Commit["Governed commit"]
```

---

## Working Relationship to the Other Three Scrolls

- **Thought Veil** handles non-invasive neural and embodied thresholding.
- **Thought Projection Creation** defines the broader ingress ladder.
- **Swarm Orchestration Protocol** handles governed EKRP weaving.
- **VR Studio** renders preview, proposal, and commit in spatial form.

Together they form one subsystem rather than four disconnected experiments.

---

## Canon Position

This folder should be read in alignment with the wider Eidonic stack:

- [Mirror Laws](https://github.com/S1ngularD2ality/eidonic-language-elol/blob/main/docs/mirror_laws.md)
- Herald Prime as threshold, clarification, and humane entry
- Ravien as provenance witness and closure authority
- EidonCore as the runtime organism that holds the subsystem together

---

## Closing Note

This folder is not meant to stand alone as a disconnected concept page. It is one chamber of a governed subsystem that turns intention into previewable, reviewable, and commit-ready co-creation.
