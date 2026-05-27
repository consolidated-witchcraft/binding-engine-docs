# Overview

BindingEngine is a provenance-aware semantic processing system for extracting structured semantic meaning from authored markdown documents.

It is designed to allow semantic structure to coexist naturally with human-readable prose while preserving:
- provenance
- authored intent
- vocabulary context
- deterministic behaviour
- semantic traceability

The system is application-neutral and intended to support a wide range of semantic domains, including:
- worldbuilding
- campaign management
- knowledge systems
- historical archives
- semantic publishing
- collaborative fiction
- structured documentation
- graph-oriented information systems

---

## Core Philosophy

BindingEngine treats semantic markup as:

> authored semantic claims

rather than:

> canonical objective truth.

This distinction is foundational to the architecture.

A document may:
- contain incomplete information
- contain conflicting information
- represent unreliable narration
- contain historical uncertainty
- evolve over time

The responsibility of BindingEngine is therefore:
- extracting semantic structure
- preserving provenance
- maintaining deterministic transformations
- exposing semantic relationships explicitly

It is NOT responsible for:
- deciding canonical truth
- resolving semantic conflicts
- inferring hidden meaning automatically
- performing silent reconciliation

Those concerns belong to downstream application layers.

---

## Semantic Markup Within Prose

BindingEngine is designed to enrich prose rather than replace it.

Semantic bindings are intended to integrate naturally into authored text.

Example:

```markdown
@person[jane-austen](Jane Austen) was an English writer known primarily for her six novels.

Jane Austen was born on 16 December 1775 in @place[steventon-hampshire](Steventon, Hampshire). Her @relationship[type: parent_of, subject: george-austen, object: jane-austen](father, George Austen), wrote of her arrival in a letter that her mother, @relationship[type: parent_of, subject: cassandra-austen, object: jane-austen](Cassandra), "certainly expected to have been brought to bed a month ago."
```

This allows documents to remain:
- readable
- expressive
- author-friendly

while still exposing machine-readable semantic structure.

---

## The Semantic Pipeline

BindingEngine processes documents through a layered semantic pipeline.

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

Each layer has a narrowly scoped responsibility.

---

## Architectural Layers

### Parser

The parser transforms authored markdown into structured AST representations.

The parser answers:

> “What syntactically exists in this document?”

The parser is intentionally syntax-focused and does not perform semantic reasoning.

---

### Vocabulary Validation

The vocabulary layer validates semantic meaning against a defined vocabulary.

This layer answers:

> “Is this binding semantically valid under this vocabulary?”

Vocabularies define:
- binding types
- payload shapes
- attribute definitions
- value types
- attribute roles

---

### Assertions

The assertions layer extracts provenance-aware semantic claims from validated documents.

This layer answers:

> “What claims does this document make?”

Assertions preserve:
- source spans
- source identifiers
- revision identifiers
- vocabulary versions
- authored semantic structure

Assertions represent claims rather than truth.

---

### Projection

The projection layer transforms assertions into deterministic semantic structures suitable for graph-oriented processing systems.

This layer answers:

> “What semantic structures do these claims describe?”

Projection:
- preserves provenance
- preserves deterministic identity
- avoids hidden inference
- remains storage-neutral

Projection does not:
- resolve conflicts
- infer canonical truth
- merge entities automatically

---

### Inference

Inference derives additional semantic structures from explicit authored claims.

Inference may:
- derive implied entities
- derive implied relationships
- construct higher-order semantic structures

Inference must preserve provenance and derivation traceability.

Inference does not decide canonical truth.

---

### Conflict Detection

Conflict detection identifies incompatible or competing semantic claims.

Examples include:
- contradictory dates
- conflicting relationships
- incompatible classifications
- overlapping semantic identities

Conflict detection exposes disagreements explicitly rather than silently resolving them.

---

### Reification

Reification transforms semantic structures into application-specific canonical models.

Reification is intentionally domain-specific.

Different applications may use different strategies, including:
- canonical-source resolution
- manual conflict resolution
- editorial review workflows
- probabilistic trust systems

BindingEngine intentionally avoids imposing a universal truth model.

---

# Provenance

Provenance preservation is a foundational architectural principle.

Every semantic structure should remain traceable back to:
- the source document
- the originating revision
- the authored binding
- the vocabulary version
- the original source span

Downstream systems should always be able to answer:

> “Where did this semantic claim originate?”

Loss of provenance is considered a serious architectural failure.

---

# Semantic vs Visibility Metadata

BindingEngine distinguishes between:
- semantic attributes
- metadata attributes
- visibility attributes
- system attributes

For example:

```markdown
@event[
    type: battle,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

In this example:
- `occurred-at` contributes to semantic chronology
- `revealed-at` controls presentation visibility

Visibility metadata is preserved throughout the pipeline without becoming part of semantic identity.

This distinction enables:
- spoiler management
- campaign reveal systems
- publication scheduling
- access control workflows

without contaminating semantic graph structure.

---

# Design Principles

BindingEngine prioritises:

- provenance preservation
- deterministic behaviour
- explicit semantics
- immutable structures
- application neutrality
- strict typing
- layered architecture

BindingEngine intentionally avoids:

- hidden inference
- implicit canonicalisation
- runtime mutation
- storage-specific assumptions
- application-specific coupling

---

# Current Status

BindingEngine is currently in early development.

The architecture is stabilising, but APIs should still be considered experimental until `1.0.0`.

Further documents describe individual architectural layers in greater detail.