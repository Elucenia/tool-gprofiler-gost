# g:GOSt: Gene-Ontology-Anreicherung

Mensch; bis zu 100 Gensymbole; Quellen GO:BP, GO:MF und GO:CC. Annotierter Hintergrund oder bis zu 1.000 eigene Hintergrundgene. P-Werte verwenden die gewählte Korrektur für multiples Testen. KEGG und TRANSFAC sind ausgeschlossen.

## Umfang

Computergestützte Forschungsanalyse. Sie begründet keine Diagnose, Pathogenität, Wirksamkeit oder Behandlung. Prüfen Sie Population, Herkunft, Version und Umfang vor der Interpretation.

Oberfläche und Schnittstellenverträge sind in ELUCENIA implementiert. Die Analyse hängt von der Verfügbarkeit des zuständigen Dienstes ab. Die unabhängige klinische Prüfung und die professionelle sprachliche Prüfung sind nicht abgeschlossen.

## Abfrage

- Gensymbole
- Quellen
- Hintergrund-Gensatz
- Signifikanzschwelle
- Korrektur für multiples Testen
- Elektronische Annotationen ausschließen
- Ich bestätige, dass ich ausschließlich öffentliche oder synthetische Forschungsdaten ohne Patienten- oder vertrauliche Daten übermittle.

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

Offizielle Begriffsnamen und wissenschaftliche Kennungen bleiben in der Quellsprache; die Oberflächenbeschriftungen sind übersetzt.

## Ergebnisse

- Begriffskennung
- Offizieller Begriffsname
- Quelle
- Adjustierter p-Wert
- Überlappende Gene
- Abfragegene
- Gene des Begriffs
- Referenzuniversum
- Präzision
- Vollständigkeit
- Genzuordnung
- Nicht erkannte Gene

Der Export erhält Quellen, Attribution, Versionen und Grenzen. Quelldaten behalten ihre Lizenz.

## Version

`g:Profiler e114_eg62_p19_27110d83 · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## Quellen

Die g:Profiler-API erlaubt akademische und nicht akademische Nutzung. Gene-Ontology-Daten stehen unter CC BY 4.0: Quellenangabe, Version und DOI müssen erhalten bleiben. KEGG und TRANSFAC werden nicht abgefragt.

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## Wartezeitbegrenzungen

Jede Anfrage an diesen Anbieter ist auf 20 Sekunden begrenzt. Der gesamte Ablauf ist auf 120 Sekunden begrenzt; die Oberfläche wartet höchstens 125 Sekunden. Die Anfragen teilen sich die verbleibende Zeit des Ablaufs. Es gibt keine automatische Wiederholung. Antwortet der Anbieter nicht rechtzeitig, endet die Analyse mit einer ausdrücklichen Fehlermeldung; es wird kein Ergebnis geschätzt oder ersetzt.
