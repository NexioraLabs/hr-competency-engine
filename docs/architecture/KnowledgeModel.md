# Knowledge Model

**Project:** HR Competency Engine (Enterprise Competency Knowledge Platform)

**Document ID:** KM-001

**Version:** 2.0 (Draft)

**Status:** Working Draft

**Last Updated:** 2026-04-07

---

# 1. Introduction

## 1.1 Purpose

The Knowledge Model defines the conceptual foundation of the HR Competency Engine.

Its purpose is to provide a provider-independent, extensible and versioned representation of occupational knowledge, competencies, skills and their relationships.

Unlike traditional HR systems that store competencies as isolated records, this model represents organizational knowledge as an interconnected graph of concepts that can be imported from multiple international competency frameworks.

The Knowledge Model is the highest-level architectural specification of the platform.

Every database schema, API, import mechanism, reporting engine and AI capability must conform to this specification.

---

## 1.2 Goals

The Knowledge Model has the following goals.

### Provider Independence

The platform shall support multiple external providers without requiring structural changes.

Examples include:

- OaSIS
- O*NET
- ESCO
- SFIA
- APQC
- Customer-defined libraries

The internal architecture must never assume the existence of a particular provider.

---

### Long-term Stability

The conceptual model should remain stable even when:

- new competency frameworks appear
- providers publish new versions
- new entity types are introduced
- AI capabilities are added

Database redesign should not be required.

---

### Extensibility

New concepts shall be introduced by configuration rather than schema modification whenever possible.

Examples:

- New Entity Types
- New Relation Types
- New Competency Categories
- New Collections

---

### Separation of Knowledge and Customer Data

Knowledge libraries are read-only reference sources.

Customer operational data must always remain independent.

The Import Engine is the only mechanism that transfers knowledge into customer-owned data structures.

---

### Internationalization

The model shall support multilingual content as a first-class capability.

Languages must never require schema redesign.

---

### Enterprise Scalability

The architecture must support:

- millions of entities
- millions of relationships
- multiple providers
- multiple versions
- concurrent imports

without conceptual redesign.

---

## 1.3 Scope

The Knowledge Model is responsible for representing:

- occupations
- competencies
- skills
- knowledge
- abilities
- tasks
- work activities
- work context
- qualifications
- education
- certifications
- technologies
- tools
- behavioral indicators
- collections
- hierarchical structures
- semantic relationships

The Knowledge Model is NOT responsible for:

- employee information
- competency assessments
- learning records
- performance management
- recruitment workflows
- succession planning

Those domains belong to the Core HR Model.

---

## 1.4 Architectural Position

The HR Competency Engine consists of two independent domains.

```
                External Providers
                       │
      ┌────────────────────────────────┐
      │                                │
      ▼                                ▼
 Knowledge Model              Customer Core Model
      │                                │
      └──────────────┬─────────────────┘
                     │
               Import Engine
```

The Knowledge Model owns reference knowledge.

The Customer Core owns operational business data.

Neither layer directly depends on the internal implementation of the other.

---

## 1.5 Design Philosophy

The Knowledge Model is intentionally designed as a **Meta Model**, not as a collection of tables.

This distinction is fundamental.

Traditional HR systems model concepts such as:

- Job
- Skill
- Knowledge
- Task

using dedicated database tables.

This approach tightly couples the database schema to a specific competency framework.

The HR Competency Engine adopts a different philosophy.

Everything inside a knowledge library is treated as a Knowledge Entity.

Relationships between concepts are represented explicitly rather than implicitly.

As a result:

- new standards can be supported without redesign
- new entity types can be introduced without changing existing structures
- relationships become first-class architectural elements
- graph-like capabilities become available while remaining fully compatible with PostgreSQL

This philosophy has been validated against:

- OaSIS
- O*NET
- ESCO

and forms the architectural foundation of the platform.

---

# 2. Core Concepts

## 2.1 Introduction

The Knowledge Model is built around a small number of fundamental concepts.

Every structure, relationship, API, import process and future AI capability is derived from these concepts.

The purpose of this chapter is not to describe database tables.

Instead, it defines the business vocabulary of the platform.

Every subsequent document—including the physical database model—must conform to these concepts.

---

# 2.2 Knowledge Provider

## Purpose

A Knowledge Provider represents the organization responsible for publishing a body of knowledge.

Examples include international standards, governmental organizations, industry associations, commercial vendors, or customer-defined repositories.

Examples:

- OaSIS
- O*NET
- ESCO
- SFIA
- APQC
- Customer Library

