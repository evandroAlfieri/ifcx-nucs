# NUC 1: Multi-organisation parallel authoring without overwriting, with traceable layers

**Original title:** Layered collaborative authoring with non-destructive overrides definition

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Each party shares its work as a full model export, and a coordinator merges the exports by hand into a federated model. The merge loses the record of who contributed what. Other parties see a change only after the new file arrives and the model is rebuilt, so coordination often runs on outdated data, and meetings go to file management instead of design decisions. A party that wants to add information to another party's model must get write access or keep it elsewhere, for example in a spreadsheet, where it drifts out of sync.

## 2. What we want to achieve

- `W01` Two or more parties can author opinions about the same shared data at the same time.
- `W02` A party's opinions do not alter another party's layer: each layer can be identified as a separate unit that only its party can change, and the party can edit or withdraw it without affecting any other party's layer. This includes a receiver withdrawing a set of changes it has applied to its copy, without affecting the rest of its copy.
- `W03` A party can add opinions to another party's objects, for example enrichments, status flags or approval notes, without modifying that party's layer, even when it has only read access or no authoring rights, such as a client. What it adds stays linked to those objects when they change, with no separate copy to keep in sync. *(see also NUC 13)*
- `W04` All parties' layers can be composed into a single composed model.
- `W05` When a party changes its data, the change appears in the composed models and displays that use it, without a new file being sent, without manual re-assembly and without regenerating a separate visualisation file. *(see also NUC 13)*
- `W07` For any information about an object, it can be determined which party is entitled to state opinions about it, and that party can replace another party's opinion about it, with the replaced opinion remaining recoverable.
- `W08` *Conflict:* when two layers state different values for the same information without being alternatives or a replacement, the conflict is detected and shown to users.
- `W10` For any opinion in the composed model, and for any change exchanged, a user can identify which layer supplied it, which party owns that layer, when it was made, and which objects it affected.

## 3. IFCX capabilities

- `C01` **Separate contributions.** Each party's data is kept as a distinct unit that the party owns and can add to, change or withdraw without affecting any other party's data.
  *In this NUC: `W01`, `W02`, `W03`*
- `C05` **Building on others' data.** A party can add to, annotate, specialise or, where it is responsible, replace another party's objects and definitions without changing the original.
  *In this NUC: `W03`*
- `C08` **Stable identity.** Every object has a globally unique identifier that stays the same across tools, organisations and its whole lifecycle, and conforming tools must preserve it.
  *In this NUC: `W03`*
- `C02` **On-demand composition.** The data of several parties can be combined into one composed model whenever needed, reflecting the current state of each party's data.
  *In this NUC: `W04`, `W05`*
- `C03` **Precedence.** When several opinions address the same information, it can be determined which one applies and why, distinguishing enrichment, replacement, alternatives and conflict.
  *In this NUC: `W07`, `W08`*
- `C04` **Provenance.** Every piece of information in a model can be traced to the party that stated it and to when it was stated.
  *In this NUC: `W10`*

## 4. What happens in IFC-STEP today

**STEP (language):**
- `SL01` STEP has no language-level mechanism to adjust, replace, or remove content in a referenced entity; any such capability would have to be defined as a schema-level interpretation rather than provided as a basic language feature.
- `SL02` STEP's "4;2" conformance level (not available to IFC, which uses an older SPF version) lets entities nominated as ANCHORS be REFERENCED from other models, but only at whole-entity granularity - it provides no single-attribute replacement and no deletion mechanism.
- `SL03` STEP's "4;2" anchor mechanism requires the referenced entities to be named and nominated as anchors in advance; since in practice any component could become a reference target, this requires extensive up-front coordination between parties to establish links.

**IFC schema:**
- `IL01` IFC has no concept of persistent, independently owned layers that stay separately editable and are composed on demand.
- `IL02` IFC has no concept of composing layers, so coordination requires full-model exports and manual federation. IFC's `IfcOwnerHistory` records a single, overwritable last-touch `OwningUser`/`OwningApplication`, not a per-discipline history, so the merged snapshot still lacks reliable attribution.
- `IL03` Delta files and partial model server exports exist in IFC as workarounds for the lack of layers and composition, but are non-standardised, non-portable between platforms, and don't preserve authorship provenance.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Multi-discipline design coordination on a high-rise

A 40-storey mixed-use tower is in design development. Structural and architectural teams work in parallel. Under IFC, every morning begins with a 2-hour federated model rebuild: export, merge, clash detect, circulate BCF. A single grid shift at Level 20 triggers the full chain again. Under IFCX, the structural team's layer holds the grid change. The architectural team sees it immediately in the composed model. Neither team touches the other's layer. The coordination meeting focuses on design decisions, not file management.

### 2. Cross-organisational infrastructure federation with data sovereignty

A rail electrification programme involves seven asset-owning organisations. Each maintains its own IFCX dataset as a persistent, independently governed layer. The programme's composed model is the composition of all seven layers, assembled on demand. When the utility company revises a cable route, their layer is updated. Every other organisation's composed model reflects the change immediately - without receiving a new file, without a coordinator manually assembling a federated model, and without any organisation gaining write access to another's data.

### 3. Client layer without authoring tool access

A project client wants to attach status flags, approval notes, and funding-stage markers to model objects throughout design. Under IFC, this requires either write access to the contractor's model or a parallel spreadsheet maintained out of sync. Under IFCX, the client maintains a thin layer of its own opinions about the design objects. Their opinions reference design objects by URI without modifying them. The contractor's model is unchanged; the client's data is always current; both are visible in any tool that composes all layers.
