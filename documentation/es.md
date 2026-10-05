# g:GOSt: enriquecimiento en Gene Ontology

Humanos; hasta 100 símbolos de genes; fuentes GO:BP, GO:MF y GO:CC. Fondo anotado o hasta 1.000 genes de fondo personalizado. Los valores p usan la corrección seleccionada. Se excluyen KEGG y TRANSFAC.

## Alcance

Análisis computacional para investigación. No establece diagnóstico, patogenicidad, eficacia ni tratamiento. Revise población, fuente, versión y alcance antes de interpretar.

Interfaz y contratos implementados en ELUCENIA. El análisis depende de la disponibilidad del servicio responsable. No se han completado la revisión clínica independiente ni la revisión lingüística profesional.

## Consulta

- Símbolos de genes
- Fuentes
- Conjunto de genes de fondo
- Umbral de significación
- Corrección por pruebas múltiples
- Excluir anotaciones electrónicas
- Confirmo que enviaré solo datos públicos o sintéticos de investigación, sin datos de pacientes ni información confidencial.

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

Los nombres oficiales de términos e identificadores científicos conservan el idioma de la fuente; las etiquetas de interfaz están traducidas.

## Resultados

- Identificador del término
- Nombre oficial del término
- Fuente
- Valor p ajustado
- Genes coincidentes
- Genes consultados
- Genes del término
- Universo de referencia
- Precisión
- Exhaustividad
- Mapeo de genes
- Genes no reconocidos

La exportación conserva fuentes, atribución, versiones y límites. Los datos de origen mantienen su licencia.

## Versión

`g:Profiler e114_eg62_p19_27110d83 · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## Fuentes

La API g:Profiler permite uso académico y no académico. Los datos Gene Ontology usan CC BY 4.0: conserve atribución, versión y DOI. No se consultan KEGG ni TRANSFAC.

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## Límites de espera

Cada solicitud a este proveedor tiene un límite de 20 segundos. El flujo completo tiene un límite de 120 segundos; la interfaz espera como máximo 125 segundos. Las solicitudes comparten el tiempo restante del flujo. No hay reintentos automáticos. Si el proveedor no responde a tiempo, el análisis termina con un error explícito; no se estima ni se sustituye ningún resultado.
