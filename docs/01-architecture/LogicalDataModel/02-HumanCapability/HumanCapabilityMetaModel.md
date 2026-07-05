# Human Capability Meta Model

**Version:** 1.0  
**Status:** Draft  
**Layer:** Domain Meta Model  
**Context:** Human Capability

---

# 1. Purpose

The Human Capability Meta Model defines the fundamental conceptual building blocks used to describe human capability within the HR Competency Engine.

It establishes the canonical semantic foundation upon which all capability-related knowledge is built.

The purpose of this model is not to define specific competencies or skills, but to define the types of concepts from which all human capability knowledge is constructed.

---

# 2. Scope

This meta model applies to every capability represented within the Canonical Knowledge Model, regardless of its source.

It governs capabilities originating from:

- OaSIS
- O*NET
- ESCO
- Organizational Libraries
- Customer Extensions
- AI-generated Knowledge

The model is provider-independent, technology-independent and organization-independent.

---

# 3. Design Objectives

The Human Capability Meta Model aims to:

- establish a common semantic language,
- eliminate ambiguity,
- support interoperability,
- enable semantic reasoning,
- support explainable AI,
- enable future knowledge evolution.

---

# 4. Modeling Philosophy

Human capability is not a single concept.

It is a structured system of complementary concepts that together explain what a person knows, can do, is capable of doing, and actually demonstrates.

The model distinguishes between elementary concepts and composite concepts.

---

# 5. Primitive Concepts

Primitive Concepts represent fundamental human capability concepts that cannot be decomposed into other capability concepts within the scope of this model.

The following concepts are considered primitive.

## Knowledge

Represents theoretical understanding, factual information or conceptual understanding acquired through education, study or experience.

Knowledge answers:

> What does a person know?

---

## Skill

Represents an acquired capability that can be learned, practiced and improved.

Skills require application.

Skills answer:

> What can a person do?

---

## Ability

Represents relatively stable human capacities that influence how effectively a person can acquire or perform skills.

Abilities answer:

> What is a person inherently capable of?

---

## Behavior

Represents observable actions performed by an individual.

Behaviors provide evidence of capabilities in real situations.

Behaviors answer:

> What does a person actually demonstrate?

---

# 6. Composite Concepts

Composite Concepts are constructed by combining primitive concepts through semantic relationships.

Within this model:

## Competency

A Competency represents an integrated human capability.

A competency is not an independent primitive concept.

Instead, it emerges from the combination of:

- Knowledge
- Skills
- Abilities
- Behaviors

Different competencies may require different combinations of these concepts.

---

# 7. Composition Model

The canonical composition model is illustrated conceptually below.

```
Knowledge
        \
         \
Skill -----\
            \
Ability ----- > Competency
            /
Behavior ---/
```

Competencies integrate multiple human capability dimensions.

No primitive concept is inherently more important than another.

---

# 8. Semantic Relationships

The following conceptual relationships are permitted.

Knowledge

- supports Skill
- contributes_to Competency

Skill

- requires Knowledge
- contributes_to Competency

Ability

- enables Skill
- contributes_to Competency

Behavior

- demonstrates Competency
- evidences Skill

Competency

- integrates Knowledge
- integrates Skill
- integrates Ability
- integrates Behavior

Additional semantic predicates may be introduced through the Meta Model.

---

# 9. Concept Independence

Primitive concepts remain independent.

A Skill is not a Knowledge.

A Knowledge is not an Ability.

A Behavior is not a Skill.

A Competency is not a Skill.

Each concept has its own identity, lifecycle and semantic meaning.

---

# 10. Granularity

The model supports multiple levels of granularity.

Example:

Knowledge

Programming Fundamentals

↓

Object-Oriented Programming

↓

Python Syntax

Skill

Programming

↓

Backend Development

↓

Python Programming

Competency

Software Engineering

↓

Backend Software Engineering

↓

Python Backend Development

Granularity is managed through Semantic Relationships rather than inheritance.

---

# 11. Extensibility

Future capability concepts may be introduced provided that:

- they represent a distinct semantic meaning,
- they cannot be represented using existing concepts,
- they preserve compatibility with the canonical model.

Extensions shall not redefine primitive concepts.

---

# 12. Constraints

The following constraints apply.

A primitive concept shall belong to exactly one primitive type.

A competency shall not redefine primitive concepts.

Composite concepts shall reference primitive concepts through Semantic Relationships.

Primitive concepts may exist independently.

Composite concepts may not exist without semantic composition.

---

# 13. Relationship with Other Models

This meta model is specialized by:

- HumanCapabilityOntology.md

It is implemented by:

- Competency.md
- Skill.md
- Knowledge.md
- Ability.md
- Behavior.md

It relies upon:

- KnowledgeObject.md
- SemanticRelationship.md
- SemanticPredicate.md
- KnowledgeProperty.md

---

# 14. Future Evolution

The Human Capability Meta Model is expected to support future extensions including:

- proficiency modeling,
- capability maturity,
- capability similarity,
- capability inference,
- competency embeddings,
- AI-assisted capability discovery,
- dynamic competency composition.

These extensions shall preserve the semantic integrity of the primitive concepts defined by this model.

---

# 15. References

- CanonicalKnowledgeModel.md
- HumanCapabilityContext.md
- KnowledgeObject.md
- SemanticRelationship.md
- SemanticPredicate.md
- KnowledgeProperty.md

---
End of Document
