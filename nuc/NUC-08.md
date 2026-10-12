# NUC 8: Linking model data to external resources through typed, recognisable references

**Original title:** Dereferenceable semantic linking to external data

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Building data is expected to connect to outside sources such as classification dictionaries, product databases, regulatory registers and facility management or IoT systems, and models also need to point to each other, for example from a valve to the space it serves or from a work task to the components it concerns. IFC has no standard, schema-enforced way to make an attribute a typed pointer to an external resource: references sit as plain text in fields meant for something else, how to resolve them is left to agreement between parties, and they go stale when the resource moves. At handover, assets must carry operation and maintenance data structured to the client's data dictionary, often linked to bSDD, yet it usually arrives as a large IFC file plus a COBie spreadsheet that import badly into facility management systems, followed by months of manual data entry.

## 2. What we want to achieve

- `W23` An attribute value can be declared to be a reference to an external resource, such as a classification entry, product data, a certification, a facility management record or a sensor endpoint, so that any tool can tell a reference from ordinary text and recognise what kind of resource it points to.
- `W24` A user or tool holding a reference to an object in another model, or to an external resource, can follow it and read the target's current content from its source at any time, without the model being updated when the target changes, for example a work task reading the areas and colour of the walls it concerns, or a third-party platform following references to compile a material passport that stays traceable to its sources. *(see also NUC 13)*
- `W25` At handover, a receiving system can take over a model directly and check that every external reference in it resolves and every classification is valid against its source, without a separate spreadsheet or manual data entry.
- `W14` A set of changes can be validated and read on its own, without the rest of the model; a receiver can see which objects the sender deleted; and a change can carry a link to external evidence, such as an inspection certificate. *(see also NUC 7)*
- `W12` A sender can send only the information added, changed or deleted since a previous state, down to a single attribute of one object, instead of the whole model, using the same tools it already uses to exchange complete models. *(see also NUC 7)*

*Access to other organisations' data at its source, and building systems writing to models, are covered in NUC 13, where this NUC's former scenarios 3 and 5 now sit.*

## 3. IFCX capabilities

- `C10` **References.** Data can point to objects in other models and to external resources in a way any tool recognises, and the target of a reference can be reached (see Q49).
  *In this NUC: `W23`, `W24`, `W14`*
- `C13` **Self-describing data.** The meaning of every attribute is defined by a recognisable definition governed by its owner, so independent tools can interpret the data without bespoke mapping.
  *In this NUC: `W23`, `W25`*
- `C12` **Published data.** A party can publish data, such as a dataset or a product library, that others use directly at its source instead of copying, following either its current state or a fixed version and, where allowed, writing to it; any local copy can be checked against the source, so it is never silently taken as current.
  *In this NUC: `W24`*
- `C06` **Change-only exchange.** Additions, changes and deletions since a previous state can be exchanged on their own, validated on their own, and applied to an existing copy with the same result as a full exchange.
  *In this NUC: `W14`, `W12`*

**Not claimed**
- IFCX does not claim that a URI attribute is linked data in the RDF sense: the URI carries no inherent semantics, and resolving it is a convention a consuming tool chooses to implement, not a protocol the format enforces. The claim is limited to structural clarity and namespace addressability (`C10`, `C13`), not a resolution guarantee.

## 4. What happens in IFC-STEP today

**STEP (language):** No language-level limitations - object-level classification (below) already shows a schema-typed reference is achievable in EXPRESS. The gaps here are attributable to the current IFC schema, not the STEP language.

**IFC schema:**
- Object-level classification already works: `IfcClassificationReference` + `IfcRelAssociatesClassification` link an object to an external entry, dereferenceable via bSDD's API where applicable.
- `IL13` IFC provides `IfcPropertyAbstraction.HasExternalReferences`, a relationship linking an individual property to an external reference; IFC2x3 has no equivalent. The documented plain-text convention (`IfcPropertySingleValue.Specification`/`.Description`) still isn't schema-typed as a URI, and both mechanisms are inconsistently used in practice.

**Implementation note:** whether a tool resolves a reference, and whether write-back to the source is possible, are implementation questions independent of schema or language.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Digital handover with validated external references

A 60,000 m² hospital is handed over to the FM team. 3,200 maintainable assets must carry O&M data structured to the client's data dictionary, linked via bSDD. Under IFC, the contractor delivers a 2 GB IFC file and a 400-sheet COBie spreadsheet. Neither import correctly; three months of manual data entry follows. Under IFCX, every asset attribute referencing a bSDD classification resolves to a machine-readable definition at the bSDD URI. Warranty documents and supplier records are live URI references, not embedded text. At handover, the CAFM system ingests the IFCX model directly: every classification is validated against the live bSDD schema, every external link is verified as resolvable. Data completeness is confirmed before the FM team opens the building, not three months after.

### 2. Progressive as-built records with linked evidence

A motorway widening project has 1,400 drainage structures to install over 18 months. As each is installed, the supervisor's app pushes a minimal layer containing only changes: status, date, inspector ID, and a URI pointing to the externally stored inspection certificate. Any party - client, contractor, regulator - can dereference that URI at any time and retrieve the current certificate. If the certificate is superseded, the updated document is available at the same URI without any model update. Under IFC, the certificate reference would be an embedded string in a property set: untyped, unverifiable, and gone stale the moment the document moves.

### 3. Digital Product Passport with live EPD resolution

A 200-unit residential development targets a circular economy rating. Every product instance in the IFCX model carries a persistent URI to its Digital Product Passport, hosted by the manufacturer or a certification body. When a manufacturer updates an EPD, all referencing building models resolve the updated data on demand - no manual model corrections, no stale property sets. At practical completion, the investor's ESG platform queries the live IFCX model and generates the material passport with verified carbon data for each product, directly traceable to the manufacturer's live certification endpoint.

### 4. References between domain models *(moved from NUC 6)*

In construction there are multiple needs for references between domain models. For example, a valve in a ventilation model refers to the space it is serving. A work task in a work schedule refers to the components that the task deals with. In IFCX it is simple to refer to an already existing component in a different model. So a work task can refer to those and get, for example, their quantities and other attributes. If a task is about painting walls, it is easy to get the areas and color of the walls to be painted.
