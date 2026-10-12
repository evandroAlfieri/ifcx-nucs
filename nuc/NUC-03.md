# NUC 3: Retrieving only the parts of a model a user or tool needs

**Original title:** In-browser streaming and selective node loading

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

BIM models keep growing, but IFC can only be exchanged as a complete file. Reaching one floor, one system or one changed element means downloading and parsing the whole model, so web viewers, mobile access and targeted automation are slow and expensive to build. Automated checks such as clash detection re-read the full model on every run, which makes continuous checking impractical on large projects. An authority receiving models from many applicants can spend weeks converting each file before any assessment begins.

## 2. What we want to achieve

- `W34` A user or tool can retrieve a specific part of a model, such as a single object, a storey with everything in it, or all objects of one system, and can load a model progressively, showing a first part, such as the spatial structure, and fetching further parts only when they are needed, without downloading or reading the rest of the model.
- `W35` A tool can read model data with ordinary web technology, such as a web browser, without dedicated middleware or pre-processing.
- `W15` Downstream processes, such as clash detection, can run on only the objects affected by a set of changes, without processing the whole model.
- `W26` An organisation can publish its data, such as a dataset or a manufacturer's product types, so that other parties and their tools use it directly at its source instead of holding copies, and see its current state, for example new or updated products when they are released, without static exports, imports or separate data transfers. A manufacturer can also learn which of its types a design uses, without a separate data transfer. *(see also NUC 13)*

## 3. IFCX capabilities

- `C14` **Selective access.** Any part of a model, such as a single object, a subtree or a filtered subset, can be retrieved on its own and on demand, by any client including a web browser, without retrieving or reading the rest of the model.
  *In this NUC: `W34`, `W35`*
- `C06` **Change-only exchange.** Additions, changes and deletions since a previous state can be exchanged on their own, validated on their own, and applied to an existing copy with the same result as a full exchange.
  *In this NUC: `W15`*
- `C10` **References.** Data can point to objects in other models and to external resources in a way any tool recognises, and the target of a reference can be reached (see Q49).
  *In this NUC: `W26`*
- `C12` **Published data.** A party can publish data, such as a dataset or a product library, that others use directly at its source instead of copying, following either its current state or a fixed version and, where allowed, writing to it; any local copy can be checked against the source, so it is never silently taken as current.
  *In this NUC: `W26`*

## 4. What happens in IFC-STEP today

**STEP (language):**
- `SL05` STEP's classic Part 21 Clear Text Encoding file is a sequential text stream in which every entity is addressed by a local integer (#N), meaningful only within that file.
- `SL06` STEP's Part 21 Clear Text Encoding has no index of instance locations, so a reader must scan the file to locate the byte position of a given `#N` reference; there is no way to jump directly to an arbitrary instance without such a scan or a separately built index.
- `SL07` STEP's Part 21 Clear Text Encoding has no random-access index or pagination primitive native to it; splitting a model across multiple "4;2" files reduces size per unit but doesn't remove the per-file full reference-resolution pass.
- This applies specifically to this classic encoding, not necessarily to STEP as a whole - other STEP capabilities/encodings could support more granular access.

**IFC schema and implementation:**
- `IL07` IFC has not adopted alternative STEP encodings, so current IFC tooling needs either a full file download/parse or purpose-built middleware with its own index - non-standardised, costly infrastructure.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Progressive loading of a large hospital model in a browser

A 500,000-node hospital model is served over HTTP. A facilities manager opens it in a browser-based viewer. Under IFC, the viewer must download and parse the full 2 GB file before rendering anything - a process that takes minutes and fails entirely on a mobile connection. Under IFCX, the viewer requests only the spatial structure first: the site, building, and storey nodes load in seconds. The manager navigates to Level 3 and requests only that storey's nodes. Individual room geometries load on demand as she drills in. No middleware, no pre-processing, no desktop application required.

### 2. CI/CD quality pipeline querying only changed elements

A large design practice runs automated clash detection on every model commit. Under IFC, the checking pipeline must re-parse the full model on every run - 45 minutes for a large project, which makes continuous checking impractical. Under IFCX, the pipeline requests only the nodes that changed since the last commit, identified by their stable UUID paths. A typical commit touches 20-200 nodes. Each check completes in under 2 minutes. Quality feedback reaches designers before the next stand-up, not the next day.

### 3. Urban planning platform querying multiple submitted models

A metropolitan council assesses 14 development applications simultaneously. Each applicant's IFCX model is an addressable endpoint. The council's urban simulation platform queries volume, floor area, and use classification attributes directly from each model via API - without downloading any complete file. Shadow, transport, and wind assessments run against live data. All 14 assessments complete within 3 days of submission. Under IFC, the urban modelling team spends two weeks converting and integrating each submitted file before any assessment can begin.
