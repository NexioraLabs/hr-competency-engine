---
Entity: CareerFramework
Entity ID: ENT-001
Status: Draft
Version: 1.0
Last Updated: 2026-07-04
Owner: NexioraLabs
---

# Data Dictionary

## Table: CareerFramework

### Business Purpose
این جدول چارچوب مسیرهای شغلی (Career Ladder) را تعریف می‌کند.

### Columns

| Field | Type | Required | Description |
|------|------|----------|-------------|
| ID | int | Yes | شناسه یکتا |
| Code | nvarchar(50) | Yes | کد یکتا |
| Name | nvarchar(200) | Yes | نام چارچوب |
| Description | nvarchar(2000) | No | توضیحات |
| IsDefault | bit | Yes | چارچوب پیش‌فرض سازمان |
| IsActive | bit | Yes | فعال / غیرفعال |
| DisplayOrder | int | No | ترتیب نمایش |

### Sample Records

| Code | Name |
|------|------|
| TECH | مسیر شغلی فنی |
| MGMT | مسیر شغلی مدیریتی |
| SALES | مسیر شغلی فروش |

### Relationships

```text
CareerFramework
1 -------- N CareerLevel
```

### Business Rules

- Code باید یکتا باشد.
- هر Framework حداقل یک Career Level دارد.
- فقط یک Framework می‌تواند پیش‌فرض باشد.
