
# Compound Name Model (Model)

`ogc.bbr.utils.compoundName.ontology` *v0.1*

Ontology and SHACL rules for common implementation patterns not directly supported by other standards: compound names and name parts, qualified measures, jurisdictional codelists and reports.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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


## Examples

### Compound name with typed and referenced parts
A name whose label is composed of parts. Each part has a label, a reference to what it names, or both,
and optionally a functional type. The label of each part must appear in the compound label.
#### turtle
```turtle
@prefix com: <https://w3id.org/ogc/utils/label/> .
@prefix dct: <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix ex: <http://www.example.com/namedobjects/> .
@prefix nametype: <http://www.example.com/nametypes/> .
@prefix namerefs: <http://www.example.com/namerefs/> .

ex:lot1 com:name [
    a com:CompoundName ;
    rdfs:label "IS II - DP 3333" ;
    dct:hasPart [ com:namePartType nametype:planTypes ; com:namePartRef namerefs:dp333 ; rdfs:label "DP 3333" ] ,
                [ com:namePartType nametype:Stamp ; rdfs:label "IS II" ]
  ] .

```


### Specialised compound name class
A local subclass of CompoundName. Its instances are validated by the CompoundName rules, provided the
rdfs:subClassOf statement is available to the validator (here it is included in the data).
#### turtle
```turtle
@prefix com: <https://w3id.org/ogc/utils/label/> .
@prefix dct: <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix ex: <http://www.example.com/namedobjects/> .
@prefix nametype: <http://www.example.com/nametypes/> .
@prefix namerefs: <http://www.example.com/namerefs/> .

ex:PlanName rdfs:subClassOf com:CompoundName .

ex:plan1 a ex:PlanName ;
  rdfs:label "IS II - DP 3333" ;
  dct:hasPart [ com:namePartType nametype:planTypes ; com:namePartRef namerefs:dp333 ; rdfs:label "DP 3333" ] ,
              [ com:namePartType nametype:Stamp ; rdfs:label "IS II" ] .

```


### Specialised name property
Local sub-properties of com:name (directly or transitively). Their values are validated by the
CompoundName rules, provided the rdfs:subPropertyOf statements are available to the validator
(here they are included in the data).
#### turtle
```turtle
@prefix com: <https://w3id.org/ogc/utils/label/> .
@prefix dct: <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix ex: <http://www.example.com/namedobjects/> .
@prefix nametype: <http://www.example.com/nametypes/> .

ex:officialName rdfs:subPropertyOf com:name .
ex:registeredName rdfs:subPropertyOf ex:officialName .

ex:lot1 ex:officialName [
    rdfs:label "IS II - DP 3333" ;
    dct:hasPart [ rdfs:label "DP 3333" ] , [ com:namePartType nametype:Stamp ; rdfs:label "IS II" ]
  ] ;
  ex:registeredName [ rdfs:label "Lot 1" ] .

```


### Qualified measurement
#### turtle
```turtle
@prefix com: <https://w3id.org/ogc/utils/label/> .
@prefix ex: <http://www.example.com/measures/> .

ex:m1 a com:Measure ;
  com:value 17.055 ;
  com:qualityMeasure 0.05 .

```


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-utility](https://github.com/ogcincubator/bblocks-utility)
* Path: `_sources/compoundName/ontology`

