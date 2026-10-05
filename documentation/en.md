# g:GOSt: Gene Ontology enrichment

Human; up to 100 gene symbols; GO:BP, GO:MF and GO:CC sources. Annotated background or up to 1,000 custom background genes. P values use the selected multiple testing correction. KEGG and TRANSFAC are excluded.

## Scope

Computational research analysis. It does not establish diagnosis, pathogenicity, efficacy or treatment. Check population, provenance, version and scope before interpreting.

Interface and contracts implemented on ELUCENIA. Analysis depends on the responsible service being available. Independent clinical review and professional language review are incomplete.

## Query

- Gene symbols
- Sources
- Background gene set
- Significance threshold
- Multiple testing correction
- Exclude electronic annotations
- I confirm that I will submit only public or synthetic research data, without patient or confidential data.

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

Official term names and scientific identifiers retain the source language; interface labels are translated.

## Results

- Term identifier
- Official term name
- Source
- Adjusted p value
- Overlapping genes
- Query genes
- Term genes
- Reference universe
- Precision
- Recall
- Gene mapping
- Unrecognized genes

Export preserves sources, attribution, versions and limitations. Source data retain their license.

## Version

`g:Profiler e114_eg62_p19_27110d83 · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## Sources

The g:Profiler API permits academic and non-academic use. Gene Ontology data use CC BY 4.0: preserve attribution, release and DOI. KEGG and TRANSFAC are not queried.

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## Waiting limits

Each request to this provider has a 20-second limit. The complete workflow has a 120-second limit; the interface waits at most 125 seconds. Requests share the workflow’s remaining time. There is no automatic retry. If the provider does not respond in time, analysis ends with an explicit error; no result is estimated or substituted.
