# Reference Model

**Version:** 1.0

**Status:** Draft

---

# 1. Purpose

Reference Model لایه‌ای مستقل از داده‌های مشتری است که امکان نگهداری، نسخه‌بندی و مدیریت بانک‌های اطلاعاتی استاندارد منابع انسانی را فراهم می‌کند.

هدف این مدل، پشتیبانی از منابع مختلف مانند:

* OaSIS (Canada)
* O*NET (USA)
* ESCO (Europe)
* SFIA
* APQC
* Customer Libraries

بدون وابستگی به ساختار داخلی هر یک از آن‌ها است.

این لایه تنها مرجع نگهداری اطلاعات استاندارد بوده و هیچ‌یک از داده‌های آن مستقیماً در فرآیندهای عملیاتی مشتری استفاده نمی‌شود.

---

# 2. Design Principles

این مدل بر اساس اصول زیر طراحی شده است:

1. استقلال کامل از مدل داده مشتری
2. پشتیبانی از چندین Provider
3. پشتیبانی از نسخه‌های مختلف هر Library
4. قابلیت Import انتخابی اطلاعات
5. عدم وابستگی به استاندارد خاص
6. توسعه‌پذیری بدون تغییر ساختار اصلی
7. استفاده از Meta Model به جای طراحی اختصاصی برای هر استاندارد

---

# 3. High Level Architecture

```
Reference Provider
        │
Reference Library
        │
Reference Version
        │
Reference Entity
        │
Reference Relation
        │
Import Engine
        │
Customer Core
```

---

# 4. Core Entities

## ReferenceProvider

نماینده تولیدکننده یا مالک بانک اطلاعاتی.

نمونه‌ها:

* OaSIS
* O*NET
* ESCO
* SFIA
* APQC
* Customer

---

## ReferenceLibrary

هر Provider می‌تواند یک یا چند Library منتشر کند.

نمونه:

* IT Occupations
* Healthcare
* Generic Competencies

---

## ReferenceVersion

هر Library دارای نسخه‌های مختلف است.

نمونه:

* 2025
* 2026
* Version 31.0

---

## ReferenceEntityType

نوع هر موجودیت را مشخص می‌کند.

نمونه‌ها:

* Role
* Task
* Competency
* Behavior
* Level
* Knowledge
* Skill
* Ability
* Personal Attribute
* Work Activity
* Work Context
* Tool
* Certification

در آینده امکان افزودن انواع جدید بدون تغییر مدل وجود دارد.

---

## ReferenceEntity

تمام عناصر موجود در Library صرف‌نظر از نوع آن‌ها در این موجودیت ذخیره می‌شوند.

نمونه‌ها:

* Python Developer
* Leadership
* Programming
* Analyze Requirements
* REST API
* Level 4

---

## ReferenceRelationType

نوع ارتباط بین دو Entity را مشخص می‌کند.

نمونه:

* Requires
* HasTask
* Contains
* RelatedTo
* ParentOf
* ChildOf
* Prerequisite

---

## ReferenceRelation

تمام ارتباطات بین Entityها در این جدول نگهداری می‌شوند.

نمونه‌ها:

Role → Requires → Competency

Role → HasTask → Task

Competency → Contains → Behavior

Task → Requires → Competency

---

## ReferenceProperty

تعریف ویژگی‌های اختصاصی هر نوع Entity.

نمونه:

ISCO Code

Criticality

Importance

Difficulty

---

## ReferencePropertyValue

مقدار ویژگی‌های هر Entity.

---

## ReferenceTag

برچسب‌های موضوعی برای دسته‌بندی و جستجو.

---

## ReferenceEntityTag

ارتباط بین Entityها و Tagها.

---

## ReferenceImportLog

ثبت عملیات Import به سیستم مشتری.

---

# 5. Architecture Rules

* هر Entity دقیقاً متعلق به یک Version است.
* هر Version متعلق به یک Library است.
* هر Library متعلق به یک Provider است.
* تمام ارتباطات فقط از طریق ReferenceRelation برقرار می‌شوند.
* هیچ ارتباط مستقیمی بین Reference Model و جداول عملیاتی مشتری وجود ندارد.
* انتقال اطلاعات به Core فقط از طریق Import Engine انجام می‌شود.
* حذف یا ویرایش داده‌های Reference نباید اطلاعات مشتری را تغییر دهد.

---

# 6. Out of Scope

در نسخه 1.0 موارد زیر خارج از محدوده هستند:

* Semantic Mapping
* Canonical Entity
* AI Matching
* Cross Provider Synchronization
* Automatic Merge Between Libraries

این قابلیت‌ها در نسخه‌های آینده بررسی خواهند شد.

---

# 7. Import Strategy

کاربر می‌تواند:

* یک Provider انتخاب کند.
* یک Library انتخاب کند.
* یک Version انتخاب کند.
* فقط Entityهای مورد نیاز را انتخاب کند.
* اطلاعات انتخاب‌شده را به جداول Core منتقل کند.

Reference Model هیچ وابستگی مستقیمی به ساختار Core ندارد.

---

# 8. Future Architecture

در نسخه‌های آینده قابلیت‌های زیر قابل اضافه شدن هستند:

* Canonical Entity
* Knowledge Graph
* AI-Based Mapping
* Cross Library Comparison
* Library Marketplace
* Automatic Update Engine

این قابلیت‌ها بدون نیاز به بازطراحی ساختار اصلی قابل پیاده‌سازی خواهند بود.
