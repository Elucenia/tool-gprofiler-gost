# g:GOSt: Gene Ontology संवर्धन

मानव; अधिकतम 100 जीन प्रतीक; स्रोत GO:BP, GO:MF और GO:CC। एनोटेटेड पृष्ठभूमि या अधिकतम 1,000 कस्टम पृष्ठभूमि जीन। p मान चुने गए बहु-परीक्षण समायोजन से सुधारे जाते हैं। KEGG और TRANSFAC उपयोग नहीं होते।

## दायरा

अनुसंधान के लिए संगणकीय विश्लेषण। यह निदान, रोगजनकता, प्रभावकारिता या उपचार निर्धारित नहीं करता। व्याख्या से पहले जनसमूह, स्रोत, संस्करण और दायरा जाँचें।

ELUCENIA में इंटरफ़ेस और अनुरोध तथा प्रतिक्रिया अनुबंध लागू हैं। विश्लेषण संबंधित सेवा की उपलब्धता पर निर्भर है। स्वतंत्र नैदानिक समीक्षा और पेशेवर भाषा समीक्षा पूरी नहीं हुई हैं।

## प्रश्न

- जीन प्रतीक
- स्रोत
- पृष्ठभूमि जीन समूह
- सांख्यिकीय महत्व की सीमा
- बहु-परीक्षण समायोजन
- इलेक्ट्रॉनिक टिप्पणियाँ हटाएँ
- मैं पुष्टि करता हूँ कि केवल सार्वजनिक या कृत्रिम अनुसंधान डेटा भेजूँगा, जिसमें रोगी या गोपनीय डेटा नहीं होगा।

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

आधिकारिक शब्द-नाम और वैज्ञानिक पहचानकर्ता स्रोत की भाषा में सुरक्षित रहते हैं; इंटरफ़ेस के लेबल अनूदित हैं।

## परिणाम

- शब्द पहचानकर्ता
- आधिकारिक शब्द-नाम
- स्रोत
- समायोजित p मान
- समान जीन
- प्रश्न के जीन
- शब्द के जीन
- संदर्भ समष्टि
- परिशुद्धता
- पुनर्प्राप्ति
- जीन मिलान
- अपरिचित जीन

निर्यात में स्रोत, श्रेय, संस्करण और सीमाएँ सुरक्षित रहते हैं। मूल डेटा का लाइसेंस बना रहता है।

## संस्करण

`g:Profiler e114_eg62_p19_* · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## स्रोत

g:Profiler API अकादमिक और गैर-अकादमिक उपयोग की अनुमति देती है। Gene Ontology डेटा CC BY 4.0 के अंतर्गत है; श्रेय, संस्करण और DOI बनाए रखें। KEGG और TRANSFAC से पूछताछ नहीं की जाती।

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## प्रतीक्षा की समय-सीमाएँ

इस प्रदाता को भेजे गए हर अनुरोध की सीमा 20 सेकंड है। पूरी कार्यप्रक्रिया की सीमा 120 सेकंड है; इंटरफ़ेस अधिकतम 125 सेकंड प्रतीक्षा करता है। सभी अनुरोध कार्यप्रक्रिया का बचा हुआ समय साझा करते हैं। अपने-आप दोबारा प्रयास नहीं किया जाता। यदि प्रदाता समय पर जवाब नहीं देता, तो विश्लेषण स्पष्ट त्रुटि के साथ समाप्त होता है; किसी परिणाम का अनुमान नहीं लगाया जाता और न ही कोई वैकल्पिक परिणाम दिया जाता।
