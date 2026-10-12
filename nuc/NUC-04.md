# NUC 4: Any organisation adding its own typed data without changing the core schema

**Original title:** Third-party typed domain extensions without schema governance

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

A built asset carries data from dozens of disciplines, each with its own classifications, vocabularies and regulations. IFC's schema changes only through a central standards process that usually takes years, so organisations that need their own typed data have no standard way to add it. The data ends up in property sets with informal names, which only tools built for that convention can interpret or validate. IDS can check that a property is present, but not that its value has the right type and meaning.

## 2. What we want to achieve

- `W31` Any organisation can define its own typed attributes, own and maintain their definition, and attach them to any object, without changing the core schema, without approval from a standards body, and without conflicting with attributes defined by other organisations on the same object.
- `W32` A tool that does not understand an organisation's attributes can still read the rest of the model, ignoring those attributes without failing.
- `W33` A tool that understands an organisation's attributes can check their values against that organisation's definition, including their data types, and data requirements, such as an IDS specification, can refer to both core and organisation-defined attributes, so that a model is checked automatically, including the type and meaning of values, not only their presence.

## 3. IFCX capabilities

- `C15` **Open extension.** Any party can define its own attributes and their meaning and attach them to any object, without changing the core definitions or needing anyone's approval; definitions from different parties coexist on the same object, and tools that do not know a definition can ignore it without failing.
  *In this NUC: `W31`, `W32`, `W33`*
- `C13` **Self-describing data.** The meaning of every attribute is defined by a recognisable definition governed by its owner, so independent tools can interpret the data without bespoke mapping.
  *In this NUC: `W33`*

## 4. What happens in IFC-STEP today

**STEP (language):**
- `SL08` EXPRESS is a closed-world schema language: every entity type and attribute must be declared in the schema before it can appear in a valid file. This is inherent to EXPRESS - and by extension STEP - not an IFC-specific choice. An open-world-assumption language would allow more flexibility, but that is a different language.
- `SL09` Because EXPRESS's closed-world declaration requirement is a language-level constraint, an independently governed, typed extension mechanism cannot be achieved within an EXPRESS-based schema without changing the underlying schema language.

**IFC schema:**
- No distinct schema-level limitation beyond the EXPRESS constraint above.
- `IL08` IFC's workaround for EXPRESS's closed-world constraint is `IfcPropertySet`. Property values are typed via `IfcValue`, but the property `Name` is an unconstrained string with no namespace, so nothing prevents name collisions across organisations.
- `IL09` IFC has a documented convention that lets a property carry a bSDD reference as a plain string, but it's unenforced by the schema and inconsistently adopted, so most property sets stay opaque to tools unaware of the specific naming convention.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Geotechnical data on infrastructure models

A geotechnical firm needs to attach borehole log data, soil classification attributes, and groundwater table references to IFCX nodes representing site terrain. They publish a geotec:: namespace schema on their own domain. Any tool that understands geotec:: reads the attributes with full type safety. Tools that do not simply skip them. No modification to the IFC core schema is required; no bSI working group approval is needed. Under IFC, the same data would live in IfcPropertySet entries with informal string names - untyped, unvalidatable, and interpretable only by tools that were specifically programmed to recognise that particular property set convention.

### 2. Jurisdiction-specific regulatory extensions

A national planning authority needs to attach jurisdiction-specific compliance attributes to building elements - fire compartment ratings, energy performance classifications, accessibility grades - structured to their national regulatory framework. Under IFC, these either wait for the next IFC release cycle or live in untyped property sets with no formal link to the regulatory schema. Under IFCX, the authority publishes a reg-dk:: namespace schema aligned to their national framework. Applicants' tools attach the attributes. The authority's validation platform checks them against the live schema. Any IFC-compliant tool that has not implemented reg-dk:: ignores the attributes gracefully without failing.

### 3. Machine-interpretable IDS requirements as validation gates

A client's data requirements are expressed as an IDS file referencing IFCX core concepts and domain-specific namespace attributes. Contractors validate continuously throughout construction - every model commit triggers a check against the IDS. At handover, the client runs a final automated check: every maintainable asset carries a maintenance interval, warranty expiry, linked supplier record, and geometry, all typed and validated against their namespace schemas. Under IFC, IDS can reference property set names but cannot enforce type correctness on untyped property set values - validation catches presence, not semantic correctness.
