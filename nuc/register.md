# IFCX NUC Register

The single list of all wants, capabilities, mechanisms and limitations used across NUCs.

- **Before writing or rewriting a NUC**, check this register. If an item with the same meaning already exists, reuse its ID and its exact wording. Do not redefine it.
- **After writing or rewriting a NUC**, update this register: add new items, and add the NUC to the *Used in* column of every item it uses.
- Terms follow [glossary.md](glossary.md).
- The comparison with IFC 4.3 is in [IFC4x-IFC5-constructs.md](IFC4x-IFC5-constructs.md); it has no IDs of its own.
- **Merging overlapping items:** keep the most generic statement as the main text, and add the more specific one as a specification, an example or an "includes" clause. Every NUC using a merged item is updated. When two capabilities merge, the surviving one lists the mechanisms of both, and its *In Alpha* result is judged again.

---

## Wants (`W`)

Needs or requirements, grouped by theme. The number is only an identifier: it implies neither order nor priority. Every want must be testable and solution-neutral (see glossary).

### Separate contributions

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W01` | Two or more parties can author opinions about the same shared data at the same time. | NUC 1, NUC 2 | C01 |
| `W02` | A party's opinions do not alter another party's layer: each layer can be identified as a separate unit that only its party can change, and the party can edit or withdraw it without affecting any other party's layer. This includes a receiver withdrawing a set of changes it has applied to its copy, without affecting the rest of its copy. | NUC 1, NUC 7 | C01 |
| `W03` | A party can add opinions to another party's objects, for example enrichments, status flags or approval notes, without modifying that party's layer, even when it has only read access or no authoring rights, such as a client. What it adds stays linked to those objects when they change, with no separate copy to keep in sync. | NUC 1, NUC 2, NUC 13 | C01, C05, C08 |

### Composition and currency

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W04` | All parties' layers can be composed into a single composed model. | NUC 1, NUC 2 | C02 |
| `W05` | When a party changes its data, the change appears in the composed models and displays that use it, without a new file being sent, without manual re-assembly and without regenerating a separate visualisation file. | NUC 1, NUC 2, NUC 5, NUC 13 | C02 |
| `W06` | A third party can compose data from several independent sources, together with its own additions, which can stay private, without copying the sources and without the sources knowing about each other or about the composition. | NUC 13 | C02, C10, C17 |

### Precedence

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W07` | For any information about an object, it can be determined which party is entitled to state opinions about it, and that party can replace another party's opinion about it, with the replaced opinion remaining recoverable. | NUC 1 | C03 |
| `W08` | *Conflict:* when two layers state different values for the same information without being alternatives or a replacement, the conflict is detected and shown to users. | NUC 1 | C03 |
| `W09` | A user or tool can tell whether two compositions are alternatives that coexist or successive versions of the same data. | NUC 12 | C03, C07 |

### Provenance and history

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W10` | For any opinion in the composed model, and for any change exchanged, a user can identify which layer supplied it, which party owns that layer, when it was made, and which objects it affected. | NUC 1, NUC 7 | C04 |
| `W11` | An ordered sequence of exchanged changes can be replayed to reproduce any intermediate or final state of the model, and gives a timestamped record of every value written to each object's attributes. | NUC 7 | C04, C07 |

### Change-only exchange

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W12` | A sender can send only the information added, changed or deleted since a previous state, down to a single attribute of one object, instead of the whole model, using the same tools it already uses to exchange complete models. | NUC 6, NUC 7, NUC 8 | C06 |
| `W13` | A receiver can bring its existing copy of a model up to date by applying changes alone, as each change arrives, without receiving the full dataset again or re-importing the whole model. | NUC 7 | C06 |
| `W14` | A set of changes can be validated and read on its own, without the rest of the model; a receiver can see which objects the sender deleted; and a change can carry a link to external evidence, such as an inspection certificate. | NUC 7, NUC 8 | C06, C10 |
| `W15` | Downstream processes, such as clash detection, can run on only the objects affected by a set of changes, without processing the whole model. | NUC 3, NUC 7 | C06 |

### Reuse by definition

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W16` | A party can share an incomplete definition, such as a type still being designed, and other parties can use it before it is complete, or create a more specific definition based on it, without modifying or taking ownership of the original. | NUC 2 | C05, C09 |
| `W17` | A definition, such as a type, a component assembly or a spatial subsection with its sub-components, structure, relationships and attributes, can be defined once and used wherever it is needed without being duplicated in every placement, and every use reflects a later change to it without being updated by hand. This includes the parts of a type appearing under every occurrence without being redefined at each placement. | NUC 2, NUC 9 | C09 |
| `W18` | A user can find out how many occurrences of each type a model contains, without counting them by hand. | NUC 9 | C09 |

### Access

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W19` | A party can decide which parts of its data each other party can see, and other parties can still use the objects and definitions that they see only in part. | NUC 2, NUC 13 | C11 |
| `W20` | A data owner can give another party read access without write access or ownership, and can later withdraw that access. | NUC 13 | C11 |

### Identity

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W21` | An object keeps one globally unique identifier through its whole lifecycle, so that identifiers from different projects and organisations do not collide, including when the object is modified, moved to a different parent, re-exported, combined into a larger model or handed over to another tool or organisation, and a party can rely on every tool to keep it, so that identity does not depend on one tool's behaviour. Information any party records about the object at any stage, such as as-built status or asset data at handover, stays attached to that same object, without lookup tables, manual matching or reconciliation. | NUC 6 | C08 |
| `W22` | References to an object made by other tools and organisations, such as BCF issues, IDS reports and asset register entries, keep resolving to that object throughout its lifecycle. | NUC 6 | C08, C10 |

