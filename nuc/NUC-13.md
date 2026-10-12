# NUC 13: Using other parties' data at its source, live or at a fixed version, without copies

**Original title:** Reference-first distributed access

**Related NUCs:** NUC 2 addresses decentralised collaboration, NUC 3 addresses selective loading, NUC 7 addresses incremental updates, and NUC 8 addresses external references. This NUC also provides the distributed access model needed for the external structures, placements, and options described by NUC 10, NUC 11, and NUC 12.

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

With IFC, data has to be sent somewhere else before it can be used: the recipient downloads a file, imports it and works on a new copy. For large programmes where each organisation owns and governs its own data, those copies raise questions of ownership, currency, synchronisation and redistribution. Building owners also run HVAC, fire safety and access control systems from different vendors, each needing its own integration and mapping to exchange data with the model. Today's IFCX prototype still works inside the file boundary, so it does not yet support using data live at its source.

## 2. What we want to achieve

**Using data at its source**
- `W26` An organisation can publish its data, such as a dataset or a manufacturer's product types, so that other parties and their tools use it directly at its source instead of holding copies, and see its current state, for example new or updated products when they are released, without static exports, imports or separate data transfers. A manufacturer can also learn which of its types a design uses, without a separate data transfer.
- `W28` A reference to a source dataset can follow the source's current state or stay on a fixed version of it, as chosen by the party making the reference.
- `W05` When a party changes its data, the change appears in the composed models and displays that use it, without a new file being sent, without manual re-assembly and without regenerating a separate visualisation file. *(see also NUC 1)*
- `W29` A local copy of another party's data is never silently treated as current: a consumer keeps track of where each piece of data came from and can check its copy against the source.
- `W24` A user or tool holding a reference to an object in another model, or to an external resource, can follow it and read the target's current content from its source at any time, without the model being updated when the target changes, for example a work task reading the areas and colour of the walls it concerns, or a third-party platform following references to compile a material passport that stays traceable to its sources. *(see also NUC 8)*

**Composing independent sources**
- `W06` A third party can compose data from several independent sources, together with its own additions, which can stay private, without copying the sources and without the sources knowing about each other or about the composition.
- `W03` A party can add opinions to another party's objects, for example enrichments, status flags or approval notes, without modifying that party's layer, even when it has only read access or no authoring rights, such as a client. What it adds stays linked to those objects when they change, with no separate copy to keep in sync. *(see also NUC 1)*

**Permissions**
- `W19` A party can decide which parts of its data each other party can see, and other parties can still use the objects and definitions that they see only in part. *(see also NUC 2)*
- `W20` A data owner can give another party read access without write access or ownership, and can later withdraw that access.

**Different platforms and live systems**
- `W30` Systems from different vendors can exchange data with a model without bespoke integration or vendor-specific mapping.
- `W27` External systems, such as building management systems or IoT controllers, can write data, such as readings and fault statuses, directly to specific objects in a model, and several authorised platforms can read that same current data.

## 3. IFCX capabilities

- `C10` **References.** Data can point to objects in other models and to external resources in a way any tool recognises, and the target of a reference can be reached (see Q49).
  *In this NUC: `W26`, `W24`, `W06`*
- `C12` **Published data.** A party can publish data, such as a dataset or a product library, that others use directly at its source instead of copying, following either its current state or a fixed version and, where allowed, writing to it; any local copy can be checked against the source, so it is never silently taken as current.
  *In this NUC: `W26`, `W28`, `W29`, `W24`, `W27`*
- `C02` **On-demand composition.** The data of several parties can be combined into one composed model whenever needed, reflecting the current state of each party's data.
  *In this NUC: `W05`, `W06`*
- `C04` **Provenance.** Every piece of information in a model can be traced to the party that stated it and to when it was stated.
  *In this NUC: `W29`*
- `C17` **Purpose-specific arrangements.** A party can arrange existing data for a particular purpose, such as a navigation hierarchy, a placement scheme or a set of alternatives, without copying or modifying that data; several arrangements can coexist over the same data, and a user or tool selects the one it needs.
  *In this NUC: `W06`*
- `C01` **Separate contributions.** Each party's data is kept as a distinct unit that the party owns and can add to, change or withdraw without affecting any other party's data.
  *In this NUC: `W03`*
- `C05` **Building on others' data.** A party can add to, annotate, specialise or, where it is responsible, replace another party's objects and definitions without changing the original.
  *In this NUC: `W03`*
- `C08` **Stable identity.** Every object has a globally unique identifier that stays the same across tools, organisations and its whole lifecycle, and conforming tools must preserve it.
  *In this NUC: `W03`*
