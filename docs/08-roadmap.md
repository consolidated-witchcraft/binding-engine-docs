# Roadmap

This document describes the planned architectural direction of the BindingEngine ecosystem.

The roadmap is intentionally:
- architectural
- conceptual
- direction-focused

rather than:
- deadline-driven
- release-date-driven
- feature-checklist-oriented

BindingEngine is intended to evolve carefully with strong emphasis on:
- provenance preservation
- deterministic behaviour
- semantic clarity
- explicit architecture
- long-term maintainability

---

## Architectural Priorities

The long-term direction of BindingEngine prioritises:

- deterministic semantic processing
- provenance-aware transformation
- layered architecture
- explicit semantic modelling
- application neutrality
- graph-oriented interoperability

The ecosystem intentionally avoids:
- hidden inference
- magical behaviour
- implicit canonicalisation
- tightly coupled application logic
- storage-specific assumptions

---

## Current Ecosystem

The ecosystem currently includes:

| Package | Responsibility |
|---|---|
| `binding-engine-parser` | Parses semantic binding syntax into AST structures |
| `binding-engine-vocabulary` | Defines semantic vocabularies |
| `binding-engine-vocabulary-loader` | Loads vocabularies from JSON |
| `binding-engine-assertions` | Extracts provenance-aware semantic assertions |
| `binding-engine-projection` | Produces deterministic semantic projections |
| `binding-engine-demo` | Demonstrates the end-to-end semantic pipeline |

Current capabilities include:
- deterministic parsing
- vocabulary validation
- provenance-aware assertions
- deterministic projection
- projection serialization
- semantic attribute roles
- visibility metadata handling

---

## Near-Term Goals

### Projection Expansion

Current projection support is intentionally minimal.

Planned expansion includes:
- event projections
- attribute projections
- reference projections
- richer semantic edge modelling
- temporal projection support

Projection expansion should remain:
- deterministic
- provenance-aware
- storage-neutral

---

### Conflict Detection

Planned package:

```text
binding-engine-conflicts
```

Purpose:
- detect incompatible semantic claims
- expose conflicting semantic structures
- preserve competing provenance

Examples:
- contradictory chronology
- conflicting relationships
- incompatible classifications
- overlapping semantic identities

Conflict detection should:
- expose disagreement explicitly
- avoid hidden reconciliation
- preserve provenance chains

Conflict detection should NOT:
- silently choose winners
- canonicalise truth
- discard conflicting claims

---

### Inference Systems

Planned package:

```text
binding-engine-inference
```

Purpose:
- derive implied semantic structures
- construct higher-order semantic relationships
- support semantic expansion workflows

Examples:
- implied entities
- inferred relationships
- semantic hierarchy construction
- derived temporal relationships

Inference must:
- preserve derivation provenance
- distinguish inferred structures from authored structures
- remain deterministic where possible

Inference should NOT:
- silently canonicalise truth
- erase authored ambiguity

---

## Reification Systems

Planned package:

```text
binding-engine-reification
```

Purpose:
- transform semantic structures into application-specific canonical models

Reification is intentionally domain-specific.

Different applications may implement:
- canonical-source resolution
- editorial review workflows
- manual conflict resolution
- trust-weighted systems
- publication workflows

BindingEngine intentionally avoids imposing:
- universal truth models
- global canonicalisation rules

---

## Planned Conflict Resolution Strategies

### Canonical Source Resolution

One semantic structure may be treated as authoritative.

Example:

```text
event:battle-of-thornbridge
```

may be designated as:
- canonical
- editorially trusted
- authoritative

Other structures may then:
- enrich
- backlink
- conflict with
- derive from

the canonical structure.

---

### Manual Conflict Resolution

Applications may instead expose conflicts directly to users.

Example:

```text
occurred-at = 1844
```

vs:

```text
occurred-at = 1845
```

The system may:
- preserve both claims
- expose the disagreement
- require manual editorial selection

BindingEngine intentionally supports multiple resolution strategies.

---

## Visibility Systems

Planned capabilities include:
- reveal workflows
- spoiler systems
- publication scheduling
- audience segmentation
- role-based visibility
- provenance-aware access filtering

Example:

```markdown
@event[
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

The semantic structure may exist immediately while remaining hidden from certain users.

Visibility semantics should remain separated from semantic identity.

---

## Temporal Systems

Future temporal support may include:
- multiple calendar systems
- relative chronology
- semantic timelines
- uncertain chronology
- temporal conflict detection
- chronology-aware projection

The architecture intentionally avoids assuming:
- Gregorian calendars
- real-world chronology
- universal timestamp systems

---

## Vocabulary Expansion

Planned vocabulary capabilities may include:
- richer value types
- vocabulary composition
- vocabulary inheritance
- typed references
- semantic constraints
- validation plugins
- vocabulary migration tooling

Vocabulary evolution should remain:
- explicit
- versioned
- provenance-aware

---

## Provenance Expansion

Future provenance systems may include:
- provenance graphs
- derivation lineage
- semantic ancestry tracking
- assertion signatures
- trust metadata
- transformation audit chains

Provenance preservation will remain a foundational architectural principle.

---

## Serialization Expansion

Future serialization support may include:
- JSON-LD
- graph export formats
- RDF interoperability
- semantic snapshots
- streaming serialization
- semantic diff formats

Serialization should remain:
- deterministic
- provenance-preserving
- transport-safe

---

## Tooling and Editor Support

Planned tooling may include:
- language server support
- editor diagnostics
- syntax highlighting
- semantic autocomplete
- provenance-aware editing tools
- semantic visualisation systems

Tooling should preserve:
- deterministic semantics
- source traceability
- authored structure

---

## Graph and Query Systems

Future systems may include:
- semantic traversal APIs
- graph query interfaces
- semantic indexing systems
- provenance-aware querying
- temporal graph querying
- semantic search systems

BindingEngine itself intends to remain:
- graph-oriented
- storage-neutral

rather than tightly coupled to:
- specific graph databases
- query engines
- persistence layers

---

## Ecosystem Philosophy

BindingEngine is intended to become:
- infrastructure-grade
- provenance-safe
- deterministic
- semantically explicit
- application-neutral

The ecosystem prioritises:
- correctness
- traceability
- maintainability
- semantic clarity

over:
- hidden abstraction
- magical behaviour
- convenience-driven shortcuts
- premature optimisation

---

## Stability Goals

Before `1.0.0`, the focus is:
- architectural stabilisation
- semantic clarity
- provenance guarantees
- deterministic behaviour
- package boundary refinement

The ecosystem should reach `1.0.0` only once:
- package responsibilities are stable
- semantic boundaries are clear
- provenance guarantees are reliable
- deterministic behaviour is well established

---

## Long-Term Vision

The long-term vision of BindingEngine is:

> a deterministic, provenance-aware semantic infrastructure ecosystem for authored semantic knowledge systems.

The ecosystem is intended to support:
- worldbuilding systems
- collaborative fiction
- semantic archives
- campaign management
- graph-oriented publishing
- historical modelling
- semantic knowledge systems

while remaining:
- application-neutral
- provenance-preserving
- semantically explicit
- human-author-friendly