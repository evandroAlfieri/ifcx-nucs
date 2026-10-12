# IFCX NUC: not-use-cases for the new IFC standard

A small, articulated list of *not-use-cases* (NUCs) for the new IFC standard (IFC 5 / IFCX), based on API-first, AI- and cloud-enabled workflows. Each NUC describes one problem that today's IFC-STEP does not solve well, what parties want to achieve, and the capabilities IFCX would need to offer.

This folder (`/nuc`) holds the NUCs and the documents that keep them consistent. This file is the entry point.

**Contents**

1. [NUCs](#nucs)
2. [IFC 4.3 and IFCX concepts](#ifc-43-and-ifcx-concepts)
3. [Register](#register)
4. [Glossary](#glossary)
5. [Open questions](#open-questions)
6. [Reading a NUC](#reading-a-nuc)
7. [Capabilities across NUCs](#capabilities-across-nucs)
8. [Other files](#other-files)
9. [Instructions for writing a NUC](#instructions-for-writing-a-nuc)

---

## NUCs

| # | NUC | Original title | Capabilities |
|---|---|---|---|
| 1 | [Multi-organisation parallel authoring without overwriting, with traceable layers](NUC-01.md) | Layered collaborative authoring with non-destructive overrides definition | C01–C05, C08 |
| 2 | [Several parties building in parallel on incomplete, evolving and access-restricted data](NUC-02.md) | Collaboration in a decentralized, low-trust data environment with evolving and partial information | C01, C02, C05, C08, C09, C11 |
| 3 | [Retrieving only the parts of a model a user or tool needs](NUC-03.md) | In-browser streaming and selective node loading | C06, C10, C12, C14 |
| 4 | [Any organisation adding its own typed data without changing the core schema](NUC-04.md) | Third-party typed domain extensions without schema governance | C13, C15 |
| 5 | [Rendering models in game engines and web viewers without a geometry kernel](NUC-05.md) | Direct integration with game engine and web rendering pipelines | C02, C12, C14, C16 |
| 6 | [Keeping each object's identifier stable across tools, organisations and the whole lifecycle](NUC-06.md) | Stable object identity through the full asset lifecycle | C06, C08, C10 |
| 7 | [Exchanging only what changed and applying it to an existing copy of the model](NUC-07.md) | Standardised delta and incremental update exchange | C01, C04, C06, C07, C10 |
| 8 | [Linking model data to external resources through typed, recognisable references](NUC-08.md) | Dereferenceable semantic linking to external data | C06, C10, C12, C13 |
| 9 | [Defining an assembly once and reusing it everywhere, with changes reaching every occurrence](NUC-09.md) | Formal assembly type instantiation | C09, C10, C12 |
| 10 | [Organising the same data in several structures, none of them canonical](NUC-10.md) | Arbitrary spatial structures | C05, C17 |
| 11 | [Placing objects relative to a chosen basis, with intent and tolerances explicit](NUC-11.md) | Goal-specific relative placement | C05, C17, C18 |
| 12 | [Developing design alternatives that share common data without copying it](NUC-12.md) | First-class options without duplication | C01–C03, C05, C07, C12, C17 |
| 13 | [Using other parties' data at its source, live or at a fixed version, without copies](NUC-13.md) | Reference-first distributed access | C01, C02, C04, C05, C08, C10–C13, C17 |

NUC 10–13 were added after NUC 1–9 and follow provisional rules (see the [open questions](open-questions.md)). Whether some NUCs should be split or merged (NUC 13 is the largest; NUC 1 and NUC 2 overlap) is still open: Q02 and Q03.

New NUCs start from [NUC-TEMPLATE.md](NUC-TEMPLATE.md).

---

## IFC 4.3 and IFCX concepts

[**IFC4x-IFC5-constructs.md**](IFC4x-IFC5-constructs.md) answers a different question from the NUCs. The NUCs describe what IFCX should do *better* than IFC. This document checks that IFCX does not lose anything IFC 4.3 does today.

It is organised by **concept**: something a model can represent, such as identity, placement, material association or georeferencing, stated without saying how. For each concept it gives the **mechanism** on both sides (an entity, attribute or `IfcRel*` relationship in IFC 4.3; a rule or structure of the format in IFCX) and whether the current prototype ("Alpha") supports it: yes, partly or no. A section on how Alpha encodes some IFC concepts, and a worked walk through an `IfcDoor`, complete it.

The document is a draft for review by the group. It has no IDs of its own, and it is not an input for writing a NUC. Its verdicts may be preliminary (Q30), and the NUCs that would show IFCX keeps what IFC 4.3 does are not written yet (Q48).

---

## Register

[**register.md**](register.md) is the single list of every tagged item used across the NUCs: wants (`W01`–`W43`, in 14 themes), capabilities (`C01`–`C18`), mechanisms (`M01`–`M21`, in seven families), and the STEP and IFC limitations. It records which NUCs use each item and which wants each capability answers. When the same statement appears in several NUCs, it has one ID and one wording here.

Mechanisms (`M`) describe *how* IFCX could deliver a capability. They live only in the register, never in a NUC. Each one records its source (Alpha, proposed in a NUC, or both) and what the prototype does today, with links to the evidence pinned to a commit. Behaviour checked by running the reference implementation is in [alpha-probes.md](alpha-probes.md).

Use the register to find where an item is used, to check that a want is answered by a capability, and to spot overlap between NUCs.

## Glossary

[**glossary.md**](glossary.md) defines the tags and the terms the NUCs use (for example *layer*, *opinion*, *composed model*, *precedence*) and the rules for using them, including the cases when several parties address the same object (enrichment, alternative, replacement, conflict), the retired terms and the terms to avoid. *Layer* and *opinion* are provisional and planned to be renamed *contribution* and *statement* after the group review (Q17). If a NUC uses a term in a different sense, the NUC is wrong or the glossary needs a question raised.

## Open questions

[**open-questions.md**](open-questions.md) holds everything still to be decided about the NUCs, the register, the glossary and the writing process.

- Questions have permanent IDs (`Q02`, `Q03`, …) and are grouped by topic, with an index at the top.
- Each records where it was raised, which items and files it affects, and its status. Resolved questions move to a *Resolved* section with how they were resolved.
- A question that exists only in a chat or a review report is lost, so every new question is added to this file.

---

## Reading a NUC

Every NUC has the same five sections:

1. **Current workflow and problem:** one short paragraph of plain prose on how work is done today and why that is a problem. It has no tags.
2. **What we want to achieve:** wants (`W`), each testable on its own and independent of any solution.
3. **IFCX capabilities:** capabilities (`C`), each listing the wants of that NUC it answers, plus any *Not claimed* bullets that limit the claim.
4. **What happens in IFC-STEP today:** limitations of the STEP language (`SL`) and of the IFC schema (`IL`).
5. **Example scenarios:** illustrations. They may describe solution-specific mechanisms to stay realistic; the final mechanism may differ.

Tags:

| Tag | Meaning |
|---|---|
| `W##` | Want: something a party wants to be able to do |
| `C##` | IFCX capability answering one or more wants |
| `M##` | Mechanism: how a capability could be delivered (register only, never in a NUC) |
| `SL##` | Limitation of the STEP language |
| `IL##` | Limitation of the IFC schema or its implementation |
| `Q##` | Open question, tracked in [open-questions.md](open-questions.md) |

*Not claimed* bullets carry no ID: each states what IFCX does not promise in that NUC and names the capability it limits. Assumptions are no longer tagged; they are part of the section 1 paragraph.

IDs are shared across NUCs: the same ID always means the same statement. The numbers imply neither order nor priority.

---

## Capabilities across NUCs

The capabilities that recur across NUCs. The [register](register.md) is authoritative for their wording, their mechanisms and the wants each one answers.

| ID | Capability | NUCs |
|---|---|---|
| `C01` | Separate contributions | 1, 2, 7, 12, 13 |
| `C02` | On-demand composition | 1, 2, 5, 12, 13 |
| `C03` | Precedence | 1, 12 |
| `C04` | Provenance | 1, 7, 13 |
| `C05` | Building on others' data | 1, 2, 10, 11, 12, 13 |
| `C06` | Change-only exchange | 3, 6, 7, 8 |
| `C07` | Change history | 7, 12 |
| `C08` | Stable identity | 1, 2, 6, 13 |
| `C09` | Reuse by definition | 2, 9 |
| `C10` | References | 3, 6, 7, 8, 9, 13 |
| `C11` | Controlled access | 2, 13 |
| `C12` | Published data | 3, 5, 8, 9, 12, 13 |
| `C13` | Self-describing data | 4, 8, 13 |
| `C14` | Selective access | 3, 5 |
| `C15` | Open extension | 4 |
| `C16` | Render-ready geometry | 5 |
| `C17` | Purpose-specific arrangements | 10, 11, 12, 13 |
| `C18` | Placement intent | 11 |

---

## Other files

Working material behind the NUCs. It is not part of the NUCs themselves.

| File | Content |
|---|---|
| [NUC-TEMPLATE.md](NUC-TEMPLATE.md) | Template for writing a new NUC |
| [alpha-probes.md](alpha-probes.md) | Checks of what the IFCX prototype (Alpha) does today, referenced by the register |

---

## Instructions for writing a NUC

[**nuc-rewrite-instructions.md**](nuc-rewrite-instructions.md) holds the instructions for writing a NUC, whether new or rewritten from the original list: the inputs to read first (glossary, register, open questions, the concepts comparison, the template and two reference NUCs), the structure of a NUC, the steps from tagging and rewording to reusing register items, and the report a reviewer receives. Follow them when writing or changing a NUC, so all NUCs keep the same structure and wording rules.
