# Data Dictionary

## Table: Role

### Business Purpose
نقش‌های شغلی سازمان را تعریف می‌کند.

### Columns

| Field | Type | Required | Description |
|------|------|----------|-------------|
| ID | bigint | Yes | شناسه |
| JobFamilyID | bigint | Yes | کلید خارجی |
| CareerFrameworkID | bigint | Yes | کلید خارجی |
| Code | nvarchar(50) | Yes | کد |
| Name | nvarchar(200) | Yes | عنوان نقش |
| Description | nvarchar(2000) | No | توضیحات |
| IsActive | bit | Yes | فعال |
| DisplayOrder | int | No | ترتیب |

### Sample Records

| Job Family | Framework | Code | Name |
|------------|-----------|------|------|
| Software Engineering | TECH | PYDEV | Python Developer |
| Software Engineering | TECH | NETDEV | .NET Developer |
| HR | MGMT | HRSPEC | HR Specialist |
| HR | MGMT | HRMGR | HR Manager |
| Sales | SALES | SALESREP | Sales Representative |

### Relationships

```text
JobFamily
1 -------- N Role

CareerFramework
1 -------- N Role
```

### Business Rules

- هر Role متعلق به یک JobFamily است.
- هر Role از یک CareerFramework استفاده می‌کند.
- Code یکتا باشد.
