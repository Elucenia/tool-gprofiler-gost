# g:GOSt: enriquecimento em Gene Ontology

Humanos; até 100 símbolos de genes; fontes GO:BP, GO:MF e GO:CC. Fundo anotado ou até 1.000 genes de fundo personalizado. Valores p são corrigidos pelo método escolhido. Não usa KEGG ou TRANSFAC.

## Escopo

Análise computacional para pesquisa. Não determina diagnóstico, patogenicidade, eficácia ou tratamento. Confira população, fonte, versão e escopo antes de interpretar.

Interface e contratos implementados na ELUCENIA. A análise depende da disponibilidade do serviço responsável. Revisão clínica independente e revisão linguística profissional não concluídas.

## Consulta

- Símbolos dos genes
- Fontes
- Genes de referência de fundo
- Limiar de significância
- Correção de testes múltiplos
- Excluir anotações eletrônicas
- Confirmo que enviarei somente dados públicos ou sintéticos de pesquisa, sem dados de pacientes ou dados confidenciais.

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

Nomes oficiais de termos e identificadores científicos são preservados no idioma da fonte; os rótulos da interface estão traduzidos.

## Resultados

- Identificador do termo
- Nome oficial do termo
- Fonte
- Valor p ajustado
- Genes em comum
- Genes na consulta
- Genes no termo
- Universo de referência
- Precisão
- Revocação
- Mapeamento dos genes
- Genes não reconhecidos

A exportação conserva fontes, atribuição, versões e limites. Dados de origem mantêm sua licença.

## Versão

`g:Profiler e114_eg62_p19_27110d83 · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## Fontes

A API g:Profiler permite uso acadêmico e não acadêmico. Os dados Gene Ontology usam CC BY 4.0: preserve a atribuição, a versão e o DOI. KEGG e TRANSFAC não são consultados.

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## Limites de espera

Cada requisição a este provedor tem limite de 20 segundos. O fluxo completo tem limite de 120 segundos; a interface espera no máximo 125 segundos. Os pedidos compartilham o tempo restante do fluxo. Não há repetição automática. Se o provedor não responder a tempo, a análise termina com um erro explícito; nenhum resultado é estimado ou substituído.