---

## Design Rationale

Knowledge published by different organizations evolves independently.

Each provider has:

- its own release cycle
- terminology
- governance model
- identifiers
- licensing rules

The architecture must therefore isolate providers from one another.

The platform shall never assume that two providers describe the same concept in the same way.

---

## Business Rules

• Every Knowledge Library belongs to exactly one Provider.

• Providers never share versions.

• Providers are immutable business identities.

---

# 2.3 Knowledge Library

## Purpose

A Knowledge Library represents a coherent body of knowledge published by a provider.

Examples:

OaSIS

• IT Occupations

• Healthcare

ESCO

• Occupations

• Skills

Customer

• Internal Leadership Framework

---

## Design Rationale

Providers frequently publish multiple independent knowledge domains.

Treating them as separate libraries enables:

- selective import
- independent versioning
- independent lifecycle management

---

## Business Rules

A Library:

- belongs to one Provider
- contains multiple Versions
- may be active or archived
- is immutable once released

---

# 2.4 Knowledge Version

## Purpose

A Version represents a snapshot of a Library at a particular point in time.

Examples:

OaSIS 2025

ESCO v1.2

O*NET 30.0

---

## Design Rationale

Knowledge continuously evolves.

Occupations change.

Skills appear.

Competencies are retired.

Versioning guarantees that historical imports remain reproducible.

Customer data must always be traceable back to the exact version from which it originated.

---

## Business Rules

Versions are immutable.

Once published, a Version cannot be modified.

Corrections require a new Version.

---

# 2.5 Knowledge Entity

## Purpose

Knowledge Entity is the central concept of the entire architecture.

Everything contained inside a Knowledge Library is represented as a Knowledge Entity.

Examples include:

Occupation

Competency

Task

Technology

Qualification

Tool

Certification

Context

Behavior Indicator

Collection

---

## Design Rationale

Traditional HR systems model each concept using a dedicated database table.

This creates rigid schemas that are difficult to extend.

The Knowledge Model instead represents every concept uniformly.

Behavior is determined by metadata rather than by physical schema.

This allows future standards to introduce new concept types without requiring database redesign.

---

## Business Rules

Every Entity:

- belongs to one Version
- has one Entity Type
- may participate in zero or more Relations
- may have multilingual labels
- may belong to multiple Collections
- may have arbitrary metadata

Entities never exist outside a Version.

---

# 2.6 Knowledge Relation

## Purpose

A Knowledge Relation represents an explicit semantic relationship between two Knowledge Entities.

Examples:

Occupation

REQUIRES

Competency

---

Competency

CONTAINS

Behavior Indicator

---

Task

USES

Technology

---

Qualification

RELATED TO

Occupation

---

## Design Rationale

Relationships are first-class architectural elements.

The model intentionally avoids hidden or implicit relationships.

Every meaningful dependency is explicitly represented.

This enables:

- graph traversal
- impact analysis
- AI reasoning
- career path discovery
- recommendation engines

without architectural changes.

---

## Business Rules

Every Relation:

- has one source Entity
- has one target Entity
- has one Relation Type
- belongs to one Version
- may contain Relation Attributes

---

# 2.7 Relation Attributes

## Purpose

Many knowledge frameworks assign properties to relationships rather than entities.

Examples:

Programming

Importance = 92

Required Level = Expert

Mandatory = Yes

Experience = 3 Years

These values describe the relationship between Occupation and Competency—not either entity independently.

---

## Design Rationale

Validation against OaSIS, O*NET and ESCO demonstrated that relation metadata is more important than entity metadata.

For this reason, Relation Attributes are treated as first-class concepts.

---

## Business Rules

Relation Attributes never exist independently.

They always belong to exactly one Relation.

---

# 2.8 Collections

## Purpose

Collections provide logical grouping independently of hierarchical relationships.

Examples:

Digital Skills

Leadership Competencies

Green Skills

AI Technologies

---

## Design Rationale

Hierarchy answers:

"What is the parent?"

Collections answer:

"What belongs together?"

These are fundamentally different concepts.

An Entity may belong to multiple Collections.

---

# 2.9 Translations

## Purpose

Translations enable multilingual representation of knowledge.

Examples:

English

French

German

Arabic

Persian

---

## Design Rationale

Internationalization is a core architectural capability—not an optional feature.

All user-visible text should be represented independently from the conceptual model.

---

# 2.10 Import

## Purpose

Import is the controlled process that transforms reference knowledge into customer-owned operational data.