- `C11` **Controlled access.** The owner of data decides which parts each other party can see and which it can change, and can withdraw that access later; data that is only partly visible remains usable.
  *In this NUC: `W19`, `W20`*
- `C13` **Self-describing data.** The meaning of every attribute is defined by a recognisable definition governed by its owner, so independent tools can interpret the data without bespoke mapping.
  *In this NUC: `W30`*

**Not claimed**
- IFCX does not prescribe how data is cached, where or for how long, or how distributed infrastructure refreshes it; the claim is limited to identifying, authorising, resolving, versioning and checking data against its source (`C12`).
- IFCX does not claim, in this NUC, to address offline exchange or long-term archival formats; the claim is limited to access to data at its source (`C12`).
- IFCX does not claim that data already delivered to an authorised party can be prevented from being copied; the claim is limited to granting and withdrawing future access (`C11`).

## 4. What happens in IFC-STEP today

**Note on terminology:** reviewer feedback flagged that "reference-first distributed access" needs clearer definition. The bullets below reflect the existing technical claims about the STEP/IFC exchange model.

**STEP (language):**
- `SL15` STEP Part 21 and conventional IFC exchange serialise a model snapshot for transfer and import: most instance references are only meaningful within that exchange graph, so a recipient normally needs a local resolved copy of the data before using it. This copy-first model is a characteristic of the classic exchange format, not of any one schema built on it.
- `SL16` Existing STEP/IFC-related API work provides programmatic access to models, but an API alone doesn't establish independently governed live datasets, permissioned cross-owner references, source-authoritative freshness, arbitrary third-party composition, or implementation-independent caching; these require additional standardised protocol and reference semantics, not just schema changes.

**IFC schema:** No distinct schema-level gap beyond the above.

Current file-based IFCX prototypes inherit the same copy-first boundary described above, even though their JSON representation may be easier to serve over HTTP. (This is a note on IFCX's current state, not an IFC/STEP limitation.)

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Live composition across three CDEs

One project CDE holds geometric data and a second holds metadata under a different organisation's control. A third CDE creates a private set of arrangements containing the spatial structures, placement logic, and options described by NUCs 10, 11, and 12. It composes both source datasets by reference; the first two CDEs do not need to know about one another or store those arrangements. No additional IFCX container holding copies of all three datasets is required, although any participant may use an implementation-specific cache.

### 2. Permissioned read-only project data

An owner gives a consultant read-only access to a live dataset in the way an online document can be shared without granting edit rights or transferring ownership. The consultant's application consumes the authorised data directly and cannot write back to the source. Contractual and technical controls may restrict retention or caching, but the exchange format does not make the impossible promise that bytes already delivered to an authorised client cannot be copied.

### 3. Frequently changing authoritative information

An author updates project data throughout the day. Consumers follow the live reference rather than treating yesterday's downloaded file or an unchecked cache as authoritative. A consuming system may retain data locally for performance, but it validates the cached state against the source and refreshes it when required. The author publishes once at the source instead of redistributing a new container after every change.

### 4. Share once across heterogeneous platforms

Following the business pattern demonstrated by Delta Sharing, a provider exposes one governed dataset through an open access protocol. Design, construction, analysis, and operational platforms connect to that shared source using their own technology stacks. Each consumer decides how to process and cache the data, while the provider manages permissions and the authoritative live or versioned states once rather than shipping platform-specific copies.

### 5. Cross-organisational infrastructure federation by reference *(moved from NUC 8)*

A rail electrification programme spans assets owned by seven organisations. Under IFCX, each organisation's dataset is a live, addressable endpoint. When the utility company updates a diversion route, highway designers hold a live URI reference to that object - the update is visible immediately by reference resolution, not by file redistribution. No organisation holds a copy of another's data; all hold pointers. The semantic content at each pointer is governed by the owning organisation's namespace schema, machine-readable to any party that dereferences it.

### 6. Live IoT and BMS writes against model objects *(moved from NUC 8)*

A district council operates 34 municipal buildings. Each has HVAC, fire safety, and access control systems from different vendors. Under IFCX, the model is not a read-only handover artifact - it is a writable data endpoint. The HVAC controller pushes energy readings against each AHU's URI every 15 minutes. When a fire damper fails its weekly test, the BMS writes a fault status directly to the corresponding IFCX object. Any authorised platform - the council's FM dashboard, a compliance auditor's tool, a maintenance contractor's app - reads the same live data from the same URIs. No bespoke integration, no vendor-specific API mapping.
