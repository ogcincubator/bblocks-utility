Many regulations require complex naming rules, where components of a name must match various content control rules.

This model defines a simple pattern for **compound names**, allowing applications to add additional rules to profile this for specific applications.

This ontology was originally the Common Patterns module of the ICSM 3D Cadastral Survey Data Model (3D CSDM)
(`https://linked.data.gov.au/def/csdm/commonpatterns`). It has been generalised for reuse in the
`https://w3id.org/ogc/utils/label/` namespace, which is also used by the Compound Name (`ogc.bbr.utils.compoundName`)
JSON-LD context.

## SHACL rules

The SHACL rules for compound names live here rather than in the Compound Name schema block, which depends on this block
and inherits them. The rules follow the RDF produced from the Compound Name JSON encoding:

- **Compound name:** a label, one or more `dct:hasPart` name parts, or both. Where both are present, the label of each
  part must appear in the compound label.
- **Name part:** a label (`rdfs:label`), a reference to what it names (`namePartRef`), or both, and optionally a
  functional type (`namePartType`). The reference and the type are IRIs.


The compound name rules apply to two kinds of node: instances of `CompoundName`, and values of `<https://w3id.org/ogc/utils/label/name>`. Compound names
that are neither are not checked. This includes compound names reached through a sub-property of `name` (validation does
not apply RDFS inference) and the untyped top-level object of a Compound Name JSON document. To have such names checked,
type them as `CompoundName`. 

