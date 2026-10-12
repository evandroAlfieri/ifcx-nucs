# IFCX NUC Glossary

Shared terms for writing and reviewing all NUCs. Use these terms consistently; if a NUC needs a term that is not here, add it here first.

---

## Tags

| Tag | Meaning | Rule |
|---|---|---|
| `W` | **Want** — a need or requirement. | Must be testable (IFCX either does it or not) and solution-neutral (two different technical designs could both deliver it). If it cannot be made testable, it becomes part of the problem paragraph in section 1 of the NUC. |
| `C` | **Capability** — an ability IFCX provides, stated without saying how, whether or not the current prototype supports it yet. | Must pass four checks: (1) it states an ability, not a method, so no mechanism terms (URI, UUID, file, record, import, tombstone…), though glossary concepts such as layer, opinion and precedence are allowed; (2) it answers several wants, or one only if no more general capability fits; (3) it is more general than any want it answers, so if it reads like one of its wants, it is that want; (4) how IFCX delivers it lives in mechanisms and ADRs. Capabilities are few and shared: a NUC maps its wants to existing capabilities and proposes a new one only when none fits. |
| `M` | **Mechanism** — how a capability is realised: a concrete rule or structure, implemented in the IFCX prototype (Alpha), proposed by a NUC's original text, or both. | One mechanism is one decision an ADR would record, and links its ADR once one exists. May use mechanism terms (file, import, record, path, URI). Its *Source* says whether Alpha implements it, which NUCs propose it, or both; an Alpha mechanism cites evidence pinned to a commit, and its defects go in *Gap in Alpha*. Several mechanisms may realise the same capability: they are alternatives until an ADR chooses. |
| `SL` / `IL` | **STEP language / IFC schema limitation.** | Maintained separately; reviewed. |

Tags are shared across all NUCs: a want or capability that appears in several NUCs keeps the same ID. Mechanisms live only in the register, not in the NUCs.

**Not claimed.** What IFCX does not promise in one NUC is written as a plain bullet under **Not claimed** in section 3 of that NUC. It has no tag and no ID and is not in the register. It names the capability whose claim it limits, for example "…the claim is limited to `C07`".

**Section 1 of a NUC has no tags.** The statements about how work is done today, and about the context of a problem, are plain prose: one short paragraph with no IDs. In that paragraph, avoid absolutes about practice (always, never, every, cannot) unless the statement is literally true, for example a fact about the IFC schema; no source is required.

Every tagged item must be **self-contained**: understandable when read alone in the register, without the items around it. Avoid references that depend on neighbouring text, such as "the merge", "such", "do so", "where entitled", or "other parties" with no stated situation.

---

## Terms

| Term | Definition |
|---|---|
| **Party** | An organisation or role that authors information (for example structural engineer, fire engineer, client). |
| **Node** | What opinions are about, identified by a stable path. A node has no content of its own: its content is the composition of all opinions about it. Objects are nodes, but not all nodes are objects (types, geometry and property holders are nodes too). Wants say *object*; capabilities may say *node*. |
| **Opinion** *(provisional — to be renamed **statement**)* | One piece of information about a node — an attribute value, a relationship, a classification — authored by one party. |
| **Layer** *(provisional — to be renamed **contribution**)* | A set of opinions authored and owned by one party, usually about many nodes. An .ifcx file is one way to serialise a layer; the layer is the logical unit, whatever the serialisation. A party can publish, edit or withdraw its layer without changing anyone else's. |
| **Tombstone** | An opinion stating that a node or a value is deleted. |
| **Inheritance** | A node takes the opinions of another node it inherits from (for example an occurrence from its type), without modifying that node. The inheriting node can add opinions of its own; an opinion stated directly on a node always takes precedence over an inherited opinion on the same information. |
| **Occurrence** | An object that instantiates a type, as in IFC's type/occurrence pattern. Use *occurrence*, not *instance*: in STEP and IFC every entity in a file is an instance of a schema entity, so *instance* is too generic. |
| **Composition** | The process of combining several layers into one result. |
| **Composed model** | The result of a composition: what a user or tool actually reads. |
| **Responsibility** | Which party is entitled to state opinions about which information of which objects (as in a responsibility matrix or LOIN). |
| **Precedence** | The rule that decides which opinion applies when several opinions address the same information. An opinion stated directly on a node always takes precedence over an opinion the node inherits. Between layers, precedence is derived from responsibility and time, not simply from order. *(See Q14.)* |
| **Alpha** | The current IFCX prototype: the schema, reference implementation and examples in the buildingSMART IFC5 development repository, at the commit named in the register's Mechanisms section. |

