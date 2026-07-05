# KnowledgeObject

**Version:** 1.0  
**Status:** Draft  
**Context:** Foundation  
**Category:** Core Entity

---

# 1. Purpose

The KnowledgeObject is the fundamental entity of the HR Competency Engine.

It represents any uniquely identifiable business concept that participates in the enterprise knowledge graph.

Every semantic concept managed by the platform shall be represented as a KnowledgeObject.

The KnowledgeObject provides a stable identity independent of providers, organizations, technologies and implementation details.

---

# 2. Definition

A KnowledgeObject is a uniquely identifiable semantic concept with a stable business meaning.

A KnowledgeObject may represent tangible or intangible concepts, provided that the concept has an independent business identity.

KnowledgeObjects are connected through SemanticRelationships to form the Canonical Knowledge Graph.

---

# 3. Responsibilities

The KnowledgeObject is responsible for:

- Representing a unique business concept.
- Providing a stable canonical identity.
- Acting as a node within the Knowledge Graph.
- Supporting semantic relationships.
- Supporting metadata and governance.
- Supporting mappings from external knowledge providers.
- Remaining independent from implementation technologies.

The KnowledgeObject is **not** responsible for:

- Organizational policies.
- Runtime business data.
- Assessment results.
- Database implementation.
- User interface behavior.

---

# 4. Design Principles

The KnowledgeObject shall follow these principles:

1. Every object has exactly one canonical identity.
2. Identity is immutable.
3. Meaning is stable across versions.
4. Objects represent business concepts, not implementation artifacts.
5. Objects shall be reusable across all HR modules.
6. Objects shall be technology-independent.
7. Objects shall participate in semantic relationships.

---

# 5. Canonical Identity

Each KnowledgeObject owns one globally unique Canonical Identifier.

The canonical identity:

- never changes,
- is provider-independent,
- is organization-independent,
- survives version changes,
- survives provider migrations.

Provider identifiers are mapped to the canonical identity rather than replacing it.

Example:

Canonical ID

```
KO-00000452
```

Mapped identifiers

```
ESCO: 12345

O*NET: 15-1252

OaSIS: CP-00198
```

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

Lifecycle transitions are governed by the Governance Model.

Identity remains unchanged throughout the lifecycle.

---

# 7. Relationships

A KnowledgeObject may participate in any number of SemanticRelationships.

Typical relationships include:

- requires
- measured_by
- developed_by
- assessed_by
- equivalent_to
- broader_than
- narrower_than
- related_to
- part_of

Relationship semantics are defined by RelationshipType.

---

# 8. Attributes

The KnowledgeObject defines the following conceptual attributes.

| Attribute | Required | Description |
|------------|----------|-------------|
| CanonicalId | Yes | Immutable canonical identifier |
| ObjectType | Yes | Type of business concept |
| PreferredName | Yes | Primary display name |
| Definition | Yes | Canonical business definition |
| Status | Yes | Lifecycle status |
| CreatedAt | Yes | Creation timestamp |
| UpdatedAt | Yes | Last modification timestamp |

Additional metadata shall be defined outside the core entity.

---

# 9. Business Rules

BR-001

Every KnowledgeObject shall have exactly one canonical identity.

---

BR-002

A KnowledgeObject shall belong to exactly one ObjectType.

---

BR-003

A KnowledgeObject may participate in multiple SemanticRelationships.

---

BR-004

Deleting a KnowledgeObject is prohibited once published.

Objects shall be deprecated instead.

---

BR-005

Business meaning shall remain stable across versions.

---

# 10. Validation Rules

The platform shall validate that:

- CanonicalId is unique.
- ObjectType exists.
- PreferredName is not empty.
- Definition exists.
- Lifecycle state is valid.
- No circular self-reference exists unless explicitly allowed.
- Semantic constraints are satisfied.

---

# 11. Examples

Examples of valid KnowledgeObjects:

| Object Type | Name |
|-------------|------|
| Competency | Leadership |
| Skill | Python Programming |
| Knowledge | Database Design |
| Ability | Numerical Reasoning |
| Behavior | Active Listening |
| Role | Senior Software Engineer |
| Occupation | Software Developer |
| Assessment Method | Technical Interview |
| Learning Activity | Python Bootcamp |
| Certification | AWS Certified Developer |

---

# 12. Non-Examples

The following should **not** be modeled as KnowledgeObjects.

- Employee
- Candidate
- Assessment Result
- Performance Review
- Login User
- Database Table
- API Endpoint
- HTML Page

These belong to runtime or implementation models.

---

# 13. Extensibility

Organizations may extend KnowledgeObjects through:

- additional metadata,
- localized names,
- external references,
- provider mappings,
- organizational classifications.

Extensions shall not modify canonical identity.

---

# 14. Notes

KnowledgeObject represents semantic identity.

It is the root abstraction upon which all canonical knowledge is built.

Business modules consume KnowledgeObjects but do not redefine them.

---

# 15. Open Questions

None.

---

# 16. References

- CanonicalKnowledgeModel.md
- Knowledge Graph Model
- Semantic Constraints Model
- Governance Model
- Query & Reasoning Model
