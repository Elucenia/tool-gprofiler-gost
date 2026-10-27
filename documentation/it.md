# g:GOSt: arricchimento Gene Ontology

Umano; fino a 100 simboli di geni; fonti GO:BP, GO:MF e GO:CC. Fondo annotato o fino a 1.000 geni di fondo personalizzato. I valori p usano la correzione selezionata. KEGG e TRANSFAC sono esclusi.

## Ambito

Analisi computazionale per ricerca. Non determina diagnosi, patogenicità, efficacia o trattamento. Verifica popolazione, fonte, versione e ambito prima di interpretare.

Interfaccia e contratti implementati in ELUCENIA. L’analisi dipende dalla disponibilità del servizio responsabile. La revisione clinica indipendente e la revisione linguistica professionale non sono complete.

## Ricerca

- Simboli dei geni
- Fonti
- Insieme di geni di fondo
- Soglia di significatività
- Correzione per test multipli
- Escludi annotazioni elettroniche
- Confermo che invierò solo dati di ricerca pubblici o sintetici, senza dati di pazienti o informazioni riservate.

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

I nomi ufficiali dei termini e gli identificatori scientifici conservano la lingua della fonte; le etichette dell’interfaccia sono tradotte.

## Risultati

- Identificativo del termine
- Nome ufficiale del termine
- Fonte
- Valore p corretto
- Geni in comune
- Geni della ricerca
- Geni del termine
- Universo di riferimento
- Precisione
- Richiamo
- Mappatura dei geni
- Geni non riconosciuti

L’esportazione conserva fonti, attribuzione, versioni e limiti. I dati originali mantengono la propria licenza.

## Versione

`g:Profiler e114_eg62_p19_* · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## Fonti

L’API g:Profiler consente l’uso accademico e non accademico. I dati Gene Ontology usano CC BY 4.0: conservare attribuzione, versione e DOI. KEGG e TRANSFAC non vengono interrogati.

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## Limiti di attesa

Ogni richiesta a questo fornitore ha un limite di 20 secondi. Il flusso completo ha un limite di 120 secondi; l’interfaccia attende al massimo 125 secondi. Le richieste condividono il tempo rimanente del flusso. Non sono previsti tentativi automatici. Se il fornitore non risponde in tempo, l’analisi termina con un errore esplicito; nessun risultato viene stimato o sostituito.