Knowledge remains immutable.

Customer data remains independent.

Import is the bridge between the two domains.

---

End of Chapter 2

# 3. Meta Model

## 3.1 Purpose

This chapter defines the structural architecture of the Knowledge Model.

Unlike previous chapters that define business concepts, this chapter specifies how those concepts are represented and connected.

The Meta Model is independent of any external framework.

Whether the source is OaSIS, O*NET, ESCO, SFIA, APQC or a customer-defined library, the same Meta Model shall be used.

This chapter represents the architectural core of the platform.

---

# 3.2 Philosophy

The Knowledge Model does not model occupations, competencies or tasks directly.

Instead, it models knowledge.

Everything inside a knowledge library is represented as a Knowledge Entity.

Relationships between concepts are represented as Knowledge Relations.

The model intentionally minimizes structural assumptions.

This philosophy allows the platform to support future frameworks without schema redesign.

---

# 3.3 Meta Object Types

The architecture is built around five fundamental object families.

```
Knowledge Provider

↓

Knowledge Library

↓

Knowledge Version

↓

Knowledge Entity

↓

Knowledge Relation
```

Everything else is metadata.

This decision dramatically reduces architectural complexity while maximizing extensibility.

---

# 3.4 Entity-Centric Architecture

Traditional HR systems typically implement structures similar to:

Job

Skill

Knowledge

Task

Certification

Education

Tool

Technology

...

using independent database tables.

The Knowledge Model intentionally rejects this approach.

Instead:

Every concept is represented by a Knowledge Entity.

Behavior is determined by metadata rather than schema.

Advantages include:

• unlimited extensibility

• simplified API design

• unified search

• graph traversal

• AI compatibility

• framework independence

---

# 3.5 Relationship-Centric Architecture

Relationships are first-class architectural objects.

They are not implemented as hidden foreign keys.

Every semantic connection is explicitly represented.

Examples:

Occupation

REQUIRES

Competency

---

Task

USES

Technology

---

Competency

CONTAINS

Behavior Indicator

---

Occupation

REQUIRES

Qualification

---

Skill

IS PART OF

Collection

Each relationship may contain its own metadata.

This architecture was validated using OaSIS, O*NET and ESCO.

---

# 3.6 Relation Metadata

One of the most important architectural discoveries during validation was that the most valuable information belongs to relationships—not entities.

Example:

Occupation

Software Developer

↓

Programming

↓

Importance = 95

↓

Required Level = Advanced

↓

Mandatory = Yes

↓

Experience = 3 Years

Programming itself has none of these properties.

The relationship owns them.

Therefore:

Relations are modeled as business objects.

Not as simple foreign keys.

---

# 3.7 Hierarchies

Hierarchies are implemented using ordinary relationships.

The model does not introduce special hierarchy tables.

Examples:

Parent Of

Child Of

Broader

Narrower

This enables unlimited hierarchy depth.

Examples:

Occupation Hierarchy

Competency Hierarchy

Technology Hierarchy

Qualification Hierarchy

Collections

---

# 3.8 Multiple Classification Systems

The same Entity may simultaneously belong to multiple classification systems.

Example:

Python Programming

↓

Digital Skills

↓

Software Development

↓

Programming Languages

↓

AI Technologies

These are independent classifications.

The architecture never assumes only one hierarchy exists.

---

# 3.9 Collections versus Hierarchies

Collections are intentionally separated from hierarchical relationships.

Hierarchy answers:

"What is the parent?"

Collection answers:

"What belongs together?"

Example:

Docker

Hierarchy

↓

Container Technology

Collection

↓

DevOps Toolkit

Collection

↓

Cloud Native Stack

An Entity may belong to unlimited Collections.

---

# 3.10 Identity

Every Entity has two identities.

Internal Identity

Generated by the platform.

External Identity

Provided by the original knowledge source.

Examples:

ESCO URI

O*NET Code

OaSIS Identifier

This enables future synchronization between library versions.

---

# 3.11 Version Isolation

Versions are immutable.

Entities from different versions never coexist inside the same logical model.

Relationships cannot connect entities belonging to different versions.

This guarantees reproducibility.

---

# 3.12 Graph Characteristics

Although implemented on PostgreSQL,

the conceptual model behaves as a Property Graph.

Node

↓

Knowledge Entity

Edge

↓

Knowledge Relation

Edge Properties

↓

Relation Attributes

Node Properties

↓

Entity Properties

This allows future migration to native graph databases without redesigning the conceptual model.

---

# 3.13 Architecture Constraints

