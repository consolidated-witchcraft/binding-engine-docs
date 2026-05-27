# Assertions

The assertions layer transforms validated semantic bindings into provenance-aware semantic claims.

Assertions represent:

> “This document claims X.”

Assertions do NOT represent:

> “X is objectively true.”

This distinction is foundational to BindingEngine’s architecture.

Assertions preserve:
- authored semantic structure
- provenance
- vocabulary context
- source traceability
- deterministic extraction behaviour

---

## Purpose

The parser answers:

> “What syntactically exists in this document?”

The vocabulary layer answers:

> “Is this binding semantically valid under this vocabulary?”

The assertions layer answers:

> “What claims does this document make?”

Assertions form the bridge between:
- validated semantic syntax
- higher-order semantic processing systems

including:
- projection
- inference
- graph construction
- conflict detection
- reification

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
```

Assertions operate only on:
- syntactically valid documents
- vocabulary-valid semantic structures

The assertions layer assumes upstream validation has already succeeded.

---

## Core Philosophy

Assertions preserve explicit authored meaning.

The assertions layer intentionally avoids:
- hidden inference
- graph construction
- canonicalisation
- conflict resolution
- semantic reconciliation

Assertions should remain:
- deterministic
- provenance-aware
- minimally interpretive

---

## Example

Example authored markdown:

```markdown
@relationship[
    type: parent_of,
    subject: george-austen,
    object: jane-austen
](George Austen was Jane Austen’s father)
```

Example conceptual assertion:

```text
Assertion
├── bindingType: relationship
├── payloadShape: attribute_list
├── attributes:
│   ├── type = parent_of
│   ├── subject = george-austen
│   └── object = jane-austen
├── label:
│   George Austen was Jane Austen’s father
├── sourceDocumentId: biography.md
├── sourceRevisionId: rev-123
├── vocabulary: worldbook@0.2.0
└── sourceSpan: [142, 261)
```

---

## Assertions As Claims

Assertions represent semantic claims authored within documents.

Example:

```markdown
@relationship[
    type: ruler_of,
    subject: king-arthur,
    object: camelot
](Arthur ruled Camelot)
```

The assertion means:

> “This document claims Arthur ruled Camelot.”

It does NOT mean:

> “Arthur objectively ruled Camelot.”

Multiple conflicting assertions may coexist.

Conflict resolution belongs to downstream systems.

---

## Deterministic Extraction

Assertion extraction is intentionally deterministic.

Given identical:
- documents
- vocabularies
- parser output
- library versions

the same assertions should always be produced.

Determinism is important for:
- provenance traceability
- caching
- indexing
- synchronization
- reproducibility
- debugging

---

## Assertion Structure

Assertions typically preserve:
- binding type
- payload shape
- semantic attributes
- shorthand values
- authored labels
- source provenance
- vocabulary context
- source spans

---

## Binding Types

Assertions preserve the originating binding type.

Example:

```markdown
@person[jane-austen](Jane Austen)
```

Produces:

```text
bindingType: person
```

Binding types remain vocabulary-defined.

The assertions layer does not impose semantic ontologies.

---

## Payload Shapes

Assertions preserve payload structure.

Examples:
- shorthand payloads
- attribute-list payloads

Example:

```text
payloadShape: shorthand
```

or:

```text
payloadShape: attribute_list
```

Payload structure preservation is important for:
- deterministic projection
- semantic interpretation
- downstream tooling

---

## Shorthand Assertions

Example:

```markdown
@person[jane-austen](Jane Austen)
```

Produces a shorthand semantic assertion containing:
- shorthand identifier
- authored label
- provenance information

Conceptual structure:

```text
Assertion
├── bindingType: person
├── payloadShape: shorthand
├── shorthandValue: jane-austen
└── label: Jane Austen
```

---

## Attribute Assertions

Example:

```markdown
@event[
    type: birth,
    subject: jane-austen,
    occurred-at: gregorian:1775-12-16
](Birth of Jane Austen)
```

Produces an attribute-list semantic assertion:

```text
Assertion
├── bindingType: event
├── attributes:
│   ├── type = birth
│   ├── subject = jane-austen
│   └── occurred-at = gregorian:1775-12-16
```

The assertions layer preserves explicit authored structure without interpretation.

---

## Provenance

Provenance preservation is a foundational architectural principle.

Assertions preserve:
- source document identifiers
- revision identifiers
- vocabulary identifiers
- vocabulary versions
- source spans
- authored labels

Downstream systems should always be able to answer:

> “Where did this semantic claim originate?”

Loss of provenance is considered a serious architectural failure.

---

## Source Context

Assertions carry source context describing:
- the source system
- document identity
- revision identity
- vocabulary identity
- vocabulary version

Example conceptual structure:

```text
SourceContext
├── sourceId: worldbook
├── documentId: biography.md
├── revisionId: rev-123
├── vocabularyIdentifier: worldbook
└── vocabularyVersion: 0.2.0
```

---

## Source Spans

Assertions preserve exact source spans from the parser layer.

Example:

```text
sourceSpan: [142, 261)
```

Source spans allow downstream systems to:
- trace semantic claims
- generate diagnostics
- support editor tooling
- preserve provenance
- perform source-aware workflows

---

## Vocabulary Context

Assertions preserve vocabulary identity and version context.

This is important because:
- vocabularies evolve
- semantic interpretation may change
- attributes may gain new meaning
- validation rules may differ between versions

Vocabulary provenance should survive the entire semantic pipeline.

---

## Semantic vs Visibility Attributes

Assertions preserve all validated attributes, including:
- semantic attributes
- visibility attributes
- metadata attributes
- system attributes

Example:

```markdown
@event[
    type: battle,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

In this example:
- `occurred-at` contributes to semantic chronology
- `revealed-at` controls visibility semantics

The assertions layer preserves both.

Interpretation belongs to downstream systems.

---

## Visibility Metadata

Visibility metadata is intentionally preserved within assertions.

This enables downstream systems to implement:
- spoiler systems
- publication scheduling
- campaign reveal workflows
- access control layers

without contaminating semantic identity.

The assertions layer preserves metadata without deciding how it should be interpreted.

---

## Assertion Sets

Assertions are typically returned as immutable assertion collections.

Example conceptual structure:

```text
AssertionSet
├── Assertion
├── Assertion
└── Assertion
```

Assertion sets preserve:
- extraction ordering
- deterministic iteration
- provenance integrity

---

## Extraction Responsibility

The assertions layer is responsible for:
- deterministic semantic extraction
- provenance preservation
- structural claim representation

It is NOT responsible for:
- graph construction
- inference
- canonicalisation
- semantic conflict resolution
- entity merging
- truth determination

---

## Assertions vs Projection

Assertions describe:
> authored semantic claims

Projection describes:
> graph-oriented semantic structures derived from those claims

This distinction is important.

Assertions preserve authored semantic structure as faithfully as possible.

Projection may later:
- derive semantic identities
- construct graph structures
- generate deterministic projection keys

---

## Assertions vs Inference

Assertions preserve:
- explicit authored semantics

Inference derives:
- implicit semantic structures

The assertions layer intentionally avoids:
- implied entity generation
- hidden relationship creation
- semantic expansion
- automatic graph completion

Those behaviours belong to inference systems.

---

## Assertions vs Reification

Assertions preserve claims.

Reification produces:
- application-specific canonical models

Different applications may:
- trust different sources
- use different resolution strategies
- reconcile conflicts differently

The assertions layer intentionally avoids imposing:
- universal truth
- canonical resolution
- semantic prioritisation

---

## Design Principles

The assertions layer prioritises:
- provenance preservation
- deterministic extraction
- explicit semantics
- immutable structures
- vocabulary traceability

The assertions layer intentionally avoids:
- hidden inference
- implicit reconciliation
- graph mutation
- application-specific semantics

---

## Future Expansion

Future assertion capabilities may include:
- richer provenance chains
- derived assertion tracking
- semantic confidence metadata
- typed assertion hierarchies
- temporal provenance
- assertion signatures
- semantic lineage tracking

However, assertions are intended to remain:
- deterministic
- provenance-aware
- minimally interpretive
- application-neutral