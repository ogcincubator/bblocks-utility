
# Compound Name (Schema)

`ogc.bbr.utils.compoundName` *v0.1*

A multiple part name, consisting of a set of strings with functional roles that can be combined into single string using a template.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Example CompoundName
A name with a label, but also a set of parts with roles that can be validated against content rules.
#### json
```json
{
    "id": "CompoundNameExample",
    "type": "CompoundName",
    "label": "IS II - DP 3333",
    "comment": "note: label may be absent or subject to rules regarding presence of parts",
    "hasPart": [
        {
            "type": "Source",
            "label": "DP 3333"
        },
        {
            "type": "Stamp",
            "label": "IS II"
        }
    ]
}
```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-utility/build/annotated/bbr/utils/compoundName/context.jsonld",
  "id": "CompoundNameExample",
  "type": "CompoundName",
  "label": "IS II - DP 3333",
  "comment": "note: label may be absent or subject to rules regarding presence of parts",
  "hasPart": [
    {
      "type": "Source",
      "label": "DP 3333"
    },
    {
      "type": "Stamp",
      "label": "IS II"
    }
  ]
}
```

#### ttl
```ttl
@prefix commonpatterns: <https://w3id.org/ogc/utils/label/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

[] rdfs:label "IS II - DP 3333" ;
    dcterms:hasPart [ rdfs:label "DP 3333" ;
            commonpatterns:namePartType "Source" ],
        [ rdfs:label "IS II" ;
            commonpatterns:namePartType "Stamp" ] .


```


### Referenced Parts
An example name where part of the name is a reference to a vocabulary source.  This can us used for validation and multi-linual applications
#### json
```json
{
    "id": "CompoundNameExample",
    "type": "CompoundName",
    "label": "IS II - DP 3333",
    "comment": "the label of the part is optional - but can be cross checked",
    "hasPart": [
        {
            "type": "wa-plan:planTypes",
            "ref": "wa-plan-register:dp333",
            "label": "DP 3333"
        },
        {
            "type": "Stamp",
            "label": "IS II"
        }
    ]
}
```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-utility/build/annotated/bbr/utils/compoundName/context.jsonld",
  "id": "CompoundNameExample",
  "type": "CompoundName",
  "label": "IS II - DP 3333",
  "comment": "the label of the part is optional - but can be cross checked",
  "hasPart": [
    {
      "type": "wa-plan:planTypes",
      "ref": "wa-plan-register:dp333",
      "label": "DP 3333"
    },
    {
      "type": "Stamp",
      "label": "IS II"
    }
  ]
}
```

#### ttl
```ttl
@prefix commonpatterns: <https://w3id.org/ogc/utils/label/> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

[] rdfs:label "IS II - DP 3333" ;
    dcterms:hasPart [ rdfs:label "DP 3333" ;
            commonpatterns:namePartRef "wa-plan-register:dp333" ;
            commonpatterns:namePartType "wa-plan:planTypes" ],
        [ rdfs:label "IS II" ;
            commonpatterns:namePartType "Stamp" ] .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
description: Compound Name
anyOf:
- required:
  - label
- required:
  - hasPart
additionalProperties: true
properties:
  label:
    anyOf:
    - type: 'null'
    - type: string
    x-jsonld-id: http://www.w3.org/2000/01/rdf-schema#label
  template:
    type: string
  hasPart:
    type: array
    items:
      type: object
      additionalProperties: false
      properties:
        label:
          type: string
          x-jsonld-id: http://www.w3.org/2000/01/rdf-schema#label
        ref:
          $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml
          x-jsonld-id: https://w3id.org/ogc/utils/label/namePartRef
        type:
          $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml
          x-jsonld-id: https://w3id.org/ogc/utils/label/namePartType
      anyOf:
      - required:
        - label
      - required:
        - ref
    x-jsonld-id: http://purl.org/dc/terms/hasPart
x-jsonld-extra-terms:
  name: https://w3id.org/ogc/utils/label/name
  CompoundName: https://w3id.org/ogc/utils/label/CompoundName
x-jsonld-prefixes:
  commonpatterns: https://w3id.org/ogc/utils/label/
  dct: http://purl.org/dc/terms/
  rdfs: http://www.w3.org/2000/01/rdf-schema#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-utility/build/annotated/bbr/utils/compoundName/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-utility/build/annotated/bbr/utils/compoundName/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "name": "commonpatterns:name",
    "CompoundName": "commonpatterns:CompoundName",
    "label": "rdfs:label",
    "hasPart": {
      "@context": {
        "ref": "commonpatterns:namePartRef",
        "type": "commonpatterns:namePartType"
      },
      "@id": "dct:hasPart"
    },
    "commonpatterns": "https://w3id.org/ogc/utils/label/",
    "dct": "http://purl.org/dc/terms/",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-utility/build/annotated/bbr/utils/compoundName/context.jsonld)

## Sources

* [CSDM model](https://github.com/icsm-au/3d-csdm)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-utility](https://github.com/ogcincubator/bblocks-utility)
* Path: `_sources/compoundName`