The following rules are mandatory.

Rule 1

Every Entity belongs to exactly one Version.

Rule 2

Every Relation belongs to exactly one Version.

Rule 3

Relations cannot cross Versions.

Rule 4

Knowledge is immutable.

Rule 5

Customer data is never stored inside the Knowledge Model.

Rule 6

Every import creates customer-owned copies.

Rule 7

Business logic shall never depend on a specific Provider.

Rule 8

New Entity Types must not require database redesign.

Rule 9

New Relation Types must not require application redesign.

Rule 10

The Meta Model must remain provider-independent.

---

# 3.14 Validation Matrix

| Requirement | OaSIS | O*NET | ESCO |
|-------------|:-----:|:------:|:-----:|
| Versioning | ✅ | ✅ | ✅ |
| Entity Model | ✅ | ✅ | ✅ |
| Relation Model | ✅ | ✅ | ✅ |
| Relation Metadata | ✅ | ✅ | ✅ |
| Hierarchy | ✅ | ✅ | ✅ |
| Multiple Classifications | ⚠ | ✅ | ✅ |
| Collections | — | — | ✅ |
| External Identifier | ⚠ | ✅ | ✅ |
| Multilingual Labels | — | — | ✅ |

The Meta Model satisfies all mandatory requirements identified during validation.

---

End of Chapter 3

# 4. Logical Knowledge Model

## 4.1 Purpose

The purpose of the Logical Knowledge Model is to define the business behavior of the Knowledge Model.

Unlike the Conceptual Model, this chapter does not describe ideas.

Unlike the Physical Model, this chapter does not describe tables.

Instead, it defines the lifecycle, responsibilities and behavior of every business object.

This chapter serves as the bridge between architecture and implementation.

---

# 4.2 Business Object

Every Knowledge Entity is considered a Business Object.

A Business Object is more than stored information.

It has:

- identity
- lifecycle
- state
- ownership
- relationships
- constraints

The platform therefore manages business objects instead of records.

---

# 4.3 Lifecycle

Every Knowledge Entity passes through the following lifecycle.

```

Draft

↓

Validated

↓

Published

↓

Deprecated

↓

Archived

```

Only Published entities may be imported into customer systems.

Draft entities are never visible outside the authoring process.

Archived entities remain available for historical reference.

---

# 4.4 Responsibilities

Every Entity is responsible for:

maintaining its identity

maintaining its metadata

maintaining its translations

maintaining its relationships

maintaining its lifecycle state

The Entity is NOT responsible for:

customer assessments

learning records

employee competencies

performance evaluations

These belong to the Customer Core.

---

# 4.5 Identity Rules

Every Entity owns one permanent internal identity.

This identity never changes.

External identifiers may change between Providers.

Internal identifiers never change.

---

# 4.6 Version Rules

Knowledge is immutable.

Published Versions are immutable.

Entities belonging to published versions are immutable.

Corrections always generate a new Version.

The system never edits published knowledge.

---

# 4.7 Relationship Rules

Relationships are business objects.

A relationship may exist even when no attributes are defined.

Relationship attributes never exist without a relationship.

Deleting a relationship deletes all relation attributes.

---

# 4.8 Translation Rules

Translations belong to Entities.

Translations never modify business meaning.

Translations only affect presentation.

One translation is designated as the Preferred Language.

Additional translations remain optional.

---

# 4.9 Collections

Collections are logical views.

Collections never own Entities.

Removing an Entity from a Collection never deletes the Entity.

Collections support:

navigation

recommendation

search

filtering

knowledge discovery

---

# 4.10 Classification

Classifications represent standardized taxonomies.

Examples include:

ISCO

NOC

ESCO

SOC

Customer-defined structures

One Entity may belong to multiple classifications simultaneously.

---

# 4.11 Ownership

Ownership exists at Library level.

Entities inherit ownership from their Library.

Ownership cannot be changed after publication.

---

# 4.12 Import

Import creates customer-owned objects.

Imported objects are disconnected from the source knowledge.

Subsequent changes to the Library never modify customer data automatically.

Updates require explicit synchronization.

---

# 4.13 Validation

Before publication every Version must satisfy:

No orphan Entities

No invalid Relations

No circular hierarchy (unless explicitly allowed)

No duplicate identifiers

No invalid translations

No broken references

Validation is mandatory.

---

# 4.14 Extensibility

The platform must allow:

new Entity Types

new Relation Types

new Relation Attributes

new Property Types

without structural redesign.

