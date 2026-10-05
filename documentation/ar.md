# g:GOSt: الإثراء في Gene Ontology

الإنسان؛ حتى 100 رمز جين؛ مصادر GO:BP وGO:MF وGO:CC. خلفية مشروحة أو حتى 1,000 جين خلفية مخصصة. تُصحّح قيم p بالطريقة المختارة. لا يُستخدم KEGG أو TRANSFAC.

## النطاق

تحليل حاسوبي لأغراض البحث. لا يحدد التشخيص أو الإمراضية أو الفعالية أو العلاج. تحقّق من المجموعة والمصدر والإصدار والنطاق قبل التفسير.

تم تنفيذ الواجهة وعقود الطلب والاستجابة داخل ELUCENIA. يعتمد التحليل على توفر الخدمة المسؤولة. لم تكتمل المراجعة السريرية المستقلة ولا المراجعة اللغوية المهنية.

## الاستعلام

- رموز الجينات
- المصادر
- مجموعة جينات الخلفية
- عتبة الدلالة
- تصحيح الاختبارات المتعددة
- استبعاد التعليقات الإلكترونية
- أؤكد أنني سأرسل بيانات بحثية عامة أو اصطناعية فقط، دون بيانات مرضى أو معلومات سرية.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "genes": {
      "type": "array",
      "items": {
        "type": "string",
        "pattern": "^[A-Za-z0-9][A-Za-z0-9.-]{0,31}$"
      },
      "minItems": 1,
      "maxItems": 100,
      "uniqueItems": true
    },
    "sources": {
      "type": "array",
      "minItems": 1,
      "maxItems": 3,
      "uniqueItems": true,
      "items": {
        "enum": [
          "GO:BP",
          "GO:MF",
          "GO:CC"
        ]
      }
    },
    "threshold": {
      "type": "number",
      "exclusiveMinimum": 0,
      "maximum": 1
    },
    "correction": {
      "enum": [
        "g_SCS",
        "bonferroni",
        "fdr"
      ]
    },
    "excludeElectronic": {
      "type": "boolean"
    },
    "background": {
      "type": "array",
      "items": {
        "type": "string",
        "pattern": "^[A-Za-z0-9][A-Za-z0-9.-]{0,31}$"
      },
      "minItems": 1,
      "maxItems": 1000,
      "uniqueItems": true
    },
    "publicResearchData": {
      "const": true,
      "description": "Only public or synthetic research inputs; no patient/confidential data."
    }
  },
  "required": [
    "genes",
    "sources",
    "threshold",
    "correction",
    "excludeElectronic",
    "publicResearchData"
  ],
  "additionalProperties": false
}
```

تُحفظ الأسماء الرسمية للمصطلحات والمعرّفات العلمية بلغة المصدر؛ تسميات الواجهة مترجمة.

## النتائج

- معرّف المصطلح
- الاسم الرسمي للمصطلح
- المصدر
- قيمة p المصحّحة
- الجينات المشتركة
- جينات الاستعلام
- جينات المصطلح
- مجموعة المرجع الإحصائية
- الدقة
- الاسترجاع
- مطابقة الجينات
- الجينات غير المعروفة

يحفظ التصدير المصادر والنسب والإصدارات والحدود. تحتفظ البيانات الأصلية بترخيصها.

## الإصدار

`g:Profiler e114_eg62_p19_27110d83 · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## المصادر

تسمح واجهة g:Profiler بالاستخدام الأكاديمي وغير الأكاديمي. تخضع بيانات Gene Ontology لترخيص CC BY 4.0؛ يجب الحفاظ على النسب والإصدار وDOI. لا يُستعلم عن KEGG أو TRANSFAC.

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## حدود الانتظار

الحد الزمني لكل طلب إلى هذا المزوّد هو 20 ثانية. الحد الزمني لسير العمل الكامل هو 120 ثانية، وتنتظر الواجهة 125 ثانية كحد أقصى. تتشارك الطلبات الوقت المتبقي لسير العمل. لا توجد إعادة محاولة تلقائية. إذا لم يستجب المزوّد في الوقت المحدد، ينتهي التحليل بخطأ صريح؛ ولا تُقدَّر أي نتيجة ولا تُستبدل.
