# g:GOSt : enrichissement Gene Ontology

Humain ; jusqu’à 100 symboles de gènes ; sources GO:BP, GO:MF et GO:CC. Fond annoté ou jusqu’à 1 000 gènes de fond personnalisés. Les valeurs p utilisent la correction choisie. KEGG et TRANSFAC sont exclus.

## Périmètre

Analyse informatique pour la recherche. Elle ne détermine ni diagnostic, ni pathogénicité, ni efficacité, ni traitement. Vérifiez population, source, version et périmètre avant interprétation.

Interface et contrats implémentés dans ELUCENIA. L’analyse dépend de la disponibilité du service responsable. La révision clinique indépendante et la révision linguistique professionnelle ne sont pas achevées.

## Requête

- Symboles des gènes
- Sources
- Ensemble de gènes de référence
- Seuil de significativité
- Correction des tests multiples
- Exclure les annotations électroniques
- Je confirme que je transmettrai uniquement des données de recherche publiques ou synthétiques, sans données de patients ni données confidentielles.

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

Les noms officiels des termes et identifiants scientifiques conservent la langue de la source ; les libellés de l’interface sont traduits.

## Résultats

- Identifiant du terme
- Nom officiel du terme
- Source
- Valeur p ajustée
- Gènes communs
- Gènes de la requête
- Gènes du terme
- Univers de référence
- Précision
- Rappel
- Correspondance des gènes
- Gènes non reconnus

L’export conserve les sources, l’attribution, les versions et les limites. Les données sources conservent leur licence.

## Version

`g:Profiler e114_eg62_p19_* · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## Sources

L’API g:Profiler permet un usage académique et non académique. Les données Gene Ontology utilisent CC BY 4.0 : conservez attribution, version et DOI. KEGG et TRANSFAC ne sont pas interrogés.

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## Limites d’attente

Chaque requête à ce fournisseur est limitée à 20 secondes. Le traitement complet est limité à 120 secondes ; l’interface attend au maximum 125 secondes. Les requêtes partagent le temps restant du traitement. Aucune nouvelle tentative n’est automatique. Si le fournisseur ne répond pas à temps, l’analyse se termine par une erreur explicite ; aucun résultat n’est estimé ni substitué.
