# Data Dictionary


## Table: JobFamily

### Business Purpose
خانواده‌های شغلی سازمان را تعریف می‌کند.

### Columns

| Field | Type | Required | Description |
|------|------|----------|-------------|
| ID | bigint | Yes | شناسه |
| Code | nvarchar(50) | Yes | کد |
| Name | nvarchar(200) | Yes | نام |
| Description | nvarchar(1000) | No | توضیحات |
| IsActive | bit | Yes | فعال |
| DisplayOrder | int | No | ترتیب |

### Sample Records

| Code | Name |
|------|------|
| SE | Software Engineering |
| QA | Quality Assurance |
| HR | Human Resources |
| FIN | Finance |
| SALES | Sales |

### Relationships

```text
JobFamily
1 -------- N Role
```

### Business Rules

- Code یکتا باشد.
