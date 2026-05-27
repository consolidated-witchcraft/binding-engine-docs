# Binding Syntax

BindingEngine extends markdown with semantic bindings.

Bindings allow authored prose to expose structured semantic meaning while remaining:
- readable
- expressive
- author-friendly

Bindings are intentionally designed to integrate naturally into text rather than replace it.

---

## Core Philosophy

Binding syntax is intended to:
- enrich prose
- expose semantic structure explicitly
- preserve authored intent
- remain human-readable

Bindings are NOT intended to:
- become a programming language
- replace natural writing
- force rigid authoring workflows
- encode hidden semantic inference

Example:

```markdown
@person[jane-austen](Jane Austen) was an English writer.
```

This remains readable to humans while exposing:
- a semantic binding type
- a semantic identifier
- an authored label

---

## Binding Structure

A binding has three conceptual components:

```text
@binding-type[payload](label)
```

| Component | Purpose |
|---|---|
| `binding-type` | The semantic category |
| `payload` | Structured semantic data |
| `label` | Human-readable authored text |

Example:

```markdown
@person[jane-austen](Jane Austen)
```

| Component | Value |
|---|---|
| binding type | `person` |
| payload | `jane-austen` |
| label | `Jane Austen` |

---

## Binding Types

Binding types are defined by vocabularies.

Examples may include:
- `person`
- `place`
- `event`
- `relationship`
- `object`
- `faction`

Binding types are application-specific and vocabulary-driven.

BindingEngine itself does not impose a universal semantic schema.

---

## Payload Shapes

Bindings support multiple payload shapes.

Currently supported payload shapes include:
- shorthand payloads
- attribute-list payloads

---

## Shorthand Payloads

Shorthand payloads represent a single semantic identifier.

Example:

```markdown
@person[jane-austen](Jane Austen)
```

The payload is:

```text
jane-austen
```

Shorthand payloads are typically used for:
- entities
- references
- identifiers
- lightweight semantic links

---

## Attribute-List Payloads

Attribute-list payloads expose structured semantic attributes.

Example:

```markdown
@relationship[
    type: parent_of,
    subject: george-austen,
    object: jane-austen
](George Austen was Jane Austen’s father)
```

This payload contains three attributes:

| Attribute | Value |
|---|---|
| `type` | `parent_of` |
| `subject` | `george-austen` |
| `object` | `jane-austen` |

Attribute-list payloads are typically used for:
- events
- relationships
- structured semantic claims
- temporal structures
- metadata-rich bindings

---

## Labels

The label is the human-readable authored text.

Example:

```markdown
@place[steventon-hampshire](Steventon, Hampshire)
```

The label is:

```text
Steventon, Hampshire
```

Labels are:
- presentation-oriented
- human-readable
- authored prose

Labels are NOT:
- semantic identifiers
- canonical values
- semantic keys

Semantic meaning should come from payload structure rather than labels.

---

## Bindings Within Prose

Bindings are intended to appear naturally within prose.

Example:

```markdown
Jane Austen was born in @place[steventon-hampshire](Steventon, Hampshire).
```

Bindings should not force authors to radically alter writing style.

This principle is foundational to BindingEngine’s design philosophy.

---

## Multi-Line Attribute Payloads

Attribute-list payloads may span multiple lines for readability.

Example:

```markdown
@event[
    type: birth,
    subject: jane-austen,
    occurred-at: gregorian:1775-12-16,
    location: steventon-hampshire
](Birth of Jane Austen)
```

Whitespace within attribute payloads is generally non-semantic.

---

## Attribute Roles

Attributes may have different semantic roles within vocabularies.

Examples include:
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
- `revealed-at` controls presentation visibility

Visibility metadata may survive the semantic pipeline without contributing to semantic identity.

---

## Source Spans

Bindings preserve exact source locations.

This allows downstream systems to:
- trace semantic claims back to source text
- generate diagnostics
- provide editor tooling
- support provenance tracking

Example conceptual span:

```text
sourceSpan: [142, 261)
```

---

## Escaping

Bindings may contain characters requiring escaping depending on payload structure.

Exact escaping behaviour is parser-specific and may evolve over time.

Applications should prefer:
- semantic identifiers
- explicit payload structure
- predictable attribute formatting

over complex inline escaping patterns.

---

## Invalid Bindings

Bindings may be syntactically invalid or semantically invalid.

Examples:
- malformed payloads
- missing delimiters
- unknown binding types
- invalid attribute values

Parser diagnostics identify syntax issues.

Vocabulary validation diagnostics identify semantic issues.

---

## Parser Responsibility

The parser is responsible for:
- recognising bindings
- constructing AST structures
- preserving source spans
- reporting syntax diagnostics

The parser is NOT responsible for:
- semantic validation
- inference
- canonicalisation
- graph construction

---

## Vocabulary Responsibility

Vocabularies define:
- which binding types exist
- which payload shapes are allowed
- which attributes are valid
- value types
- semantic roles

Binding syntax therefore remains:
- extensible
- domain-neutral
- application-neutral

---

## Semantic Claims, Not Truth

Bindings represent:
> authored semantic claims

rather than:
> canonical objective truth.

Example:

```markdown
@relationship[
    type: ruler_of,
    subject: king-arthur,
    object: camelot
](Arthur ruled Camelot)
```

The binding expresses:
- what the document claims

not:
- universal canonical truth

Multiple documents may express conflicting semantic claims.

Conflict resolution belongs to downstream systems.

---

## Design Principles

Binding syntax prioritises:
- readability
- explicit semantics
- deterministic parsing
- author-friendly structure
- provenance preservation

Binding syntax intentionally avoids:
- hidden semantic inference
- magical shorthand expansion
- parser-level canonicalisation
- implicit graph semantics

---

## Future Expansion

Future syntax capabilities may include:
- nested bindings
- richer value types
- typed references
- semantic macros
- inline semantic annotations
- domain-specific vocabulary extensions

However, BindingEngine intends to remain:
- deterministic
- provenance-aware
- application-neutral
- human-readable