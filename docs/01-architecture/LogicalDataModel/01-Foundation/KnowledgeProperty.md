# KnowledgeProperty

**Version:** 1.0  
**Status:** Draft  
**Context:** Meta Model (Foundation)  
**Category:** Core Entity

---

# 1. Purpose

The KnowledgeProperty defines a reusable semantic characteristic that may be assigned to one or more KnowledgeObjects or SemanticRelationships.

It represents the meaning of a property rather than its value.

KnowledgeProperty enables consistent definition, validation and interpretation of business information across the Canonical Knowledge Model.

---

# 2. Definition

A KnowledgeProperty is a canonical definition of a semantic attribute.

It specifies:

- what information is being described,
- how the information should be interpreted,
- what type of value is expected,
- where the property may be applied.

A KnowledgeProperty never stores actual values.

It defines the semantics of a property.

---

# 3. Responsibilities

The KnowledgeProperty is responsible for:

- Defining reusable business properties.
- Providing consistent semantic interpretation.
- Defaining expected value types.
- Supporting validation.
- Supporting metadata management.
- Supporting interoperability.
- Supporting AI understanding.

The KnowledgeProperty is **not** responsible for:

- Storing property values.
- Managing runtime data.
- Holding application configuration.
- Implementing user interface behavior.

---

# 4. Design Principles

The KnowledgeProperty shall follow these principles.

1. Every property has exactly one semantic meaning.
2. Property definitions are reusable.
3. Property definitions are technology-independent.
4. Property values are stored outside the property definition.
5. Property definitions remain stable across versions.
6. Properties shall support semantic interoperability.

---

# 5. Canonical Identity

Every KnowledgeProperty owns one immutable Canonical Identifier.

Example:

```
KP-000021
```

Provider-specific properties shall be mapped to canonical properties whenever possible.

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

Property identity never changes.

---

# 7. Property Characteristics

Each KnowledgeProperty defines its semantic characteristics.

Typical characteristics include:

- Data Type
- Cardinality
- Mandatory / Optional
- Repeatable
- Default Value
- Unit of Measure
- Controlled Vocabulary
- Validation Pattern

These characteristics describe how values should be interpreted.

---

# 8. Attributes

The KnowledgeProperty defines the following conceptual attributes.

| Attribute | Required | Description |
|------------|----------|-------------|
| PropertyId | Yes | Immutable canonical identifier |
| Code | Yes | Stable canonical code |
| PreferredName | Yes | Canonical property name |
| Definition | Yes | Business definition |
| ValueType | Yes | Expected value type |
| Cardinality | Yes | Allowed number of values |
| Required | Yes | Indicates whether a value is mandatory |
| Repeatable | Yes | Indicates whether multiple values are allowed |
| UnitOfMeasure | No | Measurement unit |
| ValidationPattern | No | Validation expression |
| Status | Yes | Lifecycle status |

---

# 9. Business Rules

BR-001

Every KnowledgeProperty shall represent exactly one semantic meaning.

---

BR-002

Property definitions shall be reusable across multiple object types.

---

BR-003

KnowledgeProperty shall never store business values.

---

BR-004

A property may be applicable to multiple ObjectTypes.

---

BR-005

Canonical properties shall not be redefined by organizations.

Organizations may extend them through additional metadata.

---

# 10. Validation Rules

The platform shall validate that:

- Property identifier is unique.
- Code is unique.
- Definition exists.
- ValueType is valid.
- Cardinality is valid.
- ValidationPattern is compatible with ValueType.
- Controlled vocabulary exists when specified.

---

# 11. Examples

Examples of KnowledgeProperties.

| Property | Value Type |
|----------|------------|
| Preferred Name | Text |
| Definition | Long Text |
| Importance | Integer |
| Weight | Decimal |
| Confidence | Percentage |
| Difficulty | Integer |
| Language | Language Code |
| Effective From | Date |
| Effective To | Date |
| Version Number | Integer |

---

# 12. Non-Examples

The following are not KnowledgeProperties.

- Python Programming
- Leadership
- Software Engineer
- Coding Test
- Employee

These are KnowledgeObjects.

---

# 13. Extensibility

Organizations may introduce additional properties provided that:

- no canonical property already exists,
- semantic meaning is unique,
- validation rules are specified.

Canonical properties shall remain unchanged.

---

# 14. Notes

KnowledgeProperty defines semantic metadata.

Actual values belong to individual KnowledgeObjects or SemanticRelationships and are managed separately.

KnowledgeProperty improves consistency across providers and applications.

---

# 15. Open Questions

Property inheritance strategy will be specified in a future version of the Canonical Knowledge Model.

---

# 16. References

- CanonicalKnowledgeModel.md
- Knowledge Metadata Model
- Knowledge Graph Model
- Semantic Constraints Model
- Governance Model
