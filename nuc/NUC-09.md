# NUC 9: Defining an assembly once and reusing it everywhere, with changes reaching every occurrence

**Original title:** Formal assembly type instantiation

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Modular, prefabricated and repetitive construction is growing fast. IFC has no way to define an assembly once and reuse it by reference, so every placement of a repeated component carries a full copy of its parts, redefined by hand. When the specification changes, every copy has to be updated, manually or with a script that is written, tested and run separately for each project. Prefabrication workflows are therefore data-heavy, error-prone and cut off from live manufacturer information, and product data in design tools often comes from static catalogue imports that go out of date.

## 2. What we want to achieve

- `W17` A definition, such as a type, a component assembly or a spatial subsection with its sub-components, structure, relationships and attributes, can be defined once and used wherever it is needed without being duplicated in every placement, and every use reflects a later change to it without being updated by hand. This includes the parts of a type appearing under every occurrence without being redefined at each placement. *(see also NUC 2)*
- `W26` An organisation can publish its data, such as a dataset or a manufacturer's product types, so that other parties and their tools use it directly at its source instead of holding copies, and see its current state, for example new or updated products when they are released, without static exports, imports or separate data transfers. A manufacturer can also learn which of its types a design uses, without a separate data transfer. *(see also NUC 13)*
- `W18` A user can find out how many occurrences of each type a model contains, without counting them by hand.

## 3. IFCX capabilities

- `C09` **Reuse by definition.** A definition, such as a type, an assembly or a module, is stated once and used in many places; every use reflects changes to it, uses can be counted, and it can be used while still incomplete.
  *In this NUC: `W17`, `W18`*
- `C10` **References.** Data can point to objects in other models and to external resources in a way any tool recognises, and the target of a reference can be reached (see Q49).
  *In this NUC: `W26`*
- `C12` **Published data.** A party can publish data, such as a dataset or a product library, that others use directly at its source instead of copying, following either its current state or a fixed version and, where allowed, writing to it; any local copy can be checked against the source, so it is never silently taken as current.
  *In this NUC: `W26`*

## 4. What happens in IFC-STEP today

**STEP (language):** No limitations. Other STEP application protocols (e.g. AP242) already support nested reuse of instances within an assembly tree, indicating the language does not preclude this.

**IFC schema:**
- `IL14` IFC's `IfcTypeObject` gives limited type-occurrence separation for single objects only, not for assemblies (typed groups of sub-components with their own structure/relationships).
- `IL15` IFC has no schema mechanism to define a reusable typed assembly (e.g. beam-with-connections-and-reinforcement) and instantiate it by reference rather than copying every sub-component into every occurrence.
- `IL16` `IfcMappedItem`/`IfcRepresentationMap` let geometry be defined once and reused across occurrences via a shared representation and per-occurrence transform, so geometry need not be literally duplicated - the redundancy problem is narrower than full geometry copies.
- `IL17` `IfcLibraryReference` (via `IfcRelAssociatesLibrary`) is a real, URI-typed schema mechanism for linking an object to an external library entry, not just static file exports. What's missing is live resolution: an update at the source doesn't automatically propagate to the referencing object.
- Addressing this needs a schema change, not a change to the STEP language.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Precast beam library with live specification propagation

A precast concrete manufacturer defines a double-T beam assembly: beam body, two connection plates, reinforcement cage, four lifting anchors - each sub-component carrying typed attributes including section profile, concrete grade, and fire rating. A structural engineer places 3,400 instances across a car park. Each instance references the type definition by URI. When the manufacturer revises the shear stud specification to meet a revised Eurocode requirement, the change is made once. All 3,400 instances reflect the update immediately, in every project referencing that library. Under IFC, the same change requires touching 3,400 individual objects - manually or through a script that must be written, tested, and run separately for each project.

### 2. Mass timber housing with 22 panel types across 500 homes

A developer builds 500 homes using 22 standard structural panel types. Under IFC, 500 homes × 80 panels = 40,000 individual panel objects, each carrying its own property sets. Updating a fire rating specification means modifying all 40,000. Under IFCX, the 22 panel types are defined once in a manufacturer-hosted library. Each home contains 80 instance references. Updating Panel Type 7's fire rating propagates to all 3,200 instances across all 500 homes in a single edit. The fabrication system reads the live library directly - the CNC programming team receives updated specifications automatically, with no manual data transfer.

### 3. Manufacturer library as a live design tool endpoint

A curtain wall manufacturer publishes their full product range as a versioned IFCX type library at a stable URI. An architect's design tool subscribes to the library. When the manufacturer releases a new glazing unit with improved U-values, the tool reflects the update in the product selector immediately. When the architect places a unit, the instance references the manufacturer's live type definition - not a static import from last year's product catalogue. At tender stage, the quantity surveyor queries the instance count of each type directly from the model. The manufacturer receives confirmed specification data without a separate data transfer exercise.
