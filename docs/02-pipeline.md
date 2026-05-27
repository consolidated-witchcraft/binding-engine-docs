# Semantic Pipeline

BindingEngine processes authored markdown through a layered semantic pipeline.

Each layer has:
- a narrowly scoped responsibility
- explicit inputs and outputs
- deterministic behaviour
- preserved provenance

The pipeline is intentionally compositional.

```text
Markdown
↓
Parser
↓
Vocabulary Validation
↓
Assertions
↓
Projection
↓
Serialization
↓
Inference / Conflict Detection / Reification
```

---

## Design Goals

The semantic pipeline is designed to prioritise:

- provenance preservation
- deterministic transformation
- explicit semantics
- application neutrality
- layered responsibility separation

The pipeline intentionally avoids:
- hidden inference
- implicit canonicalisation
- silent mutation
- storage-specific assumptions
- application-specific truth models

---

## Layer 1 — Markdown

The pipeline begins with authored markdown documents.

Example:

```markdown
@person[jane-austen](Jane Austen) was an English writer.

@event[
    type: birth,
    subject: jane-austen,
    occurred-at: gregorian:1775-12-16,
    location: steventon-hampshire
](Birth of Jane Austen)
```

Semantic bindings are intended to coexist naturally with prose.

Documents should remain:
- readable by humans
- expressive
- author-friendly

while exposing machine-readable semantic structure.

---

## Layer 2 — Parser

The parser transforms markdown into structured AST representations.

The parser answers:

> “What syntactically exists in this document?”

The parser is responsible for:
- binding recognition
- payload parsing
- source span tracking
- AST construction
- syntax diagnostics

The parser is NOT responsible for:
- semantic meaning
- validation against vocabularies
- inference
- canonicalisation

Example conceptual output:

```text
DocumentNode
├── ParagraphNode
│   ├── TextNode
│   └── BindingNode
│       ├── bindingType: person
│       ├── payloadShape: shorthand
│       ├── shorthandValue: jane-austen
│       ├── label: Jane Austen
│       └── sourceSpan: [0, 36)
```

The parser preserves exact source locations for provenance tracking.

---

## Layer 3 — Vocabulary Validation

The vocabulary layer validates semantic meaning against a defined vocabulary.

The vocabulary layer answers:

> “Is this binding semantically valid under this vocabulary?”

Vocabularies define:
- binding types
- payload shapes
- attribute definitions
- value types
- attribute roles
- required attributes
- semantic constraints

Example:

```json
{
  "identifier": "relationship",
  "allowedPayloadShapes": ["attribute_list"],
  "attributes": [
    {
      "identifier": "subject",
      "valueType": "identifier",
      "required": true,
      "role": "semantic"
    }
  ]
}
```

Validation produces diagnostics for:
- unknown binding types
- missing required attributes
- invalid payload shapes
- invalid value types
- malformed semantic structures

Validation is deterministic and vocabulary-specific.

---

## Layer 4 — Assertions

The assertions layer extracts provenance-aware semantic claims from validated documents.

The assertions layer answers:

> “What claims does this document make?”

Assertions preserve:
- source spans
- source identifiers
- revision identifiers
- vocabulary identifiers
- vocabulary versions
- authored semantic structure

Example conceptual assertion:

```text
Assertion
├── bindingType: relationship
├── attributes:
│   ├── type = parent_of
│   ├── subject = george-austen
│   └── object = jane-austen
├── sourceDocumentId: biography.md
├── sourceRevisionId: rev-123
├── vocabulary: worldbook@0.2.0
└── sourceSpan: [140, 262)
```

Assertions represent:
> authored semantic claims

not:
> canonical truth

Multiple conflicting assertions may coexist.

---

## Layer 5 — Projection

The projection layer transforms assertions into deterministic semantic structures.

The projection layer answers:

> “What semantic structures do these claims describe?”

