# NUC 6: Keeping each object's identifier stable across tools, organisations and the whole lifecycle

**Original title:** Stable object identity through the full asset lifecycle

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

A built asset lives for decades, passing through design, construction, handover and operation, and through dozens of tools and organisations. In IFC, an object's identifier can change along the way, for example when it is moved to a different parent, passed between tools or re-exported, which silently breaks the BCF issues, IDS reports and asset register links that point to it. Each handover also risks mismatched property sets or COBie mapping errors that cut the link between an object and its records. Construction records such as as-built status are matched to design objects through lookup tables or by hand, with a risk of attaching a record to the wrong object.

## 2. What we want to achieve

- `W21` An object keeps one globally unique identifier through its whole lifecycle, so that identifiers from different projects and organisations do not collide, including when the object is modified, moved to a different parent, re-exported, combined into a larger model or handed over to another tool or organisation, and a party can rely on every tool to keep it, so that identity does not depend on one tool's behaviour. Information any party records about the object at any stage, such as as-built status or asset data at handover, stays attached to that same object, without lookup tables, manual matching or reconciliation.
- `W22` References to an object made by other tools and organisations, such as BCF issues, IDS reports and asset register entries, keep resolving to that object throughout its lifecycle.
- `W12` A sender can send only the information added, changed or deleted since a previous state, down to a single attribute of one object, instead of the whole model, using the same tools it already uses to exchange complete models. *(see also NUC 7)*

## 3. IFCX capabilities

- `C08` **Stable identity.** Every object has a globally unique identifier that stays the same across tools, organisations and its whole lifecycle, and conforming tools must preserve it.
  *In this NUC: `W21`, `W22`*
- `C10` **References.** Data can point to objects in other models and to external resources in a way any tool recognises, and the target of a reference can be reached (see Q49).
  *In this NUC: `W22`*
- `C06` **Change-only exchange.** Additions, changes and deletions since a previous state can be exchanged on their own, validated on their own, and applied to an existing copy with the same result as a full exchange.
  *In this NUC: `W12`*

## 4. What happens in IFC-STEP today

**STEP (language):**
- `SL10` STEP defines no language-level semantics for an identifier that automatically persists across independently produced files, applications, or transformations; any persistence guarantee must come from schema definition and consistent implementation.
- `SL03` STEP's "4;2" anchor mechanism requires the referenced entities to be named and nominated as anchors in advance; since in practice any component could become a reference target, this requires extensive up-front coordination between parties to establish links.
- `SL11` STEP's "4;2" anchors give no stability guarantee across model transformations and are not externally resolvable URIs.

**IFC schema:**
- `IL10` IFC's `GlobalId` is a 22-character compressed 128-bit GUID, generated to be globally unique, with no hierarchical structure or namespace. The schema imposes no requirement that it stay unchanged across model server operations.

**Implementation note:** GlobalIds have at times been regenerated on export or during model transformations, breaking downstream references. This reflects application behaviour, not a requirement or prohibition in the schema or language, and applies equally to any exchange format.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Element identity surviving a design change and BCF reference

A structural column is created during schematic design, referenced in a BCF issue during coordination, cited in an IDS validation report during detailed design, and linked from the FM asset register at handover - all using the same identifier. Midway through detailed design, the column is moved from one structural frame to another (a re-parenting operation). Under IFC, many tools issue a new GlobalId at this point, silently breaking the BCF issue reference, the IDS report link, and the FM asset register entry. Under IFCX, the UUID path identifier is stable through re-parenting. Every downstream reference continues to resolve correctly.

### 2. Progressive as-built record tied to design objects

A motorway project has 1,400 drainage structures. Each structure is created in the design model with a stable IFCX UUID path. As each is installed on site, the supervisor's app pushes a status update against that same UUID - no lookup table, no manual matching of as-built to design, no risk of mis-assignment. At handover, the client's asset management system already holds live references to all 1,400 objects. The design identity and the as-built record are the same node, continuously updated throughout construction.

### 3. Multi-organisation lifecycle traceability

A building product is specified by an architect, procured by a contractor from a different manufacturer than originally specified, installed by a subcontractor, commissioned by an MEP engineer, and registered in the FM asset register by the facilities manager - five organisations, five tools, one asset lifecycle. Under IFC, each transition risks a GlobalId change, a property set mismatch, or a COBie mapping error that severs the chain. Under IFCX, the product instance carries a stable URI from specification through end-of-life. Every organisation that touches it reads and writes against the same identifier. The full lifecycle record is continuously traceable without a reconciliation exercise at any handover point.
