# NUC 5: Rendering models in game engines and web viewers without a geometry kernel

**Original title:** Direct integration with game engine and web rendering pipelines

*Terms and tags (`W` want, `C` capability) follow [glossary.md](glossary.md) and [register.md](register.md).*

---

## 1. Current workflow and problem

Showing an IFC model usually needs a geometry kernel to turn B-rep geometry into meshes. A viewer either carries a heavy, often proprietary kernel, or relies on a separate visualisation file that is cut off from the live model and goes out of date. Getting a model into a game engine takes a chain of export, tessellation, conversion and import that can take hours and loses the link to the model's data. Today's engines and web renderers, such as Unreal, Unity or three.js, have no built-in IFCX reader.

## 2. What we want to achieve

- `W36` A game engine or web renderer can display a model's geometry with only a thin import step, without a geometry kernel.
- `W37` In a rendered display, a user can select an object and read its model data, such as its classification and properties, because the rendered object stays linked to that data.
- `W05` When a party changes its data, the change appears in the composed models and displays that use it, without a new file being sent, without manual re-assembly and without regenerating a separate visualisation file. *(see also NUC 1)*
- `W35` A tool can read model data with ordinary web technology, such as a web browser, without dedicated middleware or pre-processing. *(see also NUC 3)*
- `W27` External systems, such as building management systems or IoT controllers, can write data, such as readings and fault statuses, directly to specific objects in a model, and several authorised platforms can read that same current data. *(see also NUC 13)*

## 3. IFCX capabilities

- `C16` **Render-ready geometry.** Geometry can be expressed in forms that common real-time and web rendering pipelines consume directly, without a geometry kernel, and it stays part of the same object as the rest of that object's data.
  *In this NUC: `W36`, `W37`*
- `C02` **On-demand composition.** The data of several parties can be combined into one composed model whenever needed, reflecting the current state of each party's data.
  *In this NUC: `W05`*
- `C14` **Selective access.** Any part of a model, such as a single object, a subtree or a filtered subset, can be retrieved on its own and on demand, by any client including a web browser, without retrieving or reading the rest of the model.
  *In this NUC: `W35`*
- `C12` **Published data.** A party can publish data, such as a dataset or a product library, that others use directly at its source instead of copying, following either its current state or a fixed version and, where allowed, writing to it; any local copy can be checked against the source, so it is never silently taken as current.
  *In this NUC: `W27`*

**Not claimed**
- IFCX does not claim that game engines or web renderers can read IFCX data out of the box: a loader must still compose the data, including its layers and its separate placement and geometry nodes, before passing geometry to the renderer, so a renderer-side import layer is still bespoke work, though a lighter one. The claim is limited to removing the geometry kernel (`C16`).

## 4. What happens in IFC-STEP today

**STEP (language):** No inherent limitation. STEP geometry is most commonly associated with B-rep surfaces, NURBS, and procedural solids (Parts 42, 511, and related APs), but STEP also supports tessellated (mesh) geometry, including within AP242.

**IFC schema:** No inherent limitation. IFC already includes tessellated geometry representations (e.g. `IfcTriangulatedFaceSet`), so a schema-level path to mesh output exists.

## 5. Example scenarios

*The scenarios describe IFCX as the original authors imagined it, to make the examples realistic. They may name specific solutions; the mechanisms finally chosen may differ.*

### 1. Real-time design review in a game engine

An architect wants to walk through a proposed hospital ward in Unreal Engine with a client during a design review. Under IFC, the process is: export IFC, run through a geometry kernel to tessellate, export to FBX or glTF, import into Unreal, lose all semantic data in the process. Total pipeline time: hours. Semantic link to the model: none. Under IFCX, an importer resolves the composed model and hands USD-described meshes and glTF materials to the engine - a thin translation layer rather than a full geometry-kernel tessellation pipeline. The architect can select a wall in the engine and query its IFC classification, fire rating, and specification reference, because the semantic data never left the node.

### 2. Web-based project portal without plugin or middleware

A contractor's project portal needs to display the current composed model in a browser for subcontractors who do not have authoring tools. Under IFC, this requires either a dedicated IFC web viewer with a built-in geometry kernel (heavy, slow, expensive to operate) or a pre-baked geometry conversion pipeline that produces a separate visualisation file disconnected from the live model. Under IFCX, the portal's loader resolves USD geometry from the IFCX endpoint and renders it in three.js. Subcontractors see the current model state, select elements, and read their properties - from a standard browser, with no plugin, no conversion, no middleware.

### 3. Continuous rendering in a digital twin dashboard

A facilities management team operates a dashboard that displays the live state of a building - occupancy, fault alerts, energy readings - overlaid on a 3D model. Under IFC, the 3D model in the dashboard is a pre-baked static mesh, regenerated periodically from IFC exports, always slightly out of date. Under IFCX, the dashboard renders geometry directly from the live IFCX endpoint. When a fault alert is written to an AHU node by the BMS, the dashboard highlights that object in the rendered model immediately - because the geometry, the semantic data, and the live operational attributes all live on the same node.
