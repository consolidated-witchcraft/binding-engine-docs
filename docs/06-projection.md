# Projection

The projection layer transforms semantic assertions into deterministic semantic structures suitable for graph-oriented processing systems.

Projection answers:

> “What semantic structures do these claims describe?”

Projection exists to bridge the gap between:
- authored semantic claims
- structured semantic processing systems

including:
- graph construction
- indexing
- traversal
- inference
- semantic querying
- application-level processing

Projection is intentionally:
- deterministic
- provenance-aware
- storage-neutral
- minimally interpretive

---

## Pipeline Position

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
```

Projection operates only on:
- validated assertions
- deterministic semantic structures

Projection assumes:
- parser validation has succeeded
- vocabulary validation has succeeded
- assertion extraction has succeeded

---

## Core Philosophy

Assertions represent:

> authored semantic claims

Projection represents:

> semantic structures derived from those claims

This distinction is important.

Projection intentionally avoids:
- deciding canonical truth
- resolving conflicts
- hidden inference
- semantic reconciliation
- entity merging

Projection should remain:
- deterministic
- provenance-preserving
- explicit
- application-neutral

---

## Example

Example assertion:

```text
Assertion
├── bindingType: relationship
├── attributes:
│   ├── type = parent_of
│   ├── subject = george-austen
│   └── object = jane-austen
└── provenance: (...)
```

Example projection:

```text
RelationshipProjection
├── projectionKey:
│   relationship:parent_of:george-austen:jane-austen
├── relationshipType: parent_of
├── subject: george-austen
├── object: jane-austen
└── originatingAssertion: (...)
```

Projection exposes semantic structure in a graph-oriented form while preserving provenance.

---

## Deterministic Projection

Projection is intentionally deterministic.

Given identical:
- assertions
- vocabularies
- projection rules
- library versions

the same projections should always be produced.

Determinism is important for:
- synchronization
- indexing
- caching
- reproducibility
- debugging
- semantic traceability

---

## Projection Goals

Projection is intended to:
- expose semantic structure explicitly
- support graph-oriented systems
- preserve provenance
- generate deterministic semantic identity
- remain storage-neutral

Projection is NOT intended to:
- decide truth
- merge entities automatically
- canonicalise semantic structures
- silently infer missing meaning

---

## Projection Types

Projection types are application-neutral semantic structures.

Current conceptual projection types include:
- entity projections
- relationship projections
- event projections
- attribute projections
- reference projections

Different applications may define additional projection strategies.

---

## Entity Projection

Entity projections typically derive from shorthand bindings.

Example binding:

```markdown
@person[jane-austen](Jane Austen)
```

Example assertion:

```text
Assertion
├── bindingType: person
├── shorthandValue: jane-austen
└── label: Jane Austen
```

Example projection:

```text
EntityProjection
├── projectionKey:
│   entity:person:jane-austen
├── entityType: person
├── identifier: jane-austen
├── label: Jane Austen
└── originatingAssertion: (...)
```

---

## Relationship Projection

Relationship projections derive from structured relationship assertions.

Example binding:

```markdown
@relationship[
    type: parent_of,
    subject: george-austen,
    object: jane-austen
](George Austen was Jane Austen’s father)
```

Example projection:

```text
RelationshipProjection
├── projectionKey:
│   relationship:parent_of:george-austen:jane-austen
├── relationshipType: parent_of
├── subject: george-austen
├── object: jane-austen
└── label:
│   George Austen was Jane Austen’s father
```

Relationship projections expose graph-oriented semantic edges.

---

## Event Projection

Event projections derive from structured event assertions.

Example binding:

```markdown
@event[
    type: birth,
    subject: jane-austen,
    occurred-at: gregorian:1775-12-16,
    location: steventon-hampshire
](Birth of Jane Austen)
```

Example projection:

```text
EventProjection
├── projectionKey:
│   event:birth:jane-austen:gregorian:1775-12-16
├── eventType: birth
├── subject: jane-austen
├── occurredAt:
│   gregorian:1775-12-16
├── location:
│   steventon-hampshire
└── originatingAssertion: (...)
```

Projection identity should remain deterministic and explicit.

---

## Projection Keys

Projection keys provide deterministic semantic identity.

Examples:

```text
entity:person:jane-austen
```

```text
relationship:parent_of:george-austen:jane-austen
```

Projection keys are intended to support:
- indexing
- graph traversal
- deduplication
- synchronization
- semantic identity

Projection keys should remain:
- deterministic
- explicit
- reproducible

---

## Projection Provenance

Projection preserves provenance from the assertion layer.

This includes:
- originating assertions
- source documents
- revision identifiers
- vocabulary identifiers
- vocabulary versions
- source spans

Downstream systems should always be able to answer:

> “Which authored claim produced this semantic structure?”

Loss of provenance is considered a serious architectural failure.

---

## Originating Assertions

Every projection should preserve its originating assertion.

Example conceptual structure:

```text
Projection
├── originatingAssertion:
│   Assertion(...)
```

This enables:
- traceability
- debugging
- editor tooling
- conflict analysis
- provenance reconstruction

---

## Projection Sets

Projections are typically returned as immutable projection collections.

Example conceptual structure:

```text
ProjectionSet
├── Projection
├── Projection
└── Projection
```

Projection sets preserve:
- deterministic ordering
- projection identity
- provenance integrity

---

## Composite Projection Pipelines

Projection extractors may be composed into deterministic extraction pipelines.

Example conceptual pipeline:

```text
CompositeProjectionExtractor
├── EntityProjectionExtractor
├── RelationshipProjectionExtractor
└── EventProjectionExtractor
```

This allows:
- modular projection logic
- application-specific composition
- deterministic orchestration

without introducing hidden behaviour.

---

## Semantic vs Visibility Attributes

Projection distinguishes between:
- semantic attributes
- visibility attributes
- metadata attributes
- system attributes

Example binding:

```markdown
@event[
    type: battle,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

In this example:
- `occurred-at` contributes to semantic identity
- `revealed-at` controls visibility semantics

Projection should avoid incorporating visibility metadata into semantic graph identity.

This distinction is important for:
- spoiler systems
- publication workflows
- campaign reveal systems
- access control layers

without contaminating semantic graph structure.

---

## Projection vs Inference

Projection exposes:
- explicit semantic structure

Inference derives:
- implied semantic structure

Projection intentionally avoids:
- implied entity generation
- hidden relationship construction
- semantic expansion
- graph completion

Example:

```text
relationship:
subject = george-austen
object = jane-austen
```

may imply:

```text
entity: george-austen
```

However, this implication belongs to inference systems rather than projection.

---

## Projection vs Conflict Resolution

Projection preserves semantic structures even when they conflict.

Example conflicting assertions:

```text
occurred-at = 1844
```

and:

```text
occurred-at = 1845
```

may both produce projections.

Projection intentionally avoids:
- deciding which is correct
- silently discarding information
- canonicalising semantic structures

Conflict resolution belongs to downstream systems.

---

## Projection vs Reification

Projection exposes graph-oriented semantic structures.

Reification produces:
- application-specific canonical models

Different applications may:
- trust different sources
- prioritise different assertions
- resolve conflicts differently

Projection intentionally avoids imposing:
- universal truth
- global canonicalisation
- application-specific semantics

---

## Storage Neutrality

Projection is intentionally storage-neutral.

Projection output may be consumed by:
- relational databases
- graph databases
- search indexes
- in-memory graphs
- semantic APIs
- custom application layers

Projection should not assume:
- a specific graph engine
- a specific persistence model
- a specific application architecture

---

## Serialization

Projection structures are designed to support deterministic serialization.

Serialization enables:
- JSON APIs
- indexing systems
- snapshots
- transport layers
- queues
- semantic export workflows

Projection serialization should preserve:
- projection identity
- provenance
- semantic structure
- deterministic ordering

---

## Design Principles

Projection prioritises:
- deterministic behaviour
- provenance preservation
- explicit semantic identity
- immutable structures
- application neutrality

Projection intentionally avoids:
- hidden inference
- implicit canonicalisation
- storage-specific assumptions
- semantic reconciliation

---

## Future Expansion

Future projection capabilities may include:
- richer event projections
- typed semantic edges
- temporal projections
- semantic indexing structures
- provenance graphs
- projection lineage tracking
- projection caching systems

However, projection is intended to remain:
- deterministic
- provenance-aware
- storage-neutral
- minimally interpretive