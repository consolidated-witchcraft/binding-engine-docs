# BindingEngine Documentation

Official documentation for the Consolidated Witchcraft BindingEngine ecosystem.

BindingEngine is a provenance-aware semantic processing system for extracting structured semantic meaning from authored markdown documents.

It is designed to preserve:

- authored structure
- semantic intent
- source provenance
- vocabulary context
- deterministic transformation behaviour

throughout the entire processing pipeline.

---

# Core Concept

BindingEngine treats semantic markup as:

> authored semantic claims

rather than:

> canonical objective truth.

This distinction is foundational to the architecture.

A document may:

- contain incomplete information
- contain conflicting information
- represent biased perspectives
- represent historical uncertainty
- evolve over time

BindingEngine therefore prioritises:

- provenance preservation
- deterministic extraction
- explicit semantics
- downstream conflict resolution

over:

- hidden inference
- magical interpretation
- implicit canonicalisation

---

# Semantic Pipeline

BindingEngine processes documents through a layered semantic pipeline:

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

# Example

```markdown
@person[jane-austen](Jane Austen) was an English writer.

@event[
    type: birth,
    subject: jane-austen,
    occurred-at: gregorian:1775-12-16,
    location: steventon-hampshire
](Birth of Jane Austen)
```

This may ultimately produce deterministic semantic projections such as:

```json
[
  {
    "projectionType": "entity",
    "projectionKey": "entity:person:jane-austen",
    "entityType": "person",
    "identifier": "jane-austen",
    "label": "Jane Austen"
  }
]
```

while preserving:

- source spans
- vocabulary versions
- authored labels
- originating assertions
- provenance metadata

---

# Ecosystem Packages


| Package                                                  | Responsibility                                |
| -------------------------------------------------------- | --------------------------------------------- |
| consolidated-witchcraft/binding-engine-parser            | Parses binding syntax into AST structures     |
| consolidated-witchcraft/binding-engine-vocabulary        | Defines semantic vocabulary rules             |
| consolidated-witchcraft/binding-engine-vocabulary-loader | Loads vocabularies from JSON definitions      |
| consolidated-witchcraft/binding-engine-assertions        | Extracts provenance-aware semantic assertions |
| consolidated-witchcraft/binding-engine-projection        | Projects assertions into semantic structures  |
| consolidated-witchcraft/binding-engine-demo              | Demonstrates the end-to-end semantic pipeline |

---

# Documentation Structure


| Document                             | Purpose                                        |
| ------------------------------------ | ---------------------------------------------- |
| `docs/01-overview.md`                | High-level architectural overview              |
| `docs/02-pipeline.md`                | End-to-end semantic pipeline                   |
| `docs/03-binding-syntax.md`          | Binding syntax and payload shapes              |
| `docs/04-vocabularies.md`            | Vocabulary structure and attribute definitions |
| `docs/05-assertions.md`              | Provenance-aware semantic assertions           |
| `docs/06-projection.md`              | Deterministic semantic projection              |
| `docs/07-visibility-and-metadata.md` | Semantic vs visibility/system metadata         |
| `docs/08-roadmap.md`                 | Planned architectural direction                |

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
- implicit canonical truth
- runtime mutation
- storage-specific assumptions
- application-specific coupling

---

# Current Status

BindingEngine is currently in early development.

The architecture is stabilising, but APIs should still be considered experimental until `1.0.0`.

---

# License

Licensed under the GNU Affero General Public License v3.0 or later (`AGPL-3.0-or-later`).
