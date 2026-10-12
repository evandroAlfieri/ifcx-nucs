# NUC 11: Placing objects relative to a chosen basis, with intent and tolerances explicit

**Original title:** Goal-specific relative placement

**Related NUCs:** NUC 10 separates data from any one hierarchy, NUC 6 addresses stable identity through change, and NUC 9 addresses placement of reusable assemblies.

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

One placement per object is not enough for everyone who uses it. World coordinates say where an object is, but not how it is dimensioned, built or surveyed in relation to something else: a window to its wall, a wall to the one before it, a unit of equipment to the equipment it connects to, a rail asset to an alignment. When only the resolved placement is exchanged, those relationships and their tolerances stay in drawings or in authoring-tool logic, and nobody can check them from the data. Today's IFCX prototype also places each object mainly through one hierarchy, alongside other techniques whose interaction still needs clarifying.

## 2. What we want to achieve

- `W38` Different parties can each organise the same data in their own arrangement, such as a navigation structure, or a placement relative to world coordinates, a wall, a floor, connected equipment, an alignment or a surveyed object, with no arrangement treated as the authoritative shape of the data, and a user or tool can choose which arrangement to use, or create its own. *(see also NUC 10)*
- `W39` A party can create an arrangement over data owned by others, such as a structure, a placement scheme or an option, or change its own and keep earlier ones for comparison, without copying or modifying that data or another party's arrangement, and without write access to the data. An option can add alternative data of its own, and defining which objects belong to it does not require changing them. *(see also NUC 10, NUC 12)*
- `W42` For any placement, a user or tool can read what it is relative to, the rule or tolerance behind it, and whether it was set directly, set relative to another object, or derived from relationships or constraints, so that everyone resolving it arrives at the same position.
- `W43` When one placement changes, for example after a survey, its effect on the placements that depend on it can be evaluated against stated tolerances and clearances before work continues.

## 3. IFCX capabilities

- `C17` **Purpose-specific arrangements.** A party can arrange existing data for a particular purpose, such as a navigation hierarchy, a placement scheme or a set of alternatives, without copying or modifying that data; several arrangements can coexist over the same data, and a user or tool selects the one it needs.
  *In this NUC: `W38`, `W39`*
- `C05` **Building on others' data.** A party can add to, annotate, specialise or, where it is responsible, replace another party's objects and definitions without changing the original.
  *In this NUC: `W39`*
- `C18` **Placement intent.** A placement can state what it is relative to, by which rule and within what tolerance, and how it was obtained, so that it can be evaluated and re-evaluated from the exchanged data.
  *In this NUC: `W42`, `W43`*

## 4. What happens in IFC-STEP today

**STEP (language):** No limitation, as with NUC 10 - nothing in STEP/EXPRESS precludes multiple, interchangeable placement graphs over the same data.

**IFC schema:**
- `IL21` IFC supports local, grid, and infrastructure-oriented linear placement, with local placements forming relative chains - but an occurrence exposes one placement per model state, commonly resolved to a single world-space result tied to containment/decomposition structure.
- `IL22` IFC provides no first-class, interchangeable placement graphs that different users or phases can author over the same occurrence data and select for a given evaluation.
- `IL23` In IFC, a relative placement transform doesn't itself communicate the dimensioning rule, tolerance, or constraint that motivated it - that intent stays in drawings or application-specific data, and alternative placement schemes require duplicated occurrences or separately maintained models.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Window and wall dimensional intent

A designer places a window relative to its host wall and the wall relative to a floor datum. The resolved world coordinates are useful for rendering, but the relative placement chain communicates how the opening should be dimensioned and checked. A contractor can evaluate the installed window against the wall rather than against a distant project origin, while both parties continue to reference the same object data.

### 2. Tolerance propagation during robotic layout

An installed wall is surveyed 25 mm from its intended position. The next wall was designed relative to the first, but following the measured offset may violate a required clearance or compound the error across the building. Explicit placement dependencies allow a layout robot or field application to compare the design datum, the as-built wall, and the downstream relative placement before work continues. A world-coordinate result alone cannot communicate which reference should govern that decision.

### 3. Mechanical installation relative to installed work

A mechanical contractor initially lays out equipment from the building grid, then needs to coordinate a connecting run relative to equipment and supports already installed in the field. A construction-specific placement graph can use the surveyed components as reference bases, while the designer retains the design placement graph and the operator later selects a service-oriented one. All three resolve the same equipment data for different purposes.

### 4. Rail assets re-referenced after survey

A rail asset is designed relative to an alignment. After installation and survey, another asset must be positioned relative to that installed object rather than directly from the alignment because their relationship controls performance. IFCX should allow the placement basis to change or coexist without duplicating either asset, while retaining enough intent to compare the design, survey, and operational conditions.