This requirement has higher priority than implementation simplicity.

---

# 4.15 Future Compatibility

The Logical Knowledge Model is intentionally compatible with:

Property Graphs

Knowledge Graphs

Semantic Networks

LLM Retrieval

Vector Search

AI Recommendation Engines

Future technologies should require implementation changes—not conceptual redesign.

---

End of Chapter 4

# 5. Semantic Model

## 5.1 Purpose

The Semantic Model defines the meaning of every concept used by the HR Competency Engine.

Its purpose is not to define storage.

Its purpose is not to define APIs.

Its purpose is to ensure that every concept has one—and only one—business meaning throughout the platform.

This semantic consistency is essential for interoperability, analytics, AI, reporting and future extensions.

The Semantic Model therefore acts as the canonical vocabulary of the platform.

---

# 5.2 Semantic Principles

The following principles govern the entire semantic architecture.

## Principle 1

One concept has one meaning.

Different providers may use different names.

Internally, every concept shall have one canonical meaning.

---

## Principle 2

Meaning is independent of language.

Translations never change semantics.

They only change presentation.

---

## Principle 3

Meaning is independent of implementation.

Databases,

APIs,

JSON,

Graph databases,

LLMs

must all represent exactly the same concept.

---

## Principle 4

Business meaning always has priority over technical convenience.

The platform shall never simplify a concept merely because implementation is easier.

---

# 5.3 Primitive Concepts

Primitive Concepts are concepts that cannot be derived from other concepts.

The platform recognizes the following primitives.

Occupation

Role

Competency

Task

Activity

Knowledge

Skill

Ability

Personal Attribute

Technology

Tool

Qualification

Certification

License

Education

Experience

Behavior Indicator

Collection

Classification

Context

Every other concept is derived from these primitives.

---

# 5.4 Derived Concepts

Derived Concepts are combinations of primitive concepts.

Examples include:

Role Profile

Competency Profile

Learning Path

Career Path

Assessment Profile

Succession Profile

Development Plan

These are business compositions rather than independent semantic concepts.

---

# 5.5 Competency

Definition

A Competency represents an observable capability required to perform work successfully.

A Competency is never directly measurable.

Only evidence of competency can be measured.

Competencies are realized through combinations of:

Knowledge

Skill

Ability

Personal Attribute

Therefore,

Competency is considered a composite semantic concept.

---

# 5.6 Knowledge

Definition

Knowledge represents information that an individual understands.

Knowledge answers:

"What does the person know?"

Examples:

Database Design

Accounting Standards

Python Syntax

Labor Law

Knowledge may be acquired through education or experience.

Knowledge alone does not imply successful performance.

---

# 5.7 Skill

Definition

A Skill represents learned proficiency in performing a task.

Skills answer:

"What can the person do?"

Examples:

Programming

Negotiation

Presentation

Problem Solving

Skills improve through deliberate practice.

Skills are observable.

Skills are measurable.

---

# 5.8 Ability

Definition

Ability represents relatively stable human capacity.

Abilities answer:

"What is the person capable of doing?"

Examples:

Logical Reasoning

Numerical Ability

Spatial Visualization

Working Memory

Abilities influence future skill acquisition.

Abilities are generally more stable than skills.

---

# 5.9 Personal Attribute

Definition

Personal Attributes describe enduring behavioral tendencies.

Examples:

Integrity

Adaptability

Initiative

Resilience

Customer Orientation

Leadership Orientation

Personal Attributes influence how work is performed.

They do not directly describe what work is performed.

---

# 5.10 Task

Definition

A Task is a discrete unit of work with a clear objective.

Tasks produce outcomes.

Tasks are observable.

Tasks may require multiple competencies.

---

# 5.11 Activity

Definition

Activities represent groups of related tasks.

Activities describe broader work processes.

Activities provide organizational context.

---

# 5.12 Occupation

Definition

An Occupation represents a recognized category of professional work.

Occupations define labor-market identities.

Occupations contain Roles.

Occupations are independent of organizations.

---

# 5.13 Role

Definition

A Role represents responsibilities performed within an organization.

Roles are organization-specific implementations of occupations.

Different organizations may define different Roles for the same Occupation.

---

# 5.14 Technology

Technology represents technical knowledge domains.

Examples:

Docker

Kubernetes

Oracle

Python

SAP

---

# 5.15 Tool

Tools are instruments used while performing work.

Examples:

Visual Studio Code

Jira

Git

Excel

SAP GUI

---

# 5.16 Qualification

