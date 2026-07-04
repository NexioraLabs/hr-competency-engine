# Knowledge Model

See conversation-derived specification.

## Vision
Provider-agnostic, versioned knowledge platform.

## Core entities
- KnowledgeProvider
- KnowledgeLibrary
- KnowledgeVersion
- KnowledgeEntityType
- CompetencyCategory
- KnowledgeEntity
- KnowledgeRelationType
- KnowledgeRelation
- KnowledgeRelationAttribute
- KnowledgeProperty
- KnowledgePropertyValue
- KnowledgeCollection
- KnowledgeCollectionMember
- KnowledgeTranslation
- ImportLog

## Rules
- Provider->Library->Version->Entity
- Entity graph via Relation only.
- Relation metadata stored in RelationAttribute.
- Customer data imported, never directly references provider.

## Validated against
- OaSIS
- O*NET
- ESCO
