# Data Dictionary

## Table: CareerLevel

### Business Purpose
سطوح رشد شغلی هر Framework را تعریف می‌کند.

### Columns

| Field | Type | Required | Description |
|------|------|----------|-------------|
| ID | int | Yes | شناسه |
| CareerFrameworkID | int | Yes | کلید خارجی |
| Code | nvarchar(30) | Yes | کد سطح |
| Name | nvarchar(100) | Yes | عنوان سطح |
| Description | nvarchar(2000) | No | توضیحات |
| LevelOrder | int | Yes | ترتیب |
| IsActive | bit | Yes | فعال |

### Sample Records

| Framework | Code | Name | Order |
|-----------|------|------|------:|
| TECH | L1 | Junior | 1 |
| TECH | L2 | Mid | 2 |
| TECH | L3 | Senior | 3 |
| TECH | L4 | Lead | 4 |
| TECH | L5 | Architect | 5 |
| MGMT | M1 | Supervisor | 1 |
| MGMT | M2 | Manager | 2 |
| MGMT | M3 | Senior Manager | 3 |
| MGMT | M4 | Director | 4 |
| MGMT | M5 | Vice President | 5 |


### Relationships

```text
CareerFramework
1 -------- N CareerLevel
```

### Business Rules

- Code در هر Framework یکتا باشد.
- LevelOrder در هر Framework یکتا باشد.