### References

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W23` | An attribute value can be declared to be a reference to an external resource, such as a classification entry, product data, a certification, a facility management record or a sensor endpoint, so that any tool can tell a reference from ordinary text and recognise what kind of resource it points to. | NUC 8 | C10, C13 |
| `W24` | A user or tool holding a reference to an object in another model, or to an external resource, can follow it and read the target's current content from its source at any time, without the model being updated when the target changes, for example a work task reading the areas and colour of the walls it concerns, or a third-party platform following references to compile a material passport that stays traceable to its sources. | NUC 8, NUC 13 | C10, C12 |
| `W25` | At handover, a receiving system can take over a model directly and check that every external reference in it resolves and every classification is valid against its source, without a separate spreadsheet or manual data entry. | NUC 8 | C13 |

### Published data

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W26` | An organisation can publish its data, such as a dataset or a manufacturer's product types, so that other parties and their tools use it directly at its source instead of holding copies, and see its current state, for example new or updated products when they are released, without static exports, imports or separate data transfers. A manufacturer can also learn which of its types a design uses, without a separate data transfer. | NUC 3, NUC 9, NUC 13 | C10, C12 |
| `W27` | External systems, such as building management systems or IoT controllers, can write data, such as readings and fault statuses, directly to specific objects in a model, and several authorised platforms can read that same current data. | NUC 5, NUC 13 | C12 |
| `W28` | A reference to a source dataset can follow the source's current state or stay on a fixed version of it, as chosen by the party making the reference. | NUC 12, NUC 13 | C12 |
| `W29` | A local copy of another party's data is never silently treated as current: a consumer keeps track of where each piece of data came from and can check its copy against the source. | NUC 13 | C04, C12 |

### Open and self-describing data

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W30` | Systems from different vendors can exchange data with a model without bespoke integration or vendor-specific mapping. | NUC 13 | C13 |
| `W31` | Any organisation can define its own typed attributes, own and maintain their definition, and attach them to any object, without changing the core schema, without approval from a standards body, and without conflicting with attributes defined by other organisations on the same object. | NUC 4 | C15 |
| `W32` | A tool that does not understand an organisation's attributes can still read the rest of the model, ignoring those attributes without failing. | NUC 4 | C15 |
| `W33` | A tool that understands an organisation's attributes can check their values against that organisation's definition, including their data types, and data requirements, such as an IDS specification, can refer to both core and organisation-defined attributes, so that a model is checked automatically, including the type and meaning of values, not only their presence. | NUC 4 | C13, C15 |

### Selective access

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W34` | A user or tool can retrieve a specific part of a model, such as a single object, a storey with everything in it, or all objects of one system, and can load a model progressively, showing a first part, such as the spatial structure, and fetching further parts only when they are needed, without downloading or reading the rest of the model. | NUC 3 | C14 |
| `W35` | A tool can read model data with ordinary web technology, such as a web browser, without dedicated middleware or pre-processing. | NUC 3, NUC 5 | C14 |

