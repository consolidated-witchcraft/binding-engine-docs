# Vocabularies

BindingEngine vocabularies define the semantic rules used to validate bindings.

A vocabulary describes:
- which binding types exist
- which payload shapes are allowed
- which attributes are valid
- value types
- semantic roles
- structural constraints

Vocabularies provide the semantic layer of the BindingEngine pipeline.

---

## Purpose

The parser answers:

> “What syntactically exists in this document?”

The vocabulary layer answers:

> “Is this binding semantically valid under this vocabulary?”

This separation is intentional.

The parser remains:
- syntax-focused
- deterministic
- application-neutral

while vocabularies provide:
- semantic meaning
- domain-specific rules
- structural validation
- attribute semantics

---

## Vocabulary Structure

Vocabularies are typically represented as JSON documents.

Example:

```json
{
  "identifier": "worldbook",
  "label": "Worldbook Vocabulary",
  "version": "0.2.0",
  "bindingTypes": [
    {
      "identifier": "person",
      "label": "Person",
      "description": "A person entity.",
      "allowedPayloadShapes": [
        "shorthand"
      ],
      "attributes": []
    }
  ]
}
```

---

## Top-Level Vocabulary Fields

| Field | Purpose |
|---|---|
| `identifier` | Unique vocabulary identifier |
| `label` | Human-readable vocabulary name |
| `version` | Semantic version identifier |
| `bindingTypes` | Supported semantic binding definitions |

---

## Vocabulary Identity

Vocabulary identifiers should remain stable across versions.

Example:

```json
{
  "identifier": "worldbook",
  "version": "0.2.0"
}
```

This allows downstream systems to reason about:
- vocabulary evolution
- migration
- semantic compatibility
- historical interpretation

Vocabulary versions are considered part of semantic provenance.

---

## Binding Types

Binding types define semantic categories.

Example:

```json
{
  "identifier": "person",
  "label": "Person",
  "description": "A person entity.",
  "allowedPayloadShapes": [
    "shorthand"
  ],
  "attributes": []
}
```

Binding types define:
- semantic intent
- allowed payload structures
- valid attributes
- semantic interpretation boundaries

Binding types are application-specific.

BindingEngine does not impose a universal ontology.

---

## Payload Shapes

Binding types declare which payload shapes are valid.

Currently supported payload shapes include:
- `shorthand`
- `attribute_list`

Example:

```json
{
  "allowedPayloadShapes": [
    "attribute_list"
  ]
}
```

---

## Shorthand Payloads

Shorthand payloads represent single semantic identifiers.

Example binding:

```markdown
@person[jane-austen](Jane Austen)
```

The payload:

```text
jane-austen
```

Typically represents:
- entity identifiers
- references
- lightweight semantic links

---

## Attribute-List Payloads

Attribute-list payloads expose structured semantic data.

Example:

```markdown
@relationship[
    type: parent_of,
    subject: george-austen,
    object: jane-austen
](George Austen was Jane Austen’s father)
```

Vocabulary definition:

```json
{
  "identifier": "relationship",
  "allowedPayloadShapes": [
    "attribute_list"
  ]
}
```

---

## Attributes

Attributes define structured semantic fields within bindings.

Example:

```json
{
  "identifier": "subject",
  "label": "Subject",
  "description": "The subject entity.",
  "valueType": "identifier",
  "required": true,
  "repeatable": false,
  "role": "semantic"
}
```

Attributes define:
- semantic meaning
- value type
- structural constraints
- semantic role

---

## Attribute Fields

| Field | Purpose |
|---|---|
| `identifier` | Stable semantic attribute identifier |
| `label` | Human-readable attribute name |
| `description` | Semantic description |
| `valueType` | Expected semantic value type |
| `required` | Whether the attribute must exist |
| `repeatable` | Whether multiple values are allowed |
| `role` | Semantic role classification |

---

## Value Types

Value types constrain semantic attribute values.

Examples may include:
- `string`
- `identifier`
- `integer`
- `boolean`
- `date`

Example:

```json
{
  "identifier": "location",
  "valueType": "identifier"
}
```

Value types are vocabulary-level constraints rather than parser-level syntax rules.

---

## Attribute Roles

Attributes may have different semantic roles.

Current roles include:
- `semantic`
- `visibility`
- `metadata`
- `system`

Example:

```json
{
  "identifier": "revealed-at",
  "role": "visibility"
}
```

---

## Semantic Attributes

Semantic attributes contribute directly to semantic meaning.

Examples:
- `subject`
- `object`
- `type`
- `occurred-at`
- `location`

Semantic attributes may contribute to:
- graph structure
- projection identity
- inference
- conflict detection

---

## Visibility Attributes

Visibility attributes control presentation or access semantics.

Example:

```json
{
  "identifier": "revealed-at",
  "role": "visibility"
}
```

Example binding:

```markdown
@event[
    type: battle,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

In this example:
- `occurred-at` contributes to semantic chronology
- `revealed-at` controls user visibility

Visibility attributes may survive the pipeline without contributing to semantic graph identity.

---

## Metadata Attributes

Metadata attributes represent supporting editorial information.

Examples:
- author notes
- commentary
- editorial state
- publication metadata

Metadata attributes typically:
- preserve provenance
- survive serialization
- avoid semantic graph participation

---

## System Attributes

System attributes support application or infrastructure concerns.

Examples:
- indexing hints
- internal flags
- migration markers
- workflow metadata

System attributes are intentionally application-specific.

---

## Validation

Vocabulary validation identifies:
- unknown binding types
- invalid payload shapes
- missing required attributes
- invalid value types
- invalid semantic structures

Example:

```text
Unknown binding type: event
```

Validation is deterministic and vocabulary-specific.

---

## Application Neutrality

BindingEngine vocabularies are intentionally application-neutral.

Different applications may define:
- different ontologies
- different semantic structures
- different validation rules
- different semantic interpretations

Examples:
- worldbuilding systems
- historical archives
- collaborative fiction systems
- semantic publishing tools
- graph-oriented knowledge systems

---

## Vocabulary Evolution

Vocabularies are expected to evolve over time.

Changes may include:
- new binding types
- new attributes
- changed semantic interpretation
- deprecated structures
- expanded value types

Vocabulary versions therefore form part of semantic provenance.

Downstream systems should preserve:
- vocabulary identifiers
- vocabulary versions
- originating semantic context

---

## Provenance

Vocabulary context should survive throughout the semantic pipeline.

Downstream systems should always be able to determine:
- which vocabulary validated a binding
- which vocabulary version produced a structure
- which semantic rules were applied

Loss of vocabulary provenance is considered a serious architectural failure.

---

## Validation vs Truth

Vocabulary validation determines:
> whether a semantic structure is valid under a vocabulary

It does NOT determine:
> whether the claim is true.

Example:

```markdown
@relationship[
    type: ruler_of,
    subject: king-arthur,
    object: camelot
](Arthur ruled Camelot)
```

A vocabulary may consider this structurally valid even if:
- historically disputed
- fictional
- contradictory
- uncertain

Truth resolution belongs to downstream systems.

---

## Design Principles

BindingEngine vocabularies prioritise:
- explicit semantics
- deterministic validation
- extensibility
- provenance preservation
- application neutrality

Vocabularies intentionally avoid:
- hidden inference
- implicit canonicalisation
- universal ontologies
- application-specific truth models

---

## Future Expansion

Future vocabulary capabilities may include:
- richer value types
- vocabulary inheritance
- schema composition
- semantic constraints
- typed references
- validation plugins
- temporal semantics

However, vocabularies are intended to remain:
- deterministic
- provenance-aware
- application-neutral
- explicitly structured