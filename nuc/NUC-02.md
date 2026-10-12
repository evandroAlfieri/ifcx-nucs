# NUC 2: Several parties building in parallel on incomplete, evolving and access-restricted data

**Original title:** Collaboration in a decentralized, low-trust data environment with evolving and partial information

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Organisations working on the same project rarely have the full picture: each sees only part of what the others hold, and some of what they share is still unfinished or changing. IFC has no room for that. A file must be complete and fully resolved before it is exchanged, so a designer has to finish a type before anyone else can use it, and data that only some recipients may see has no place in a valid file. When a type is used in many places, each placement also needs its own full copy of the type's parts, redefined by hand every time. Parties end up waiting for finished, fully open data before they can start, instead of building on what exists today.

## 2. What we want to achieve

- `W01` Two or more parties can author opinions about the same shared data at the same time.
- `W16` A party can share an incomplete definition, such as a type still being designed, and other parties can use it before it is complete, or create a more specific definition based on it, without modifying or taking ownership of the original.
- `W17` A definition, such as a type, a component assembly or a spatial subsection with its sub-components, structure, relationships and attributes, can be defined once and used wherever it is needed without being duplicated in every placement, and every use reflects a later change to it without being updated by hand. This includes the parts of a type appearing under every occurrence without being redefined at each placement.
- `W03` A party can add opinions to another party's objects, for example enrichments, status flags or approval notes, without modifying that party's layer, even when it has only read access or no authoring rights, such as a client. What it adds stays linked to those objects when they change, with no separate copy to keep in sync. *(see also NUC 1)*
- `W19` A party can decide which parts of its data each other party can see, and other parties can still use the objects and definitions that they see only in part. *(see also NUC 13)*
- `W04` All parties' layers can be composed into a single composed model.
- `W05` When a party changes its data, the change appears in the composed models and displays that use it, without a new file being sent, without manual re-assembly and without regenerating a separate visualisation file. *(see also NUC 13)*

## 3. IFCX capabilities

- `C01` **Separate contributions.** Each party's data is kept as a distinct unit that the party owns and can add to, change or withdraw without affecting any other party's data.
  *In this NUC: `W01`, `W03`*
- `C05` **Building on others' data.** A party can add to, annotate, specialise or, where it is responsible, replace another party's objects and definitions without changing the original.
  *In this NUC: `W16`, `W03`*
- `C09` **Reuse by definition.** A definition, such as a type, an assembly or a module, is stated once and used in many places; every use reflects changes to it, uses can be counted, and it can be used while still incomplete.
  *In this NUC: `W16`, `W17`*
- `C08` **Stable identity.** Every object has a globally unique identifier that stays the same across tools, organisations and its whole lifecycle, and conforming tools must preserve it.
  *In this NUC: `W03`*
- `C11` **Controlled access.** The owner of data decides which parts each other party can see and which it can change, and can withdraw that access later; data that is only partly visible remains usable.
  *In this NUC: `W19`*
- `C02` **On-demand composition.** The data of several parties can be combined into one composed model whenever needed, reflecting the current state of each party's data.
  *In this NUC: `W04`, `W05`*

## 4. What happens in IFC-STEP today

**STEP (language):**
- `SL04` EXPRESS supports optional, unset attribute values (the `$` placeholder in Part 21, `OPTIONAL` in the schema), so individual attributes can be left unspecified. What it has no concept of is an entity or type definition that is provisionally incomplete and expected to be extended by a different party later - every instantiated entity must still conform to a fully declared type known to the schema.

**IFC schema:**
- `IL04` IFC's schema defines a Type/Occurrence pattern (e.g. `IfcTypeObject` and its occurrences), but has no mechanism for instantiating a type's child parts under the corresponding occurrences.
- `IL05` IFC's specification describes property inheritance and override between a type and its occurrences only in prose, not as a formal schema rule, leading to inconsistent implementation across tools.
- `IL06` The IFC schema has no concept of higher-order typical objects (types of types).
- These are schema-formalisation gaps, not restrictions of the STEP/EXPRESS language, and could be addressed through schema changes.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Infrastructure corridor with partial visibility across asset owners

A highway authority, a utility company, and a rail operator are each responsible for different assets within the same physical corridor. Each party has full visibility of their own data and partial, read-only visibility of others. Under IFC, federation requires a coordinator to assemble a complete, fully-resolved file - every object fully defined, every relationship explicit - before any party can see the composed picture. Partial definitions or access-controlled data have no place in a valid IFC file. Under IFCX, each organisation publishes their dataset as a layer with explicit visibility boundaries. A drainage culvert defined by the highway authority is visible to the rail operator as a partially resolved object - its geometry present, its internal asset data withheld. Both parties work in parallel against a live composed model without either requiring full access to the other's definitions or waiting for a coordination export.

### 2. Evolving type definitions during design development

A facade engineer is developing a curtain wall system in parallel with the architect specifying individual panel placements. The type definition - glazing unit, framing profile, drainage detail - is incomplete and still evolving. Under IFC, an incomplete type cannot be validly exchanged: occurrences must resolve to a fully defined type, and children of a typical object are not automatically instantiated under its occurrences - they must be manually redefined at each placement. The architect cannot place instances of an evolving assembly without the facade engineer first completing and exporting a fully resolved definition. Under IFCX, the type tree is shared in its current partial state. The architect's instances inherit the current definition and automatically receive updates as the facade engineer refines it. Neither party blocks the other. When the glazing unit specification is finalised, all placements resolve to the updated definition without manual intervention.
