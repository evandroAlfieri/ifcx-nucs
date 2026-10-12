# NUC 7: Exchanging only what changed and applying it to an existing copy of the model

**Original title:** Standardised delta and incremental update exchange

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Construction and operation produce a steady stream of small changes: status updates, sensor readings, design revisions, as-built records. IFC can only exchange a complete file, and sending just what changed is not a supported concept, so even one changed attribute means a full re-export, and real-time workflows are hard to standardise. The re-federation that follows can take hours and hold up other coordination work. To report changes to individual objects, parties either re-export the whole model or keep a parallel spreadsheet that is reconciled with it by hand at milestones. Version control tools such as Git are a known weak point with large binary or composed files, and it is untested whether they suit large BIM datasets.

## 2. What we want to achieve

- `W12` A sender can send only the information added, changed or deleted since a previous state, down to a single attribute of one object, instead of the whole model, using the same tools it already uses to exchange complete models. *(see also NUC 6)*
- `W13` A receiver can bring its existing copy of a model up to date by applying changes alone, as each change arrives, without receiving the full dataset again or re-importing the whole model.
- `W14` A set of changes can be validated and read on its own, without the rest of the model; a receiver can see which objects the sender deleted; and a change can carry a link to external evidence, such as an inspection certificate. *(see also NUC 8)*
- `W02` A party's opinions do not alter another party's layer: each layer can be identified as a separate unit that only its party can change, and the party can edit or withdraw it without affecting any other party's layer. This includes a receiver withdrawing a set of changes it has applied to its copy, without affecting the rest of its copy. *(see also NUC 1)*
- `W15` Downstream processes, such as clash detection, can run on only the objects affected by a set of changes, without processing the whole model. *(see also NUC 3)*
- `W10` For any opinion in the composed model, and for any change exchanged, a user can identify which layer supplied it, which party owns that layer, when it was made, and which objects it affected. *(see also NUC 1)*
- `W11` An ordered sequence of exchanged changes can be replayed to reproduce any intermediate or final state of the model, and gives a timestamped record of every value written to each object's attributes.

## 3. IFCX capabilities

- `C06` **Change-only exchange.** Additions, changes and deletions since a previous state can be exchanged on their own, validated on their own, and applied to an existing copy with the same result as a full exchange.
  *In this NUC: `W12`, `W13`, `W14`, `W15`*
- `C10` **References.** Data can point to objects in other models and to external resources in a way any tool recognises, and the target of a reference can be reached (see Q49).
  *In this NUC: `W14`*
- `C01` **Separate contributions.** Each party's data is kept as a distinct unit that the party owns and can add to, change or withdraw without affecting any other party's data.
  *In this NUC: `W02`*
- `C04` **Provenance.** Every piece of information in a model can be traced to the party that stated it and to when it was stated.
  *In this NUC: `W10`, `W11`*
- `C07` **Change history.** Exchanged changes form an ordered, attributed history from which any earlier state can be reproduced.
  *In this NUC: `W11`*

**Not claimed**
- IFCX does not claim that its models work well in Git or similar general-purpose version control tools; the claim is limited to the replayable change history itself (`C07`), not any tool built on top of it.

## 4. What happens in IFC-STEP today

**STEP (language):**
- `SL12` No standardised delta format exists in the STEP/IFC ecosystem. STEP Part 21's #N instance numbering is local and ephemeral by design - tools routinely regenerate it on export - making file-to-file diffing unreliable as a basis for change detection regardless of schema.
- `SL13` In the classic Part 21 Edition 1/2 exchange structure, which must be self-contained, a file containing only changed entities is not structurally valid unless it also includes every entity those changed ones reference, in practice requiring most of the model. Edition 3's ANCHOR/REFERENCE mechanism (`SL02`, `SL03`, `SL11`) relaxes the self-containment requirement, but only at whole-entity granularity and with anchors nominated in advance, so it does not by itself provide a workable delta mechanism.
- `SL14` Standardised delta exchange is expected to stay difficult within STEP even with more recent STEP capabilities.

**IFC schema:**
- `IL11` `GlobalId` alone carries no information about what changed. `IfcOwnerHistory.ChangeAction` exists for this purpose, but it's optional, whole-object-level, and inconsistently populated in practice.
- `IL12` In the absence of a standardised IFC delta mechanism, practical approaches (BIMserver change detection, proprietary model-server delta APIs, external diffing of two full files) exist only as application-level workarounds, not standardised schema mechanisms.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Structural grid change propagated by sending only 12 changed nodes

A structural engineer shifts a column grid at Level 20 of a 40-storey tower. Under IFC, this change triggers a full model re-export, redistribution to all disciplines, re-import, and clash detection cycle - a process that takes hours and blocks other coordination work. Under IFCX, the engineer pushes a layer containing only the 12 modified nodes: the affected columns, their updated placements, and the revised grid reference. The architectural tool consumes the layer within minutes. The CI/CD pipeline runs clash detection on only the affected elements. The change is fully attributed: author, timestamp, and the specific nodes modified.

### 2. Per-object as-built status updates from a site app

A civil contractor installs 47 of 200 piles in a single day. Each installation is recorded by a lightweight site app that pushes a minimal layer per pile: status changed to installed, date, inspector ID, and a URI to the linked inspection certificate. The client's platform aggregates these layers in real time. No full model re-export is required; no spreadsheet reconciliation follows. The live record of installed versus planned piles is always current. Under IFC, transmitting the same information requires either a full IFC re-export or a parallel spreadsheet that must be manually reconciled with the model at milestone intervals.

### 3. Incremental IoT attribute writes as minimal layers

A building management system writes energy meter readings against HVAC nodes every 15 minutes. Each write is a minimal IFCX layer: one node, one updated attribute, one timestamp. The FM platform applies each layer to its live model state. The audit trail of attribute changes is the history of these layers - a complete, timestamped record of every value every sensor ever wrote to every node. Under IFC, there is no mechanism for any external system to transmit even a single attribute update to a specific model object without producing a new complete file export.
