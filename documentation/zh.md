# g:GOSt：Gene Ontology 富集分析

人类；最多 100 个基因符号；来源为 GO:BP、GO:MF 和 GO:CC。使用已注释背景或最多 1,000 个自定义背景基因。p 值采用所选多重检验校正。不使用 KEGG 或 TRANSFAC。

## 适用范围

用于研究的计算分析。不能据此确定诊断、致病性、疗效或治疗。解释前请核对人群、来源、版本与适用范围。

ELUCENIA已实现界面及请求和响应契约。分析依赖相应服务的可用性。独立临床审核和专业语言审核尚未完成。

## 查询

- 基因符号
- 来源
- 背景基因集
- 显著性阈值
- 多重检验校正
- 排除电子注释
- 我确认仅提交公开或合成研究数据，不含患者数据或保密信息。

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

官方术语名称和科学标识符保留来源语言；界面标签已翻译。

## 结果

- 术语标识符
- 官方术语名称
- 来源
- 校正后的 p 值
- 重叠基因数
- 查询基因数
- 术语基因数
- 参考总体
- 精确率
- 召回率
- 基因映射
- 未识别的基因

导出保留来源、署名、版本和限制。原始数据保留其许可证。

## 版本

`g:Profiler e114_eg62_p19_* · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## 来源

g:Profiler API允许学术和非学术使用。Gene Ontology数据采用CC BY 4.0：请保留署名、发布版本和DOI。不查询KEGG或TRANSFAC。

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## 等待时限

向此服务提供方发送的每个请求限时 20 秒。整个工作流程限时 120 秒，界面最多等待 125 秒。各请求共享工作流程的剩余时间。不会自动重试。如果服务提供方未及时响应，分析将以明确的错误结束；不会估算或替换任何结果。
