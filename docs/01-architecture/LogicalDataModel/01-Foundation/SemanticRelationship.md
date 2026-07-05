# SemanticRelationship

**Version:** 1.0  
**Status:** Draft  
**Context:** Meta Model (Foundation)  
**Category:** Core Entity

---

# 1. Purpose

The SemanticRelationship represents a meaningful, typed and directed connection between two KnowledgeObjects.

It is a first-class semantic entity that defines how concepts relate to one another within the Canonical Knowledge Graph.

Rather than acting as a simple reference or foreign-key association, a SemanticRelationship carries its own business meaning, lifecycle, governance and metadata.

---

# 2. Definition

A SemanticRelationship is a directed semantic connection between a source KnowledgeObject and a target KnowledgeObject.

Each relationship has an explicitly defined semantic meaning through its RelationshipType.

Relationships may also carry metadata, provenance, confidence, validity periods and governance information.

---

# 3. Responsibilities

The SemanticRelationship is responsible for:

- Connecting two KnowledgeObjects.
- Expressing semantic meaning.
- Preserving relationship direction.
- Supporting graph traversal.
- Supporting semantic reasoning.
- Supporting explainable AI.
- Supporting governance and versioning.
- Supporting provider mappings.

The SemanticRelationship is **not** responsible for:

- Storing business data.
- Representing organizational policies.
- Executing business rules.
- Containing application logic.

---

# 4. Design Principles

The SemanticRelationship shall follow these principles.

1. Every relationship connects exactly two KnowledgeObjects.
2. Every relationship has exactly one RelationshipType.
3. Relationships are directed unless explicitly declared symmetric.
4. Relationships are semantically meaningful.
5. Relationships have independent lifecycle management.
6. Relationships are technology-independent.
7. Relationships are traceable and explainable.

---

# 5. Canonical Identity

Every SemanticRelationship owns a globally unique Canonical Identifier.

The identifier remains stable throughout the relationship lifecycle.

Example:

```
SR-00000487
```

Provider-specific relationship identifiers shall be mapped to the canonical relationship rather than replacing it.

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

Relationship identity remains immutable.

Relationship meaning shall not change after publication.

---

# 7. Participants

Every SemanticRelationship contains:

| Role | Description |
|------|-------------|
| Source KnowledgeObject | Starting concept |
| RelationshipType | Semantic meaning |
| Target KnowledgeObject | Destination concept |

Example:

```
Python Programming

requires

Programming Fundamentals
```

---

# 8. Attributes

The SemanticRelationship defines the following conceptual attributes.

| Attribute | Required | Description |
|------------|----------|-------------|
| RelationshipId | Yes | Immutable canonical identifier |
| SourceKnowledgeObjectId | Yes | Source node |
| RelationshipTypeId | Yes | Semantic relationship type |
| TargetKnowledgeObjectId | Yes | Target node |
| Status | Yes | Lifecycle status |
| EffectiveFrom | No | Validity start |
| EffectiveTo | No | Validity end |
| CreatedAt | Yes | Creation timestamp |
| UpdatedAt | Yes | Last modification timestamp |

Additional governance metadata shall be managed separately.

---

# 9. Business Rules

BR-001

Every SemanticRelationship shall connect exactly two KnowledgeObjects.

---

BR-002

Every SemanticRelationship shall reference exactly one RelationshipType.

---

BR-003

Source and Target KnowledgeObjects shall exist.

---

BR-004

Relationship direction is semantically significant unless explicitly defined as symmetric.

---

BR-005

Published relationships shall never change semantic meaning.

---

BR-006

Relationships may be deprecated but shall not be physically deleted.

---

# 10. Validation Rules

The platform shall validate that:

- Source KnowledgeObject exists.
- Target KnowledgeObject exists.
- RelationshipType exists.
- RelationshipType is allowed between the specified ObjectTypes.
- No duplicate canonical relationship exists.
- Circular relationships comply with Semantic Constraints.
- Lifecycle state is valid.

---

# 11. Examples

Examples of valid SemanticRelationships.

| Source | Relationship | Target |
|---------|--------------|--------|
| Software Engineer | requires | Problem Solving |
| Leadership | developed_by | Leadership Workshop |
| Python Programming | measured_by | Coding Test |
| Communication | related_to | Collaboration |
| Data Analysis | broader_than | Statistical Analysis |

---

# 12. Non-Examples

The following are not SemanticRelationships.

- Employee reports to Manager
- User created Role
- Candidate submitted Application
- Assessment Result belongs to Employee
- Database Foreign Key

These represent runtime or implementation relationships rather than canonical semantic relationships.

---

# 13. Extensibility

Organizations may extend relationships by adding:

- Confidence
- Weight
- Provenance
- Local metadata
- Organizational annotations

Extensions shall not modify the canonical semantic meaning.

---

# 14. Notes

Relationships are first-class citizens within the Knowledge Graph.

Business meaning often resides as much in relationships as in the KnowledgeObjects themselves.

Reasoning engines and AI services primarily operate by traversing SemanticRelationships.

---

# 15. Open Questions

None.

---

# 16. References

- CanonicalKnowledgeModel.md
- Knowledge Graph Model
- Query & Reasoning Model
- Semantic Constraints Model
- Governance Model