### Geometry

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W36` | A game engine or web renderer can display a model's geometry with only a thin import step, without a geometry kernel. | NUC 5 | C16 |
| `W37` | In a rendered display, a user can select an object and read its model data, such as its classification and properties, because the rendered object stays linked to that data. | NUC 5 | C16 |

### Arrangements and placement

| ID | Statement | Used in | Addressed by |
|---|---|---|---|
| `W38` | Different parties can each organise the same data in their own arrangement, such as a navigation structure, or a placement relative to world coordinates, a wall, a floor, connected equipment, an alignment or a surveyed object, with no arrangement treated as the authoritative shape of the data, and a user or tool can choose which arrangement to use, or create its own. | NUC 10, NUC 11 | C17 |
| `W39` | A party can create an arrangement over data owned by others, such as a structure, a placement scheme or an option, or change its own and keep earlier ones for comparison, without copying or modifying that data or another party's arrangement, and without write access to the data. An option can add alternative data of its own, and defining which objects belong to it does not require changing them. | NUC 10, NUC 11, NUC 12 | C05, C17 |
| `W40` | A user or tool can select an option, obtain its complete composed model, and switch between options. Data common to several options is stored once and shared by them, only the data that differs being added, replaced or omitted per option. Several options can be developed at the same time as the current state of the data, without invalidating or rewriting it, and an option can be discarded without affecting its sources. | NUC 12 | C01, C02, C17 |
| `W41` | Users and tools can compare options and see which data they share and where they differ. | NUC 12 | C17 |
| `W42` | For any placement, a user or tool can read what it is relative to, the rule or tolerance behind it, and whether it was set directly, set relative to another object, or derived from relationships or constraints, so that everyone resolving it arrives at the same position. | NUC 11 | C18 |
| `W43` | When one placement changes, for example after a survey, its effect on the placements that depend on it can be evaluated against stated tolerances and clearances before work continues. | NUC 11 | C18 |

---

## Capabilities (`C`)

A capability is an **ability IFCX provides**, stated without saying how. Each one answers several wants and is more general than any of them; how IFCX delivers it is described by mechanisms (`M`: in Alpha, proposed by the NUCs, or both) and, once decided, ADRs. A new NUC maps its wants to these capabilities and proposes a new one only when none fits.

In a NUC, a capability is written as its name in bold followed by the statement: **Name.** Capability.

Each capability has a short table of the wants it **answers**, the NUCs it is **used in**, and whether it is **in Alpha**: yes, partial (with the reason) or no, at the commits named in the Mechanisms section, or *not checked* for a capability added since the last check (see Q30). The results were derived from the previous capability list on 28 Sep and are to be confirmed (Q30). "No" means not in Alpha, not impossible.

A second table lists the **mechanisms** that could deliver the capability. Mechanisms listed under *Alternative to* are alternatives: an ADR chooses between them. The others are complementary: independent decisions that work together. This is the only place where capabilities and mechanisms are linked.

### `C01` Separate contributions

Each party's data is kept as a distinct unit that the party owns and can add to, change or withdraw without affecting any other party's data.

| Answers | Used in | In Alpha |
|---|---|---|
| `W01`, `W02`, `W03`, `W40` | NUC 1, NUC 2, NUC 7, NUC 12, NUC 13 | partial — units exist; ownership not enforced |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M01` Layer files, imports and fetching by address](#m01-layer-files-imports-and-fetching-by-address) | yes | — |
| [`M02` Records merged by path and partial layers](#m02-records-merged-by-path-and-partial-layers) | yes | — |
| [`M11` Layer header with author, time and version](#m11-layer-header-with-author-time-and-version) | yes | — |

### `C02` On-demand composition

The data of several parties can be combined into one composed model whenever needed, reflecting the current state of each party's data.

| Answers | Used in | In Alpha |
|---|---|---|
| `W04`, `W05`, `W06`, `W40` | NUC 1, NUC 2, NUC 5, NUC 12, NUC 13 | partial — combined when loaded; not kept current |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M01` Layer files, imports and fetching by address](#m01-layer-files-imports-and-fetching-by-address) | yes | — |
| [`M02` Records merged by path and partial layers](#m02-records-merged-by-path-and-partial-layers) | yes | — |
| [`M03` Last layer wins](#m03-last-layer-wins) | yes | — |
| [`M04` Child links build the tree](#m04-child-links-build-the-tree) | yes | — |
| [`M05` Inheritance](#m05-inheritance) | yes | — |

### `C03` Precedence

When several opinions address the same information, it can be determined which one applies and why, distinguishing enrichment, replacement, alternatives and conflict.

| Answers | Used in | In Alpha |
|---|---|---|
| `W07`, `W08`, `W09` | NUC 1, NUC 12 | partial — direct over inherited only; between layers the last wins silently |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M03` Last layer wins](#m03-last-layer-wins) | yes | — |
| [`M05` Inheritance](#m05-inheritance) | yes | — |
| [`M21` Options as separate definitions](#m21-options-as-separate-definitions) | no | — |

### `C04` Provenance

Every piece of information in a model can be traced to the party that stated it and to when it was stated.

| Answers | Used in | In Alpha |
|---|---|---|
| `W10`, `W11`, `W29` | NUC 1, NUC 7, NUC 13 | partial — per layer only; lost when combined |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M11` Layer header with author, time and version](#m11-layer-header-with-author-time-and-version) | yes | — |

### `C05` Building on others' data

A party can add to, annotate, specialise or, where it is responsible, replace another party's objects and definitions without changing the original.

| Answers | Used in | In Alpha |
|---|---|---|
| `W03`, `W16`, `W39` | NUC 1, NUC 2, NUC 10, NUC 11, NUC 12, NUC 13 | yes |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M02` Records merged by path and partial layers](#m02-records-merged-by-path-and-partial-layers) | yes | — |

### `C06` Change-only exchange

Additions, changes and deletions since a previous state can be exchanged on their own, validated on their own, and applied to an existing copy with the same result as a full exchange.

| Answers | Used in | In Alpha |
|---|---|---|
| `W12`, `W13`, `W14`, `W15` | NUC 3, NUC 6, NUC 7, NUC 8 | partial — whole-object deletion missing; diff tool defective |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M02` Records merged by path and partial layers](#m02-records-merged-by-path-and-partial-layers) | yes | — |
| [`M06` Deletion by null](#m06-deletion-by-null) | yes | — |

### `C07` Change history

Exchanged changes form an ordered, attributed history from which any earlier state can be reproduced.

| Answers | Used in | In Alpha |
|---|---|---|
| `W09`, `W11` | NUC 7, NUC 12 | partial — no history concept |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M02` Records merged by path and partial layers](#m02-records-merged-by-path-and-partial-layers) | yes | — |
| [`M03` Last layer wins](#m03-last-layer-wins) | yes | — |
| [`M11` Layer header with author, time and version](#m11-layer-header-with-author-time-and-version) | yes | — |

### `C08` Stable identity

Every object has a globally unique identifier that stays the same across tools, organisations and its whole lifecycle, and conforming tools must preserve it.

| Answers | Used in | In Alpha |
|---|---|---|
| `W03`, `W21`, `W22` | NUC 1, NUC 2, NUC 6, NUC 13 | partial — unique by convention; no conformance rule |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M07` UUID identifiers](#m07-uuid-identifiers) | yes | [`M10` URI identifiers](#m10-uri-identifiers) |
| [`M08` Context paths](#m08-context-paths) | yes | — |
| [`M10` URI identifiers](#m10-uri-identifiers) | no | [`M07` UUID identifiers](#m07-uuid-identifiers) |

### `C09` Reuse by definition

A definition, such as a type, an assembly or a module, is stated once and used in many places; every use reflects changes to it, uses can be counted, and it can be used while still incomplete.

| Answers | Used in | In Alpha |
|---|---|---|
| `W16`, `W17`, `W18` | NUC 2, NUC 9 | yes — counting possible, no query |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M04` Child links build the tree](#m04-child-links-build-the-tree) | yes | — |
| [`M05` Inheritance](#m05-inheritance) | yes | — |
| [`M08` Context paths](#m08-context-paths) | yes | — |

### `C10` References

Data can point to objects in other models and to external resources in a way any tool recognises, and the target of a reference can be reached (see Q49).

| Answers | Used in | In Alpha |
|---|---|---|
| `W06`, `W14`, `W22`, `W23`, `W24`, `W26` | NUC 3, NUC 6, NUC 7, NUC 8, NUC 9, NUC 13 | partial — references stored, not resolved |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M09` References by identifier](#m09-references-by-identifier) | yes | [`M10` URI identifiers](#m10-uri-identifiers) |
| [`M10` URI identifiers](#m10-uri-identifiers) | no | [`M09` References by identifier](#m09-references-by-identifier) |
| [`M12` Namespaced attributes with schemas](#m12-namespaced-attributes-with-schemas) | yes | [`M13` URI-typed attributes](#m13-uri-typed-attributes) |
| [`M13` URI-typed attributes](#m13-uri-typed-attributes) | no | [`M12` Namespaced attributes with schemas](#m12-namespaced-attributes-with-schemas) |

### `C11` Controlled access

The owner of data decides which parts each other party can see and which it can change, and can withdraw that access later; data that is only partly visible remains usable.

| Answers | Used in | In Alpha |
|---|---|---|
| `W19`, `W20` | NUC 2, NUC 13 | no |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M16` Access control and sharing](#m16-access-control-and-sharing) | no | — |

### `C12` Published data

A party can publish data, such as a dataset or a product library, that others use directly at its source instead of copying, following either its current state or a fixed version and, where allowed, writing to it; any local copy can be checked against the source, so it is never silently taken as current.

| Answers | Used in | In Alpha |
|---|---|---|
| `W24`, `W26`, `W27`, `W28`, `W29` | NUC 3, NUC 5, NUC 8, NUC 9, NUC 12, NUC 13 | partial — data can be fetched by address; no following or writing |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M01` Layer files, imports and fetching by address](#m01-layer-files-imports-and-fetching-by-address) | yes | — |
| [`M11` Layer header with author, time and version](#m11-layer-header-with-author-time-and-version) | yes | — |
| [`M14` Writable model](#m14-writable-model) | no | — |
| [`M16` Access control and sharing](#m16-access-control-and-sharing) | no | — |

### `C13` Self-describing data

The meaning of every attribute is defined by a recognisable definition governed by its owner, so independent tools can interpret the data without bespoke mapping.

| Answers | Used in | In Alpha |
|---|---|---|
| `W23`, `W25`, `W30`, `W33` | NUC 4, NUC 8, NUC 13 | partial — every attribute needs a definition; unknown ones make composition fail (Q44) |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M12` Namespaced attributes with schemas](#m12-namespaced-attributes-with-schemas) | yes | — |

### `C14` Selective access

Any part of a model, such as a single object, a subtree or a filtered subset, can be retrieved on its own and on demand, by any client including a web browser, without retrieving or reading the rest of the model.

| Answers | Used in | In Alpha |
|---|---|---|
| `W34`, `W35` | NUC 3, NUC 5 | not checked |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M15` Partial retrieval over HTTP](#m15-partial-retrieval-over-http) | no | — |

### `C15` Open extension

Any party can define its own attributes and their meaning and attach them to any object, without changing the core definitions or needing anyone's approval; definitions from different parties coexist on the same object, and tools that do not know a definition can ignore it without failing.

| Answers | Used in | In Alpha |
|---|---|---|
| `W31`, `W32`, `W33` | NUC 4 | not checked |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M12` Namespaced attributes with schemas](#m12-namespaced-attributes-with-schemas) | yes | — |

### `C16` Render-ready geometry

Geometry can be expressed in forms that common real-time and web rendering pipelines consume directly, without a geometry kernel, and it stays part of the same object as the rest of that object's data.

| Answers | Used in | In Alpha |
|---|---|---|
| `W36`, `W37` | NUC 5 | not checked |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M17` USD and glTF geometry](#m17-usd-and-gltf-geometry) | yes | — |

### `C17` Purpose-specific arrangements

A party can arrange existing data for a particular purpose, such as a navigation hierarchy, a placement scheme or a set of alternatives, without copying or modifying that data; several arrangements can coexist over the same data, and a user or tool selects the one it needs.

| Answers | Used in | In Alpha |
|---|---|---|
| `W06`, `W38`, `W39`, `W40`, `W41` | NUC 10, NUC 11, NUC 12, NUC 13 | not checked |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M19` Separate placement graphs](#m19-separate-placement-graphs) | no | — |
| [`M21` Options as separate definitions](#m21-options-as-separate-definitions) | no | — |

### `C18` Placement intent

A placement can state what it is relative to, by which rule and within what tolerance, and how it was obtained, so that it can be evaluated and re-evaluated from the exchanged data.

| Answers | Used in | In Alpha |
|---|---|---|
| `W42`, `W43` | NUC 11 | not checked |

| Mechanism | In Alpha | Alternative to |
|---|---|---|
| [`M18` Transform relative to parent](#m18-transform-relative-to-parent) | yes | [`M19` Separate placement graphs](#m19-separate-placement-graphs), [`M20` Placement from constraints](#m20-placement-from-constraints) |
| [`M19` Separate placement graphs](#m19-separate-placement-graphs) | no | [`M18` Transform relative to parent](#m18-transform-relative-to-parent) |
| [`M20` Placement from constraints](#m20-placement-from-constraints) | no | [`M18` Transform relative to parent](#m18-transform-relative-to-parent) |

---

## Mechanisms (`M`)

How a capability is realised: one decision an ADR would record. A mechanism is implemented in the IFCX prototype (Alpha), proposed by a NUC's original text, or both. Alpha is evidence, not the standard: an ADR may confirm or replace what it does. Mechanisms live only in the register, not in the NUCs. Which capabilities a mechanism serves, and which mechanisms are alternatives, is recorded only under each capability.

- **A mechanism is separate** only if an ADR could change it without changing the other mechanisms. A rule inside another mechanism, a defect of the reference implementation, or one use of a mechanism is recorded inside that mechanism, not as a mechanism of its own.
- **Families:** the mechanisms are grouped by family to make the list easier to read. A family implies no priority, and the numbers imply no order.
- **Source:** *Alpha* if Alpha implements it, and *proposed in* the NUCs whose original text proposes it. A mechanism can have both. In the capabilities' mechanism tables, *In Alpha* is yes when the source includes Alpha.
- **Gap in Alpha:** where Alpha falls short of the mechanism, or of the capabilities it serves, including defects of the reference implementation.
- **Checked against:** [IFC5-development](https://github.com/buildingSMART/IFC5-development) commit `1a63082` (8 Sep 2026) and [IFCx.dev](https://github.com/buildingSMART/IFCx.dev) commit `36010c0` (19 Nov 2025). Evidence links point to these commits.
- **Level** (Alpha only): *S* schema (`schema/ifcx.tsp` or the published schemas on ifcx.dev), *R* reference implementation (`src/`, including its tests), *E* examples only.
- **Probes:** behaviour checked by running the reference implementation is in [alpha-probes.md](alpha-probes.md).
- **ADR:** to be filled in when the ADR exists (Q45).
- **Question:** links to the question in [open-questions.md](open-questions.md). The link uses the question's heading, so when a question is renamed or resolved, update its links here.

### Family: composition engine

#### `M01` Layer files, imports and fetching by address

A layer is an IFCX file identified by the `id` in its header. A file lists other layers in `imports` by URI, and the set of layers is assembled by resolving imports recursively from one root layer. Layers are fetched by URI over HTTP, or from the file system or memory, through interchangeable providers, so a dataset published at an address is used there by other parties instead of being copied.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 9, NUC 13 | S, R, E | — |

**Gap in Alpha:** A fetched layer is cached for the session and not refreshed, so it does not follow the live source. The `integrity` field of an import is defined but not checked.

**Evidence:** [ifcx.tsp L79–90](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/schema/ifcx.tsp#L79-L90) · [layer-stack.ts L88–137](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/layers/layer-stack.ts#L88-L137) · [layer-stack tests](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/layer-stack-test.ts#L22-L63) · [fetch-layer-provider.ts](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/layers/fetch-layer-provider.ts#L30-L45) · [layer-providers.ts](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/layers/layer-providers.ts) · [imports in hello-wall](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Hello%20Wall/hello-wall.ifcx)

#### `M02` Records merged by path and partial layers

Every opinion is part of a node record with a `path` and optional `children`, `inherits` and `attributes`. Any number of records, in the same layer or in different layers, can address the same path; composition merges them per path. A layer can contain records for any subset of nodes, including records that refer to nodes defined only in other layers, and composes and validates on its own, provided the schemas of its attributes are available. Changes are therefore exchanged as ordinary layers containing only the opinions added, changed or deleted, with no special format or protocol. An append-only sequence of such layers is a change history, closer to an event log than to source-control diffing.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 7 | S, R, E | — |

**Gap in Alpha:** The reference implementation's tool that computes a layer containing only changes from two files (CLI `diff`) omits added nodes, children and attributes at this commit, and turns changed values `0`, `false` and empty text into deletions, so applying its output does not reproduce the newer file. There is no concept of a change history: nothing names or orders a sequence of change layers beyond layer order.

**Evidence:** [ifcx.tsp L14–19](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/schema/ifcx.tsp#L14-L19) · [compose.ts L26–70](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L26-L70) · [fire-rating example](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Hello%20Wall/hello-wall-add-fire-rating-30.ifcx) · [federating diffs test](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/workflows-test.ts#L36-L46) · [P8](alpha-probes.md#p8) · [workflows.ts L66–152](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/workflows.ts#L66-L152) · [ifcx-cli.ts L34–56](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-cli/ifcx-cli.ts#L34-L56) · [diff tests](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/workflows-test.ts#L24-L46) · [P6](alpha-probes.md#p6), [P7](alpha-probes.md#p7)

#### `M03` Last layer wins

Precedence between layers is by position: layers are ordered (the root layer first, then its imports, depth-first), and for each child, inherit and attribute entry the value in the last record wins. As a result, an imported layer takes precedence over the layer that imports it.

| Source | Level | ADR |
|---|---|---|
| Alpha | R | — |

**Gap in Alpha:** Differing values are not reported, so conflicts are not detected and alternatives cannot be told from replacements.

**Question:** [Q19](open-questions.md#q19--how-ifcx-decides-precedence)

**Evidence:** [compose.ts L8–25](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L8-L25) · [compose.ts L26–57](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L26-L57) · [layer-stack.ts L9](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/layers/layer-stack.ts#L9) · [federation test](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/workflows-test.ts#L8-L22) · [P1](alpha-probes.md#p1)

#### `M04` Child links build the tree

The composed tree is built from `children` entries, each mapping a local name to a node path, starting from root nodes. A node that is the child of several parents has its whole subtree instantiated under each, so a type's parts appear under every occurrence. Children are resolved each time the layers are composed, from the definitions present at that moment; nothing is copied into the referring node, so a changed definition reaches every node that refers to it at the next composition. Composition rejects `children` and `inherits` entries that form a cycle.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 1, NUC 2, NUC 9, NUC 10 | S, R | — |

**Gap in Alpha:** This tree is the only hierarchy, so several arrangements of the same data cannot coexist (`C17`).

**Evidence:** [compose.ts L160–175](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L160-L175) · [compose.ts L117–137](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L117-L137) · [layer-stack.ts L26–38](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/layers/layer-stack.ts#L26-L38) · [cycles.ts](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/cycles.ts) · [cycles.ts L46–62](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/cycles.ts#L46-L62) · [children tests](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/compose-test.ts#L55-L93) · [cycle test](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/compose-test.ts#L66-L73) · [P3](alpha-probes.md#p3) · [P9](alpha-probes.md#p9) · [P10](alpha-probes.md#p10)

#### `M05` Inheritance

An `inherits` entry makes a node receive the composed attributes and children of another node, or of a part of it, by reference and not by copy. The node's own attributes are applied afterwards, so an attribute stated directly on the node wins over an inherited one. Inherits entries are resolved each time the layers are composed, so a changed definition reaches every node that inherits from it at the next composition. The cycle rule of [`M04`](#m04-child-links-build-the-tree) applies to `inherits` entries too.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 1, NUC 2, NUC 9, NUC 10 | S, R | — |

**Evidence:** [compose.ts L141–159](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L141-L159) · [compose.ts L177–180](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L177-L180) · [inherit tests](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/compose-test.ts#L95-L193) · [P3](alpha-probes.md#p3)

#### `M06` Deletion by null

A deletion is an opinion (a tombstone): a record deletes a child, inherit or attribute entry by setting it to `null`, and the deletion applies if it comes after the value in layer order.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 7 | S, R | — |

**Gap in Alpha:** No record deletes a node as such: a node leaves the tree only when it is removed from its parent's children. Deleting an attribute fails schema validation in the reference implementation.

**Question:** [Q43](open-questions.md#q43--deleting-an-object)

**Evidence:** [ifcx.tsp L16–17](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/schema/ifcx.tsp#L16-L17) · [compose.ts L41–45](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L41-L45) · [compose.ts L170–174](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L170-L174) · [deletion tests](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/test/compose-test.ts#L195-L236) · [schema-validation.ts L11](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/schema/schema-validation.ts#L11) · [P2](alpha-probes.md#p2)

### Family: identity and references

#### `M07` UUID identifiers

A node's own path is a UUID.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 3, NUC 6, NUC 7 | S, E | — |

**Gap in Alpha:** The UUID is a convention only: the schema constrains the path to a text pattern, and nothing checks that it is a UUID or unique. The pattern does not match the examples' paths and is not checked by the reference implementation.

**Question:** [Q33](open-questions.md#q33--identifier-uuid-path-or-uri)

**Evidence:** [ifcx.tsp L8–9](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/schema/ifcx.tsp#L8-L9) · [hello-wall example](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Hello%20Wall/hello-wall.ifcx) · [non-UUID path in 3rd-window example](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Hello%20Wall/advanced/3rd-window.ifcx)

#### `M08` Context paths

A node inside the composed tree can also be addressed by a context path: the identifier of a node followed by child names, for example `<uuid>/My_Project/My_Site/My_Building/My_Storey/Wall/Window_001`. An opinion on a context path applies only to the node in that position.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 6 | R, E | — |

**Question:** [Q35](open-questions.md#q35--hierarchically-composable-identifiers)

**Evidence:** [path.ts](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/path.ts) · [compose.ts L131–137](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/composition/compose.ts#L131-L137) · [specific-fire-rating example](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Hello%20Wall/hello-wall-add-specific-fire-rating.ifcx) · [P3](alpha-probes.md#p3), [P5](alpha-probes.md#p5)

#### `M09` References by identifier

A relationship to another node is an attribute value holding that node's identifier, `{"ref": "<uuid>"}`, for example in `bsi::ifc::system::connectsto` or `bsi::ifc::spaceBoundary`.

| Source | Level | ADR |
|---|---|---|
| Alpha | S, R, E | — |

**Gap in Alpha:** Published schemas type the value as text; the schema language's `Reference` data type is unused and only checked as text; composition does not resolve references.

**Question:** [Q49](open-questions.md#q49--resolving-references-wanted-but-not-claimed)

**Evidence:** [ifcx.tsp L39](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/schema/ifcx.tsp#L39) · [schema-validation.ts L76–82](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/schema/schema-validation.ts#L76-L82) · [ifc@v5a schema](https://github.com/buildingSMART/IFCx.dev/blob/36010c0e1069043f964a7dff8367e3e910255ebb/%40standards.buildingsmart.org/ifc/core/ifc%40v5a.ifcx) · [P11](alpha-probes.md#p11)

#### `M10` URI identifiers

Every object has a stable URI, and a reference identifies its target by that URI.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 1, NUC 6, NUC 8, NUC 13 | — | — |

**Question:** [Q33](open-questions.md#q33--identifier-uuid-path-or-uri)

### Family: provenance and versions

#### `M11` Layer header with author, time and version

Every layer has a required header with `id`, `ifcxVersion`, `dataVersion`, `author` and `timestamp`, which records who stated the layer's opinions and when. Versions are also written into layer identifiers and import URIs by convention, for example `ifc@v5a.ifcx` or `3rd-window@v1.ifcx`, so a reference can name a specific version of a dataset or library.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 7, NUC 9, NUC 13 | S, R, E | — |

**Gap in Alpha:** When layers are composed, only the first layer's header is kept, and the composed nodes carry no record of which layer or author supplied each value. Composition attaches no meaning to versions, so a reference cannot choose between following the current state and staying on a fixed version.

**Question:** [Q27](open-questions.md#q27--provenance-per-layer-or-per-opinion)

**Evidence:** [ifcx.tsp L21–27](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/schema/ifcx.tsp#L21-L27) · [workflows.ts L154–177](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/workflows.ts#L154-L177) · [imports in hello-wall](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Hello%20Wall/hello-wall.ifcx) · [P1](alpha-probes.md#p1)

### Family: attributes and schemas

#### `M12` Namespaced attributes with schemas

Attribute keys are namespaced identifiers, for example `bsi::ifc::prop::FireRating`, or `nlsfb::class` and `CCIConstruction::class`, which classify an object by a code and a URI pointing to bSDD, one attribute per classification system. Each key needs a schema, supplied by the layer or an imported layer, stating its data type, restrictions, quantity kind and schema inheritance, and values are checked against it. Each namespace is owned and governed by its publisher, who maintains its schema.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 4, NUC 8 | S, R, E | — |

**Gap in Alpha:** Composition fails when an attribute has no schema or its value does not match it, so a tool cannot ignore attributes it does not know. URIs in attribute values, such as bSDD links in classifications, are typed as text and nothing resolves them. Not yet checked: whether each namespace is identified by a URI owned by its publisher, with a versioned, machine-readable schema, as NUC 4 proposes.

**Question:** [Q44](open-questions.md#q44--attributes-without-a-known-definition), [Q49](open-questions.md#q49--resolving-references-wanted-but-not-claimed)

**Evidence:** [ifcx.tsp L29–77](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/schema/ifcx.tsp#L29-L77) · [schema-validation.ts L124–152](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/ifcx-core/schema/schema-validation.ts#L124-L152) · [published schemas](https://github.com/buildingSMART/IFCx.dev/blob/36010c0e1069043f964a7dff8367e3e910255ebb/%40standards.buildingsmart.org/ifc/core/prop%40v5a.ifcx) · [nlsfb schema](https://github.com/buildingSMART/IFCx.dev/blob/36010c0e1069043f964a7dff8367e3e910255ebb/%40nlsfb/nlsfb%40v1.ifcx) · [hello-wall example](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Hello%20Wall/hello-wall.ifcx)

#### `M13` URI-typed attributes

A reference to an external resource is an attribute whose schema types it as a URI, so any tool can tell it from ordinary text.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 8 | — | — |

**Question:** [Q49](open-questions.md#q49--resolving-references-wanted-but-not-claimed)

### Family: publishing and access

#### `M14` Writable model

A model is a writable data endpoint: authorised external systems write data directly to its objects.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 13 (from NUC 8) | — | — |

**Question:** [Q51](open-questions.md#q51--writable-model-endpoint)

#### `M15` Partial retrieval over HTTP

Parts of a model are requested over standard HTTP by node identifier, subtree or filter, and the data is JSON, so any HTTP client can read it incrementally.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 3 | — | — |

#### `M16` Access control and sharing

Visibility is defined per layer, as explicit boundaries stating which opinions each party can see; a party with partial access sees a partially resolved node. Access follows an open sharing protocol, analogous to Delta Sharing, through which providers keep governing the shared source. Whether these are one design or two alternatives is for an ADR.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 2, NUC 13 | — | — |

**Question:** [Q18](open-questions.md#q18--trust)

### Family: geometry and placement

#### `M17` USD and glTF geometry

Geometry and appearance are node attributes following USD and glTF definitions (`usd::usdgeom::mesh`, `usd::usdgeom::basiscurves`, `gltf::material`, `bsi::ifc::presentation::*`), plus point-cloud attributes, which a renderer displays directly, as the reference viewer does.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 5 | S, R, E | — |

*Also relevant to the IFC 4.3 and IFCX concepts comparison ([IFC4x-IFC5-constructs.md](IFC4x-IFC5-constructs.md)).*

**Question:** [Q57](open-questions.md#q57--new-capability-render-ready-geometry)

**Evidence:** [render.ts L176–370](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/viewer/render.ts#L176-L370) · [usd schema](https://github.com/buildingSMART/IFCx.dev/blob/36010c0e1069043f964a7dff8367e3e910255ebb/%40openusd.org/usd%40v1.ifcx)

#### `M18` Transform relative to parent

A node is placed by a `usd::xformop` transform matrix relative to its parent in the composed tree. Linear placement uses `bsi::ifc::linearreference` attributes.

| Source | Level | ADR |
|---|---|---|
| Alpha; proposed in NUC 11 | R, E | — |

*Also relevant to the IFC 4.3 and IFCX concepts comparison ([IFC4x-IFC5-constructs.md](IFC4x-IFC5-constructs.md)).*

**Gap in Alpha:** The basis is always the parent in the single tree, so no other reference basis can be chosen, and no rule, tolerance or origin of the placement is recorded.

**Question:** [Q60](open-questions.md#q60--how-a-placement-is-represented)

**Evidence:** [render.ts L412–422](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/src/viewer/render.ts#L412-L422) · [linear placement example](https://github.com/buildingSMART/IFC5-development/blob/1a63082ada967c683cfacee2005f8f749c8e1b79/examples/Linear%20placement%20of%20signals)

#### `M19` Separate placement graphs

Placement definitions are kept separate from any spatial structure and authored over the same data as placement graphs, from which a user or tool selects one.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 11 | — | — |

**Question:** [Q60](open-questions.md#q60--how-a-placement-is-represented)

#### `M20` Placement from constraints

A placement is derived from relationships and constraints instead of being stated as a transform.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 11 (left open: authored, derived or both) | — | — |

**Question:** [Q60](open-questions.md#q60--how-a-placement-is-represented)

### Family: options

#### `M21` Options as separate definitions

An option is a separately authored definition that collects references to existing objects, layers or datasets, marks what is shared, and adds or replaces data for one alternative; option identity is kept distinct from dataset version, layer order and repeated identifiers.

| Source | Level | ADR |
|---|---|---|
| Proposed in NUC 12 | — | — |

---

## Limitations — STEP language (`SL`)

Maintained separately and already reviewed. Only glossary alignment is allowed when writing a NUC.

| ID | Statement | Used in |
|---|---|---|
| `SL01` | STEP has no language-level mechanism to adjust, replace, or remove content in a referenced entity; any such capability would have to be defined as a schema-level interpretation rather than provided as a basic language feature. | NUC 1 |
| `SL02` | STEP's "4;2" conformance level (not available to IFC, which uses an older SPF version) lets entities nominated as ANCHORS be REFERENCED from other models, but only at whole-entity granularity - it provides no single-attribute replacement and no deletion mechanism. | NUC 1, NUC 7 (ref.) |
| `SL03` | STEP's "4;2" anchor mechanism requires the referenced entities to be named and nominated as anchors in advance; since in practice any component could become a reference target, this requires extensive up-front coordination between parties to establish links. | NUC 1, NUC 6, NUC 7 (ref.) |
| `SL04` | EXPRESS supports optional, unset attribute values (the `$` placeholder in Part 21, `OPTIONAL` in the schema), so individual attributes can be left unspecified. What it has no concept of is an entity or type definition that is provisionally incomplete and expected to be extended by a different party later - every instantiated entity must still conform to a fully declared type known to the schema. | NUC 2 |
| `SL05` | STEP's classic Part 21 Clear Text Encoding file is a sequential text stream in which every entity is addressed by a local integer (#N), meaningful only within that file. | NUC 3 |
| `SL06` | STEP's Part 21 Clear Text Encoding has no index of instance locations, so a reader must scan the file to locate the byte position of a given `#N` reference; there is no way to jump directly to an arbitrary instance without such a scan or a separately built index. | NUC 3 |
| `SL07` | STEP's Part 21 Clear Text Encoding has no random-access index or pagination primitive native to it; splitting a model across multiple "4;2" files reduces size per unit but doesn't remove the per-file full reference-resolution pass. | NUC 3 |
| `SL08` | EXPRESS is a closed-world schema language: every entity type and attribute must be declared in the schema before it can appear in a valid file. This is inherent to EXPRESS - and by extension STEP - not an IFC-specific choice. An open-world-assumption language would allow more flexibility, but that is a different language. | NUC 4 |
| `SL09` | Because EXPRESS's closed-world declaration requirement is a language-level constraint, an independently governed, typed extension mechanism cannot be achieved within an EXPRESS-based schema without changing the underlying schema language. | NUC 4 |
| `SL10` | STEP defines no language-level semantics for an identifier that automatically persists across independently produced files, applications, or transformations; any persistence guarantee must come from schema definition and consistent implementation. | NUC 6 |
| `SL11` | STEP's "4;2" anchors give no stability guarantee across model transformations and are not externally resolvable URIs. | NUC 6, NUC 7 (ref.) |
| `SL12` | No standardised delta format exists in the STEP/IFC ecosystem. STEP Part 21's #N instance numbering is local and ephemeral by design - tools routinely regenerate it on export - making file-to-file diffing unreliable as a basis for change detection regardless of schema. | NUC 7 |
| `SL13` | In the classic Part 21 Edition 1/2 exchange structure, which must be self-contained, a file containing only changed entities is not structurally valid unless it also includes every entity those changed ones reference, in practice requiring most of the model. Edition 3's ANCHOR/REFERENCE mechanism (`SL02`, `SL03`, `SL11`) relaxes the self-containment requirement, but only at whole-entity granularity and with anchors nominated in advance, so it does not by itself provide a workable delta mechanism. | NUC 7 |
| `SL14` | Standardised delta exchange is expected to stay difficult within STEP even with more recent STEP capabilities. | NUC 7 |
| `SL15` | STEP Part 21 and conventional IFC exchange serialise a model snapshot for transfer and import: most instance references are only meaningful within that exchange graph, so a recipient normally needs a local resolved copy of the data before using it. This copy-first model is a characteristic of the classic exchange format, not of any one schema built on it. | NUC 13 |
| `SL16` | Existing STEP/IFC-related API work provides programmatic access to models, but an API alone doesn't establish independently governed live datasets, permissioned cross-owner references, source-authoritative freshness, arbitrary third-party composition, or implementation-independent caching; these require additional standardised protocol and reference semantics, not just schema changes. | NUC 13 |

## Limitations — IFC schema (`IL`)

| ID | Statement | Used in |
|---|---|---|
| `IL01` | IFC has no concept of persistent, independently owned layers that stay separately editable and are composed on demand. | NUC 1 |
| `IL02` | IFC has no concept of composing layers, so coordination requires full-model exports and manual federation. IFC's `IfcOwnerHistory` records a single, overwritable last-touch `OwningUser`/`OwningApplication`, not a per-discipline history, so the merged snapshot still lacks reliable attribution. | NUC 1 |
| `IL03` | Delta files and partial model server exports exist in IFC as workarounds for the lack of layers and composition, but are non-standardised, non-portable between platforms, and don't preserve authorship provenance. | NUC 1 |
| `IL04` | IFC's schema defines a Type/Occurrence pattern (e.g. `IfcTypeObject` and its occurrences), but has no mechanism for instantiating a type's child parts under the corresponding occurrences. | NUC 2 |
| `IL05` | IFC's specification describes property inheritance and override between a type and its occurrences only in prose, not as a formal schema rule, leading to inconsistent implementation across tools. | NUC 2 |
| `IL06` | The IFC schema has no concept of higher-order typical objects (types of types). | NUC 2 |
| `IL07` | IFC has not adopted alternative STEP encodings, so current IFC tooling needs either a full file download/parse or purpose-built middleware with its own index - non-standardised, costly infrastructure. | NUC 3 |
| `IL08` | IFC's workaround for EXPRESS's closed-world constraint is `IfcPropertySet`. Property values are typed via `IfcValue`, but the property `Name` is an unconstrained string with no namespace, so nothing prevents name collisions across organisations. | NUC 4 |
| `IL09` | IFC has a documented convention that lets a property carry a bSDD reference as a plain string, but it's unenforced by the schema and inconsistently adopted, so most property sets stay opaque to tools unaware of the specific naming convention. | NUC 4 |
| `IL10` | IFC's `GlobalId` is a 22-character compressed 128-bit GUID, generated to be globally unique, with no hierarchical structure or namespace. The schema imposes no requirement that it stay unchanged across model server operations. | NUC 6 |
| `IL11` | `GlobalId` alone carries no information about what changed. `IfcOwnerHistory.ChangeAction` exists for this purpose, but it's optional, whole-object-level, and inconsistently populated in practice. | NUC 7 |
| `IL12` | In the absence of a standardised IFC delta mechanism, practical approaches (BIMserver change detection, proprietary model-server delta APIs, external diffing of two full files) exist only as application-level workarounds, not standardised schema mechanisms. | NUC 7 |
| `IL13` | IFC provides `IfcPropertyAbstraction.HasExternalReferences`, a relationship linking an individual property to an external reference; IFC2x3 has no equivalent. The documented plain-text convention (`IfcPropertySingleValue.Specification`/`.Description`) still isn't schema-typed as a URI, and both mechanisms are inconsistently used in practice. | NUC 8 |
| `IL14` | IFC's `IfcTypeObject` gives limited type-occurrence separation for single objects only, not for assemblies (typed groups of sub-components with their own structure/relationships). | NUC 9 |
| `IL15` | IFC has no schema mechanism to define a reusable typed assembly (e.g. beam-with-connections-and-reinforcement) and instantiate it by reference rather than copying every sub-component into every occurrence. | NUC 9 |
| `IL16` | `IfcMappedItem`/`IfcRepresentationMap` let geometry be defined once and reused across occurrences via a shared representation and per-occurrence transform, so geometry need not be literally duplicated - the redundancy problem is narrower than full geometry copies. | NUC 9 |
| `IL17` | `IfcLibraryReference` (via `IfcRelAssociatesLibrary`) is a real, URI-typed schema mechanism for linking an object to an external library entry, not just static file exports. What's missing is live resolution: an update at the source doesn't automatically propagate to the referencing object. | NUC 9 |
| `IL18` | In IFC, object data, decomposition/containment relationships, and placement chains are embedded in the same instance graph; groups and systems add further associations, but the common project-site-facility-storey decomposition stays closely coupled to navigation, containment, and geometry resolution. | NUC 10 |
| `IL19` | In IFC, alternative discipline- or task-specific hierarchies must be added as more relationships within the single instance graph that also holds decomposition, containment, and placement data, via external conventions, or as separately restructured models. | NUC 10 |
| `IL20` | IFC has no mechanism to publish object data independently and apply interchangeable, separately authored structures over it without duplication; a schema revision could add one. | NUC 10 |
| `IL21` | IFC supports local, grid, and infrastructure-oriented linear placement, with local placements forming relative chains - but an occurrence exposes one placement per model state, commonly resolved to a single world-space result tied to containment/decomposition structure. | NUC 11 |
| `IL22` | IFC provides no first-class, interchangeable placement graphs that different users or phases can author over the same occurrence data and select for a given evaluation. | NUC 11 |
| `IL23` | In IFC, a relative placement transform doesn't itself communicate the dimensioning rule, tolerance, or constraint that motivated it - that intent stays in drawings or application-specific data, and alternative placement schemes require duplicated occurrences or separately maintained models. | NUC 11 |
| `IL24` | IFC has no dedicated schema entities for simultaneous design options, shared membership across options, or external option sets. | NUC 12 |
| `IL25` | In IFC, alternatives can be approximated with groups, classification conventions, property values, or separate files, but a general IFC consumer can't tell from those mechanisms which elements are common, mutually exclusive, or option-specific without prior agreement. | NUC 12 |
| `IL26` | In IFC, when alternatives are exchanged as separate files, common objects are duplicated even if their GlobalIds are preserved, and changes must be coordinated across the copies. | NUC 12 |

---

## Open issues

Questions and pending decisions are kept in [open-questions.md](open-questions.md), not here. This section only tracks housekeeping.

- **Alpha encodings of IFC concepts:** how Alpha encodes materials, the IFC class, georeferencing, alignments and units serves no NUC capability. It is described at the end of the IFC 4.3 and IFCX concepts comparison ([IFC4x-IFC5-constructs.md](IFC4x-IFC5-constructs.md)), not here. `M17` and `M18` are also used by that comparison, besides `C16` and `C18`.
- **Re-checking Alpha:** when the prototype moves on, re-check the mechanisms against a new commit and update the commit named in the Mechanisms section.
- **Unnumbered notes** in the IFC/STEP sections of the NUCs (for example "These are schema-formalisation gaps…", implementation notes, and notes on IFCX's current state in NUC 12 and NUC 13) are not registered. They stay in their NUC as written.