Projection is intended to support:
- graph construction
- indexing
- traversal
- semantic processing
- downstream inference systems

Projection preserves:
- provenance
- semantic identity
- deterministic ordering
- originating assertions

Example conceptual projection:

```text
RelationshipProjection
├── projectionKey:
│   relationship:parent_of:george-austen:jane-austen
├── relationshipType: parent_of
├── subject: george-austen
├── object: jane-austen
└── originatingAssertion: (...)
```

Projection does NOT:
- infer hidden meaning
- resolve conflicts
- canonicalise entities
- merge competing structures

Projection remains deterministic and storage-neutral.

---

## Layer 6 — Serialization

Serialization transforms projections into transport-safe structures.

Serialization enables:
- JSON APIs
- persistence
- queues
- indexing systems
- snapshots
- integration pipelines

Example conceptual output:

```json
[
  {
    "projectionType": "entity",
    "projectionKey": "entity:person:jane-austen",
    "entityType": "person",
    "identifier": "jane-austen"
  }
]
```

Serialization preserves:
- semantic identity
- provenance
- projection structure
- deterministic ordering

---

## Layer 7 — Inference

Inference derives additional semantic structures from explicit authored claims.

Examples:
- deriving implied entities
- deriving implied relationships
- constructing higher-order semantic structures

Inference must:
- preserve provenance
- preserve derivation traceability
- remain deterministic where possible

Inference does NOT:
- silently decide canonical truth
- erase conflicting information

Derived structures should remain distinguishable from authored structures.

---

## Layer 8 — Conflict Detection

Conflict detection identifies incompatible semantic claims.

Examples:
- contradictory dates
- conflicting parentage
- incompatible classifications
- competing identities

Conflict detection exposes disagreement explicitly.

It does NOT silently reconcile conflicts.

Example conceptual conflict:

```text
Conflict
├── subjectKey: event:battle-of-thornbridge
├── field: occurred-at
├── candidates:
│   ├── 1844 from assertion A
│   └── 1845 from assertion B
└── resolutionRequired: true
```

---

## Layer 9 — Reification

Reification transforms semantic structures into application-specific canonical models.

Reification is intentionally domain-specific.

Different applications may use:
- canonical-source resolution
- editorial review workflows
- manual conflict resolution
- trust-weighted systems
- publication workflows

BindingEngine intentionally avoids imposing:
- universal truth models
- global canonicalisation rules
- application-specific semantics

---

## Provenance Through The Pipeline

A core architectural principle of BindingEngine is:

> provenance must survive every transformation layer.

Downstream systems should always be able to answer:

> “Where did this semantic structure originate?”

This includes:
- source document identifiers
- revision identifiers
- vocabulary versions
- source spans
- originating assertions
- derivation chains

Loss of provenance is considered a serious architectural failure.

---

## Determinism

Each layer of the pipeline is intended to be deterministic.

Given identical:
- source documents
- vocabularies
- library versions

the same semantic structures should always be produced.

This property is important for:
- reproducibility
- caching
- indexing
- synchronization
- debugging
- provenance traceability

---

## Visibility Metadata

BindingEngine distinguishes between:
- semantic meaning
- visibility metadata
- editorial metadata
- system metadata

Example:

```markdown
@event[
    type: battle,
    occurred-at: 139578122,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

In this example:
- `occurred-at` contributes to semantic chronology
- `revealed-at` controls user visibility

Visibility metadata may survive the pipeline without contributing to semantic identity or graph structure.

This enables:
- spoiler systems
- publication scheduling
- campaign reveal workflows
- access control layers

without contaminating semantic meaning.

---

## Pipeline Boundaries

Each layer should remain narrowly scoped.

Avoid:
- parser-level inference
- projection-level canonicalisation
- validation-level graph construction
- serialization-level mutation

Maintaining clear architectural boundaries is critical to preserving:
- determinism
- provenance
- maintainability
- application neutrality