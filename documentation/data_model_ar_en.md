# Data Model / نموذج البيانات

## العربية
تم إنشاء جدول مشترك باسم:

`Economic Activities`

باستخدام DAX لتجميع قائمة فريدة من الأنشطة الاقتصادية المستخدمة في الجداول الأربعة.

### العلاقات
- Economic Activities → Online Selling
- Economic Activities → Online Purchasing
- Economic Activities → Cloud Computing
- Economic Activities → IoT Usage by Purpose

جدول IoT يحتوي على عدة صفوف لكل نشاط اقتصادي بسبب وجود 4 أغراض مختلفة، ولذلك علاقته من نوع One-to-Many.

أما الجداول الثلاثة الأخرى فتحتوي على صف واحد لكل نشاط اقتصادي.

### لماذا أنشأنا Dimension مشترك؟
لتجنب ربط جداول المؤشرات ببعضها مباشرة، وتوفير Slicer واحد موحد للنشاط الاقتصادي يعمل على كل الـvisuals.

---

## English
A shared dimension table named:

`Economic Activities`

was created using DAX to provide a unique list of economic activities shared across the analytical tables.

### Relationships
- Economic Activities → Online Selling
- Economic Activities → Online Purchasing
- Economic Activities → Cloud Computing
- Economic Activities → IoT Usage by Purpose

The IoT table contains four records per economic activity, producing a one-to-many relationship.

The other three indicator tables contain one record per economic activity.

### Why use a shared dimension?
The dimension provides a consistent sector filter across the entire report and avoids direct fact-to-fact relationships.
