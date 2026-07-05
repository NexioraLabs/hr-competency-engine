# SemanticPredicate

**Version:** 1.0  
**Status:** Draft  
**Context:** Meta Model (Foundation)  
**Category:** Core Entity

---

# 1. Purpose

The SemanticPredicate defines the semantic meaning of a relationship between two KnowledgeObjects.

A SemanticPredicate represents a reusable business verb that describes how one concept relates to another within the Canonical Knowledge Graph.

Every SemanticRelationship shall reference exactly one SemanticPredicate.

---

# 2. Definition

A SemanticPredicate is a canonical semantic connector.

It specifies the meaning, direction and logical characteristics of relationships without representing individual relationship instances.

Examples include:

- requires
- developed_by
- measured_by
- assessed_by
- broader_than
- narrower_than
- equivalent_to
- related_to
- part_of

SemanticPredicates are reusable across all KnowledgeObjects.

---

# 3. Responsibilities

The SemanticPredicate is responsible for:

- Defining semantic meaning.
- Defining relationship direction.
- Defining logical characteristics.
- Supporting reasoning engines.
- Supporting graph traversal.
- Supporting semantic validation.
- Supporting explainable AI.

The SemanticPredicate is **not** responsible for:

- Connecting specific KnowledgeObjects.
- Holding runtime data.
- Executing business rules.
- Representing organizational policies.

---

# 4. Design Principles

The SemanticPredicate shall follow these principles.

1. Every predicate has one canonical meaning.
2. Predicate meaning is stable over time.
3. Predicates are reusable.
4. Predicates are technology-independent.
5. Predicates are independent of providers.
6. Predicates shall support semantic reasoning.

---

# 5. Canonical Identity

Each SemanticPredicate owns one immutable Canonical Identifier.

Example:

```
SP-00012
```

Provider-specific predicate names shall be mapped to canonical predicates.

---

# 6. Lifecycle

Typical lifecycle:

```
Draft

↓

Validated

↓

Approved

↓

Published

↓

Deprecated

↓

Archived
```

Predicate identity never changes.

---

# 7. Semantic Characteristics

A SemanticPredicate defines semantic behavior.

Typical characteristics include:

- Directional
- Symmetric
- Asymmetric
- Transitive
- Reflexive
- Inverse Predicate
- Reasoning Enabled
- AI Explainable

These characteristics determine how the graph behaves during reasoning.

---

# 8. Attributes

The SemanticPredicate defines the following conceptual attributes.

| Attribute | Required | Description |
|------------|----------|-------------|
| PredicateId | Yes | Immutable canonical identifier |
| Code | Yes | Stable canonical code |
| PreferredName | Yes | Canonical business name |
| Definition | Yes | Business meaning |
| Directional | Yes | Indicates directionality |
| Symmetric | Yes | Indicates symmetry |
| Transitive | Yes | Indicates transitivity |
| Reflexive | Yes | Indicates reflexivity |
| InversePredicateId | No | Inverse predicate |
| ReasoningEnabled | Yes | Participates in inference |
| Explainable | Yes | Can be explained to users |
| Status | Yes | Lifecycle state |

---

# 9. Business Rules

BR-001

Every SemanticPredicate shall represent exactly one semantic meaning.

---

BR-002

Predicate meaning shall remain stable across versions.

---

BR-003

A predicate may define one inverse predicate.

---

BR-004

Inverse predicates shall reference each other.

Example:

requires

⇄

required_by

---

BR-005

Symmetric predicates shall not require inverse predicates.

Example:

related_to

---

BR-006

Predicates shall be reusable across all domains.

---

# 10. Validation Rules

The platform shall validate that:

- Predicate identifier is unique.
- Canonical code is unique.
- Definition exists.
- Symmetric predicates have no inverse.
- Inverse predicates reference each other.
- Logical characteristics are internally consistent.

---

# 11. Examples

Examples of SemanticPredicates.

| Predicate | Description |
|------------|-------------|
| requires | Source depends on target |
| measured_by | Source is measured using target |
| developed_by | Source is improved through target |
| assessed_by | Source is evaluated through target |
| broader_than | Source is semantically broader |
| narrower_than | Source is semantically narrower |
| equivalent_to | Source and target represent equivalent meaning |
| part_of | Source belongs to target |
| related_to | Source has semantic association with target |

---

# 12. Non-Examples

The following are not SemanticPredicates.

- Employee reports to Manager
- User created Role
- Database Foreign Key
- Screen Navigation
- REST Endpoint

These belong to runtime or implementation models.

---

# 13. Extensibility

Organizations may introduce additional predicates provided that:

- the semantic meaning is unique,
- no existing predicate already expresses the same concept,
- the predicate complies with the Semantic Constraints Model.

Canonical predicates shall never be redefined.

---

# 14. Notes

SemanticPredicate represents the vocabulary of the Knowledge Graph.

It defines the language through which KnowledgeObjects are connected.

Reasoning engines interpret the graph primarily through predicates.

---

# 15. Open Questions

None.

---

# 16. References

- CanonicalKnowledgeModel.md
- Knowledge Graph Model
- Semantic Constraints Model
- Query & Reasoning Model
- Governance Model
