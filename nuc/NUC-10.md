# NUC 10: Organising the same data in several structures, none of them canonical

**Original title:** Arbitrary spatial structures

**Related NUCs:** NUC 2 addresses partial and evolving information, NUC 12 addresses first-class options, and NUC 13 addresses reference-first access to distributed data.

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Building and infrastructure data has no single natural hierarchy. A designer, a contractor, an operator and a renovation team each need to navigate the same information by their own discipline, task or lifecycle phase. When one spatial hierarchy is built into the data, every other way of organising it means duplicating the data, restructuring it or cross-linking it by hand.

## 2. What we want to achieve

- `W38` Different parties can each organise the same data in their own arrangement, such as a navigation structure, or a placement relative to world coordinates, a wall, a floor, connected equipment, an alignment or a surveyed object, with no arrangement treated as the authoritative shape of the data, and a user or tool can choose which arrangement to use, or create its own. *(see also NUC 11)*
- `W39` A party can create an arrangement over data owned by others, such as a structure, a placement scheme or an option, or change its own and keep earlier ones for comparison, without copying or modifying that data or another party's arrangement, and without write access to the data. An option can add alternative data of its own, and defining which objects belong to it does not require changing them. *(see also NUC 11, NUC 12)*

## 3. IFCX capabilities

- `C17` **Purpose-specific arrangements.** A party can arrange existing data for a particular purpose, such as a navigation hierarchy, a placement scheme or a set of alternatives, without copying or modifying that data; several arrangements can coexist over the same data, and a user or tool selects the one it needs.
  *In this NUC: `W38`, `W39`*
- `C05` **Building on others' data.** A party can add to, annotate, specialise or, where it is responsible, replace another party's objects and definitions without changing the original.
  *In this NUC: `W39`*

## 4. What happens in IFC-STEP today

**STEP (language):** No limitation. Nothing in STEP/EXPRESS prevents a schema from separating data from the organisational structure used to navigate it.

**IFC schema:**
- `IL18` In IFC, object data, decomposition/containment relationships, and placement chains are embedded in the same instance graph; groups and systems add further associations, but the common project-site-facility-storey decomposition stays closely coupled to navigation, containment, and geometry resolution.
- `IL19` In IFC, alternative discipline- or task-specific hierarchies must be added as more relationships within the single instance graph that also holds decomposition, containment, and placement data, via external conventions, or as separately restructured models.
- `IL20` IFC has no mechanism to publish object data independently and apply interchangeable, separately authored structures over it without duplication; a schema revision could add one.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Concurrent lifecycle structures of one building

A building is being designed, operated, constructed, and renovated at the same time. Designers navigate it by design discipline and building system, the contractor by work package and installation sequence, the operator by maintainable system, and the renovation team by intervention zone and phase. Each party composes its own structure over the same data. No party's hierarchy becomes the required shape of the model, and no duplicate model is created for any structure.

### 2. Track assets crossing a building structure

A rail project contains track assets and relationships that pass through stations and other buildings. A building-oriented structure places those objects within the facility and storey hierarchy. A track engineer instead needs to navigate every relevant object and relationship as part of the track, regardless of which building contains it. Both structures reference the same assets, allowing each user to see a hierarchy suited to the task without reorganising or copying the underlying data.

### 3. Electronic door hardware viewed through the door

An electrical engineer needs to find electronic locks, contacts, readers, and their connections through the doors they serve rather than only through a separate electrical-system hierarchy. Other users may organise the same devices by system, procurement package, space, or maintenance route. IFCX permits each structure to reference the same door and hardware data, so navigation can follow the relationship most useful to the current user.
