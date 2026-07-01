# STYLE_GUIDE.md

# HR Competency Engine - Design Style Guide

Version: 1.0

## هدف
این سند قوانین طراحی مدل داده و مستندسازی پروژه را مشخص می‌کند تا تمام موجودیت‌ها با یک استاندارد واحد طراحی شوند.

---

## 1. اصول کلی

- هر جدول فقط یک مسئولیت (Single Responsibility) داشته باشد.
- ابتدا مدل مفهومی طراحی شود، سپس مدل فیزیکی.
- از طراحی قابل توسعه استفاده شود.
- از تکرار اطلاعات غیرضروری جلوگیری شود.

---

## 2. نام‌گذاری

### Tables
- PascalCase
- اسم مفرد

مثال:
- CareerFramework
- CareerLevel
- JobFamily
- Role

### Columns
- PascalCase
- کلید اصلی: ID
- کلید خارجی: <TableName>ID

### Boolean
همیشه با Is شروع شوند.
مثال:
- IsActive
- IsDefault

---

## 3. نوع داده‌ها

| مفهوم | نوع پیشنهادی |
|--------|--------------|
| ID | bigint |
| Code | nvarchar(50) |
| Name | nvarchar(200) |
| Description | nvarchar(2000) |
| DisplayOrder | integer |
| IsActive | boolean |

---

## 4. ساختار مستندات هر جدول

1. Business Purpose
2. Columns
3. Sample Data
4. Relationships
5. Business Rules
6. Future Notes

---

## 5. روابط

برای هر رابطه موارد زیر مشخص شود:

- Parent
- Child
- Cardinality (1:1 / 1:N / N:M)

---

## 6. قوانین کسب‌وکار

فقط قوانین مهم ثبت شوند.

---

## 7. زبان

- نام جدول‌ها: English
- نام فیلدها: English
- توضیحات: فارسی
- مثال‌ها: English

---

## 8. تغییرات

- تغییرات مهم در CHANGELOG.md ثبت شوند.
- تصمیم‌های معماری در docs/decisions ثبت شوند.

---

## 9. اصل سادگی

از طراحی بیش از حد پیچیده خودداری شود.

---

## 10. اصل توسعه‌پذیری

ساختار باید امکان افزودن قابلیت‌های آینده را بدون شکستن مدل فعلی فراهم کند.

---

## 11. اصل استقلال

موجودیت‌ها تا حد امکان مستقل طراحی شوند.

---

## 12. اصل سازگاری

در کل پروژه از واژگان، نام‌گذاری و الگوی یکسان استفاده شود.
