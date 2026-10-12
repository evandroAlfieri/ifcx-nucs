# NUC 12: Developing design alternatives that share common data without copying it

**Original title:** First-class options without duplication

**Related NUCs:** NUC 1 addresses parallel authoring in separate layers, NUC 6 addresses stable identity, and NUC 7 addresses changes between versions. Like the external structures in NUC 10 and placement definitions in NUC 11, option definitions must not require modification of the data they reference.

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Design teams often work on several alternatives at once, and most of the project is common to all of them: the site, the rooms, most walls, the track. Only a few elements differ. An option is not a version: a version is the same data at an earlier point in its history, while options exist side by side at the same time. In file-based exchange each option has to carry its own copy of the common elements, and nothing in the format tells deliberate option membership from data that merely happens to be repeated. Today's IFCX prototype has no first-class options either.

## 2. What we want to achieve

- `W39` A party can create an arrangement over data owned by others, such as a structure, a placement scheme or an option, or change its own and keep earlier ones for comparison, without copying or modifying that data or another party's arrangement, and without write access to the data. An option can add alternative data of its own, and defining which objects belong to it does not require changing them. *(see also NUC 10, NUC 11)*
- `W40` A user or tool can select an option, obtain its complete composed model, and switch between options. Data common to several options is stored once and shared by them, only the data that differs being added, replaced or omitted per option. Several options can be developed at the same time as the current state of the data, without invalidating or rewriting it, and an option can be discarded without affecting its sources.
- `W41` Users and tools can compare options and see which data they share and where they differ.
- `W09` A user or tool can tell whether two compositions are alternatives that coexist or successive versions of the same data.
- `W28` A reference to a source dataset can follow the source's current state or stay on a fixed version of it, as chosen by the party making the reference. *(see also NUC 13)*

## 3. IFCX capabilities

- `C05` **Building on others' data.** A party can add to, annotate, specialise or, where it is responsible, replace another party's objects and definitions without changing the original.
  *In this NUC: `W39`*
- `C17` **Purpose-specific arrangements.** A party can arrange existing data for a particular purpose, such as a navigation hierarchy, a placement scheme or a set of alternatives, without copying or modifying that data; several arrangements can coexist over the same data, and a user or tool selects the one it needs.
  *In this NUC: `W39`, `W40`, `W41`*
- `C01` **Separate contributions.** Each party's data is kept as a distinct unit that the party owns and can add to, change or withdraw without affecting any other party's data.
  *In this NUC: `W40`*
- `C02` **On-demand composition.** The data of several parties can be combined into one composed model whenever needed, reflecting the current state of each party's data.
  *In this NUC: `W40`*
- `C03` **Precedence.** When several opinions address the same information, it can be determined which one applies and why, distinguishing enrichment, replacement, alternatives and conflict.
  *In this NUC: `W09`*
- `C07` **Change history.** Exchanged changes form an ordered, attributed history from which any earlier state can be reproduced.
  *In this NUC: `W09`*
- `C12` **Published data.** A party can publish data, such as a dataset or a product library, that others use directly at its source instead of copying, following either its current state or a fixed version and, where allowed, writing to it; any local copy can be checked against the source, so it is never silently taken as current.
  *In this NUC: `W28`*

## 4. What happens in IFC-STEP today

**Note on terminology:** "first-class options" needs clearer definition before its STEP/schema implications can be assessed with confidence; the bullets below have not been independently verified against STEP/EXPRESS's language-level capabilities to the same degree as other NUCs in this document.

**STEP (language):** No obstacle identified in STEP/EXPRESS to adding option-related entities in a future schema revision.

**IFC schema:**
- `IL24` IFC has no dedicated schema entities for simultaneous design options, shared membership across options, or external option sets.
- `IL25` In IFC, alternatives can be approximated with groups, classification conventions, property values, or separate files, but a general IFC consumer can't tell from those mechanisms which elements are common, mutually exclusive, or option-specific without prior agreement.
- `IL26` In IFC, when alternatives are exchanged as separate files, common objects are duplicated even if their GlobalIds are preserved, and changes must be coordinated across the copies.

Current file-based IFCX can approximate this with layers and repeated paths, but doesn't distinguish an option from a version or from ordinary duplicated data, and has no external option definition that collects data by reference without copying it. (This describes a current gap in IFCX itself, not an IFC/STEP limitation.)

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Client review of two design options

An architect presents two layouts to a client. The project, rooms, structural elements, and most walls are common to both; only a limited set of partitions, doors, and equipment differs. Each option references the common data once and adds only its alternative elements. The client can switch between complete compositions without the project team maintaining two copies of the unchanged model.

### 2. Renovation while a facility remains operational

An occupied space has a valid current configuration that must remain available to operators throughout a renovation study. Several proposed reconfigurations reference that operational data and add, replace, or omit elements within their own option definitions. The proposals coexist with the current condition without invalidating it, rewriting it, or requiring the renovation author to own it.

### 3. Agent-generated proposed solutions

An agent evaluates many possible layouts or infrastructure solutions. Each proposal references the same connected site, room, wall, track, and system data and contributes only its proposed changes. The alternatives remain identifiable as options rather than becoming unrelated copied datasets, allowing people and other agents to compare them, trace what is shared, and discard a proposal without affecting its sources.