Qualification represents formal recognition that predefined requirements have been satisfied.

Examples:

Bachelor Degree

Master Degree

Professional Diploma

---

# 5.17 Certification

Certification represents third-party verification of competence.

Examples:

AWS Certification

Oracle Certification

Cisco CCNA

---

# 5.18 Behavior Indicator

Behavior Indicators describe observable evidence that a competency is demonstrated.

Behavior Indicators are assessment-oriented concepts.

They are not competencies themselves.

---

# 5.19 Semantic Constraints

The following constraints are mandatory.

Knowledge is not Skill.

Skill is not Ability.

Ability is not Personality.

Technology is not Tool.

Task is not Activity.

Qualification is not Certification.

Behavior Indicator is not Competency.

Role is not Occupation.

---

# 5.20 Canonical Vocabulary

The definitions in this chapter override terminology differences introduced by external providers.

During import,

provider terminology shall be mapped to the canonical vocabulary.

The platform shall never expose provider-specific ambiguity to customer data.

---

End of Chapter 5

# 6. Capability Evidence Model

## 6.1 Purpose

The Capability Evidence Model defines how the platform represents evidence that supports the existence, level, or development of a person's capabilities.

The Knowledge Model defines **what capabilities are required**.

The Capability Evidence Model defines **how those capabilities can be demonstrated, assessed, or inferred**.

This chapter establishes the bridge between static knowledge and operational talent management processes such as recruitment, assessment, learning, certification, performance management, and succession planning.

---

## 6.2 Fundamental Principle

Capabilities themselves are not directly observable.

Only evidence of capabilities is observable.

The platform therefore distinguishes between:

- Capability (the construct)
- Evidence (the observable data)
- Evaluation (the interpretation of evidence)

This distinction is fundamental and shall be preserved throughout the platform.

---

## 6.3 Capability versus Evidence

A capability is a latent construct.

Examples:

- Python Programming
- Leadership
- Problem Solving
- Customer Orientation

None of these can be observed directly.

Instead, they are inferred from evidence.

Examples of evidence include:

- examination results
- work samples
- coding exercises
- interview ratings
- assessment center observations
- certifications
- project history
- supervisor observations

---

## 6.4 Evidence Types

The platform recognizes multiple categories of evidence.

### Examination

Evidence generated through written or computerized tests.

Typical use:

Knowledge

Some cognitive abilities

---

### Practical Assessment

Evidence generated through practical performance.

Typical use:

Technical skills

Operational skills

---

### Structured Interview

Evidence generated through standardized interviews.

Typical use:

Behavioral competencies

Leadership

Communication

---

### Assessment Center

Evidence generated through multiple standardized exercises observed by trained assessors.

Typical use:

Leadership

Management potential

Complex behavioral competencies

---

### Observation

Evidence collected during actual work.

Typical use:

Behavior

Safety

Customer interaction

Operational performance

---

### Portfolio

Evidence based on documented work products.

Examples:

Software projects

Research papers

Design portfolios

Publications

---

### Certification

Evidence provided by recognized certification bodies.

Examples:

AWS

Cisco

Oracle

Microsoft

---

### Education

Evidence based on formal educational achievement.

---

### Experience

Evidence based on documented work history.

Experience is considered supporting evidence rather than direct proof of competency.

---

## 6.5 Evidence Quality

Not all evidence has equal quality.

Each evidence type should be evaluated according to:

- validity
- reliability
- objectivity
- standardization
- relevance
- recency

The platform shall support recording these quality characteristics.

---

## 6.6 Assessment Method

Each capability may define one or more preferred assessment methods.

Example:

Knowledge

- Written Examination (60%)
- Oral Examination (20%)
- Interview (20%)

Skill

- Practical Assessment (70%)
- Portfolio Review (30%)

Ability

- Cognitive Test (70%)
- Assessment Center (30%)

Personal Attribute

- Personality Inventory (40%)
- Structured Interview (30%)
- Assessment Center (30%)

The weighting is configurable and belongs to the assessment strategy, not to the capability itself.

---

## 6.7 Evidence Lifecycle

Evidence progresses through the following lifecycle:

Draft

↓

Submitted

↓

Verified

↓

Accepted

↓

Expired

↓

Archived

Evidence may expire independently of the capability.

---

## 6.8 Traceability

Every evaluation shall be traceable to its underlying evidence.

The platform shall never allow capability levels to exist without supporting evidence.

---

## 6.9 Multiple Evidence Principle

A capability may be supported by multiple independent pieces of evidence.

No artificial limit shall exist.

