# Data Cleaning & Transformation / تنظيف وتحويل البيانات

## العربية

تم استخدام **Power Query** لتنظيف وتحويل الجداول الرسمية التالية:
- Table 21 — Online Selling
- Table 23 — Online Purchasing
- Table 25 — Cloud Computing
- Table 27 — IoT by Purpose

### الجداول 21 و23 و25
تم تطبيق الخطوات التالية:
1. إزالة أول 9 صفوف غير تحليلية.
2. استخدام الصف الأول المتبقي كعناوين للأعمدة.
3. الاحتفاظ فقط بـ `Economic Activity` وعمود النسبة `%`.
4. إعادة تسمية عمود النسبة حسب المؤشر:
   - `Online Selling %`
   - `Online Purchasing %`
   - `Cloud Computing %`
5. إزالة الصفوف:
   - null / blank
   - Total
   - Source
6. ضبط `Economic Activity` كـ Text.
7. ضبط النسبة كـ Decimal Number.
8. إعادة تسمية الـQueries بأسماء واضحة.

### جدول 27 — IoT
الخطوات:
1. إزالة أول 9 صفوف.
2. ترقية صف العناوين.
3. إزالة صف الترجمة الإضافي بعد استخدامه للتحقق من معنى الأعمدة.
4. الاحتفاظ بـ:
   - Economic Activity
   - Energy Consumption Management
   - Building Security
   - Maintenance
   - Customer Service
5. إزالة Total وSource والصفوف الفارغة.
6. تحويل الجدول من Wide إلى Long باستخدام **Unpivot Other Columns**.
7. إعادة تسمية:
   - Attribute → `IoT Purpose`
   - Value → `IoT Usage %`
8. توحيد أسماء أغراض IoT باللغة الإنجليزية.
9. الناتج النهائي: 72 صفًا = 18 نشاطًا × 4 أغراض.

---

## English

**Power Query** was used to clean and transform the following official tables:
- Table 21 — Online Selling
- Table 23 — Online Purchasing
- Table 25 — Cloud Computing
- Table 27 — IoT by Purpose

### Tables 21, 23 and 25
Transformation steps:
1. Removed the first 9 non-analytical rows.
2. Promoted the first remaining row to headers.
3. Retained only `Economic Activity` and the percentage column.
4. Renamed the percentage field to:
   - `Online Selling %`
   - `Online Purchasing %`
   - `Cloud Computing %`
5. Removed null, blank, Total, and Source rows.
6. Set `Economic Activity` to Text.
7. Set percentage fields to Decimal Number.
8. Renamed Power Query queries using descriptive names.

### Table 27 — IoT
Transformation steps:
1. Removed the first 9 rows.
2. Promoted headers.
3. Removed the additional translation row after confirming the English purpose labels.
4. Retained:
   - Economic Activity
   - Energy Consumption Management
   - Building Security
   - Maintenance
   - Customer Service
5. Removed blank, Total, and Source rows.
6. Converted the table from wide to long format using **Unpivot Other Columns**.
7. Renamed:
   - Attribute → `IoT Purpose`
   - Value → `IoT Usage %`
8. Standardized IoT purpose labels in English.
9. Final result: 72 rows = 18 activities × 4 purposes.