## Concepts and mechanisms

Used in the IFC 4.3 and IFCX comparison ([IFC4x-IFC5-constructs.md](IFC4x-IFC5-constructs.md)).

| Term | Definition |
|---|---|
| **Concept** | Something that can be represented, in IFC 4.3 and in IFCX alike, stated without saying how: for example identity, placement, material association or georeferencing. Concepts come from the IFC 4.3 schema, not from IFCX. A concept is not a capability: a capability is an ability IFCX provides (`C`), a concept is what a model can say, and a capability may serve several concepts. |
| **Mechanism** | How something is represented. In IFCX this is the `M` tag above: a rule or structure of the format, such as a child link or an attribute with a schema. In IFC 4.3 it is an entity, an attribute or an `IfcRel*` relationship of the schema. The comparison table gives, for each concept, the mechanism of each side. One concept can have several mechanisms on one side, and one mechanism can serve several concepts. |

---

## When several parties address the same object

| Case | Definition |
|---|---|
| **Enrichment** | Several layers add *different* opinions about the same object. No conflict: the object is completed progressively (for example, the structural engineer states the concrete grade, the fire engineer states the fire resistance). |
| **Alternative (option)** | Several layers deliberately give different answers for the same things, for a limited period, until one is selected. See NUC 12. |
| **Replacement** | An opinion replaces an earlier one about the same information, made by a party entitled to do so (for example design value → as-built value). The earlier opinion remains recoverable. |
| **Conflict** | Two layers state different values for the same information without being alternatives or a replacement. Must be detected and shown, not resolved silently. |

---

## Provisional terms

*Layer* and *opinion* are kept for now, so the group can review the NUCs in their new structure using familiar terms. They are planned to be renamed later in one bulk change. The definitions do not change; only the term does.

| Current term | Planned new term | Why |
|---|---|---|
| layer | contribution | "Layer" clashes with CAD and BIM layers. |
| opinion | statement | "Opinion" suggests facts such as a wall's length or fire rating are a matter of opinion. |

When the renaming is done, apply it to every NUC, `register.md`, `glossary.md` and `nuc-rewrite-instructions.md`, including plural forms and phrases ("opinion layer", "thin layer").

## Retired terms

| Do not use | Use instead |
|---|---|
| layer stack | set of layers + precedence |
| override | replacement (replaces a value) or enrichment (adds a value). "Override" stays when describing today's IFC/STEP practice, for example IFC's property override between a type and its occurrences. |
| opinion layer | layer |
| combined view, federated view | composed model |
| view (for authored data) | layer |
| broadcasting | inheritance |
| delta (for IFCX) | layer containing only changes. "Delta" stays when describing today's IFC/STEP practice. |

*Origin:* "layer", "opinion" and "stack" come from Pixar's Universal Scene Description (USD), on which the IFCX prototype's composition model is based. In USD, layers are ranked by strength and the strongest opinion wins; in these NUCs, which opinion applies is decided by precedence (see above), not by stacking order alone.

## Terms to avoid (clash with existing BIM meanings)

| Term | Clashes with |
|---|---|
| view | IFC Model View Definitions (MVD); application protocols |
| viewpoint | BCF viewpoints |
| aspect | ISO 81346 aspects |
| overlay | CAD xrefs / overlays |
| package, container | ISO 19650 information containers |
| instance (for an occurrence) | STEP instances: every entity in a STEP or IFC file is an instance of a schema entity |

*"Layer" also clashes with CAD and BIM layers, which IFC calls presentation layers; it is used provisionally (see Provisional terms).*