The evaluation model is responsible for combining evidence according to organizational policy.

---

## 6.10 Future Compatibility

The Capability Evidence Model is intentionally designed to support:

- AI-assisted evaluation
- continuous competency assessment
- evidence-based career progression
- learning effectiveness analysis
- ISO 10015 training evaluation
- predictive workforce analytics

without conceptual redesign.

---

End of Chapter 6

# 7. Capability Evaluation Model

## 7.1 Purpose

The Capability Evaluation Model defines how the platform transforms evidence into trustworthy capability evaluations.

The Knowledge Model defines **what should exist**.

The Capability Evidence Model defines **what has been observed**.

The Capability Evaluation Model defines **how observed evidence is interpreted into organizational decisions**.

This model is the single decision engine of the HR Competency Engine.

Every module requiring competency-related decisions shall use this model.

Independent evaluation logic outside this model is prohibited.

---

# 7.2 Architectural Role

The Capability Evaluation Model is the central evaluation layer of the platform.

```

Knowledge Model

↓

Capability Evidence Model

↓

Capability Evaluation Model

↓

Business Modules

↓

Recruitment

Learning

Performance

Career

Succession

Compensation

AI

```

Business modules never calculate competency levels independently.

All evaluations are delegated to this model.

---

# 7.3 Evaluation Philosophy

Capabilities are not measured directly.

Capabilities are inferred.

Inference is based on:

- evidence quality
- assessment method
- evidence recency
- assessment reliability
- organizational policy

The platform therefore evaluates evidence—not assumptions.

---

# 7.4 Evaluation Object

The primary output of this model is an Evaluation.

An Evaluation represents the platform's current judgment regarding one capability.

An Evaluation is not evidence.

An Evaluation is not a competency.

An Evaluation is an interpretation.

---

# 7.5 Evaluation Components

Every Evaluation consists of the following logical components.

Capability

Evidence Set

Evaluation Strategy

Evaluation Result

Confidence

Timestamp

Validity Period

Reviewer (optional)

Explanation

Each component contributes to the final decision.

---

# 7.6 Evaluation Strategy

Organizations may define different evaluation strategies.

Examples:

Weighted Average

Highest Evidence

Most Recent Evidence

Minimum Threshold

Composite Formula

Rule-Based Evaluation

AI-Assisted Evaluation

The strategy belongs to the organization—not to the capability.

---

# 7.7 Evidence Weighting

Evidence does not contribute equally.

Each evidence item may define:

Weight

Reliability

Validity

Recency

Importance

Example:

Coding Test

Weight = 40%

Work Sample

Weight = 35%

Interview

Weight = 15%

Certification

Weight = 10%

Organizations may configure weighting policies.

---

# 7.8 Confidence

Every Evaluation shall include a Confidence Score.

Confidence represents the degree of trust in the evaluation—not the capability level itself.

Example:

Python Skill

Level = Advanced

Confidence = High

A low-confidence evaluation should trigger additional assessment.

---

# 7.9 Evidence Aging

Evidence loses predictive value over time.

The platform therefore supports evidence aging.

Examples:

Certification

Valid for three years

Programming Assessment

Valid for two years

Safety Training

Valid for one year

Organizations define aging policies.

Expired evidence contributes less—or not at all—to future evaluations.

---

# 7.10 Missing Evidence

Absence of evidence is not evidence of absence.

The platform distinguishes:

No Evidence

Insufficient Evidence

Conflicting Evidence

Expired Evidence

Low Quality Evidence

Each state requires different organizational actions.

---

# 7.11 Explainability

Every Evaluation must be explainable.

The platform shall always answer:

Why was this capability assigned this level?

The explanation shall include:

Evidence used

Evidence ignored

Evaluation strategy

Applied rules

Confidence

This requirement also applies to AI-generated evaluations.

---

# 7.12 Human Override

Organizations may override automated evaluations.

Overrides require:

Reason

Reviewer

Timestamp

Approval (optional)

Original evaluation remains preserved.

---

# 7.13 Business Decisions

Business modules never evaluate capabilities directly.

Instead, they consume Evaluation Results.

Examples:

Recruitment

Uses Evaluation

to compare candidate capabilities against job requirements.

Learning

Uses Evaluation

to identify development gaps.

Performance

Uses Evaluation

to monitor competency growth.

Succession

Uses Evaluation

to identify readiness.

Career

Uses Evaluation

to recommend progression.

Compensation

Uses Evaluation

as one input to reward policies.

AI Advisor

Uses Evaluation

to generate recommendations.

---

# 7.14 Capability Gap

Capability Gap is calculated as:

Required Capability

minus

Evaluated Capability

Gap itself is not evidence.

Gap is an analytical result.

Gap may trigger:

Learning

Coaching

Recruitment

Promotion Delay

Certification

Mentoring

---

# 7.15 Readiness

Readiness represents organizational confidence that a person can successfully perform a future role.

Readiness is derived from:

Capability Evaluations

Experience

Performance

Potential

Organizational Rules

Readiness is therefore a higher-level concept than competency.

---

# 7.16 Evaluation History

Evaluations are never overwritten.

Every evaluation becomes part of organizational history.

Historical evaluations enable:

Growth analysis

Trend analysis

Learning effectiveness

Career analytics

Predictive AI

---

# 7.17 AI Compatibility

AI services never bypass the Capability Evaluation Model.

AI may:

recommend

predict

estimate

prioritize

explain

AI may not redefine business semantics.

All AI outputs become candidate evaluations until validated according to organizational policy.

---

# 7.18 Canonical Decision Engine

The Capability Evaluation Model is the only canonical evaluation engine within the HR Competency Engine.

Every competency-related decision across all modules shall be traceable to this model.

This guarantees consistency, explainability, auditability and future extensibility.

---

End of Chapter 7

# 8. Organizational Decision Model

## 8.1 Purpose

The Organizational Decision Model defines how capability evaluations are transformed into business decisions.

Knowledge defines organizational expectations.

Evidence represents observations.

Evaluation produces trusted judgments.

Decision determines organizational actions.

This chapter establishes a single decision framework shared by all business modules.

No module shall implement independent competency-related decision logic.

---

# 8.2 Decision Philosophy

Evaluations describe people.

Decisions affect organizations.

These concepts must remain independent.

The same Evaluation may lead to different Decisions depending on organizational policy.

Example:

Evaluation

Python = Advanced

Organization A

Decision

Eligible for promotion

Organization B

Decision

Eligible only after leadership training

The Evaluation remains identical.

Only the Decision changes.

---

# 8.3 Separation of Concerns

The platform separates:

Facts

↓

Evidence

↓

Interpretation

↓

Evaluation

↓

Policy

↓

Decision

Policies are organizational assets.

Policies are not embedded in evaluations.

---

# 8.4 Decision Context

Every Decision occurs within a business context.

Typical contexts include:

Recruitment

Learning

Performance

Promotion

Career Progression

Succession

Certification

Compensation

Talent Review

Workforce Planning

AI Recommendation

The same capability may be evaluated differently depending on context.

---

# 8.5 Decision Policy

A Decision Policy defines the organizational rules used to transform evaluations into decisions.

Examples:

Promotion Policy

Recruitment Policy

Leadership Policy

Training Policy

Compensation Policy

Policies are configurable.

Policies never modify evaluation results.

---

# 8.6 Decision Inputs

A Decision may consume one or more inputs.

Examples:

Capability Evaluation

Experience

Performance Rating

Potential Rating

Education

Certification

Business Rules

Organizational Constraints

Availability

Risk

Decision inputs are extensible.

---

# 8.7 Decision Outputs

A Decision produces one or more outcomes.

Examples:

Hire

Reject

Promote

Assign Learning Path

Nominate Successor

Recommend Coach

Increase Compensation

Require Certification

Create Development Plan

The platform records decisions independently from actions.

---

# 8.8 Explainability

Every Decision shall be explainable.

The platform must answer:

Why was this decision made?

The explanation includes:

Decision Policy

Evaluations

Business Rules

Thresholds

Exceptions

Human Overrides

Explainability is mandatory.

---

# 8.9 Human Authority

Organizational Decisions remain human-owned.

Automation supports decisions.

Automation does not replace accountability.

Human approval may be required according to policy.

---

# 8.10 AI Decision Support

Artificial Intelligence may:

recommend

prioritize

predict

simulate

summarize

Artificial Intelligence shall never become the authoritative decision maker.

AI outputs are recommendations.

Organizational policy determines final decisions.

---

# 8.11 Decision History

Decisions are immutable historical records.

Corrections create new Decisions.

Historical Decisions support:

Auditing

Analytics

Compliance

AI Learning

Organizational Knowledge

---

# 8.12 Canonical Decision Layer

The Organizational Decision Model is the only authorized business decision framework of the platform.

All HR modules consume this layer.

No HR module owns independent competency decision logic.

---

End of Chapter 8

