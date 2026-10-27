# g:GOSt：Gene Ontology の富化解析

ヒト、最大100遺伝子シンボル、情報源はGO:BP、GO:MF、GO:CC。注釈付き背景または最大1,000遺伝子の独自背景。p値には選択した多重検定補正を適用します。KEGGとTRANSFACは使用しません。

## 適用範囲

研究用の計算解析です。診断、病原性、有効性、治療を確定するものではありません。解釈前に対象集団、出典、バージョン、範囲を確認してください。

ELUCENIA内に画面とリクエスト・レスポンスの契約を実装しています。解析には提供元サービスの稼働が必要です。独立した臨床レビューと専門家による言語レビューは完了していません。

## クエリ

- 遺伝子シンボル
- 情報源
- 背景遺伝子セット
- 有意性の閾値
- 多重検定補正
- 電子的注釈を除外
- 患者データや機密情報を含まない、公開または合成の研究データのみを送信することを確認します。

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

公式の用語名と科学的識別子は情報源の言語を保持します。インターフェースのラベルは翻訳済みです。

## 結果

- 用語識別子
- 公式用語名
- 出典
- 補正済み p 値
- 重複遺伝子数
- クエリ遺伝子数
- 用語の遺伝子数
- 参照母集団
- 適合率
- 再現率
- 遺伝子マッピング
- 認識されなかった遺伝子

エクスポートには出典、帰属、バージョン、制限を保持します。原データのライセンスは引き継がれます。

## バージョン

`g:Profiler e114_eg62_p19_* · GO 2026-01-23 · DOI 10.5281/zenodo.18422732`

## 情報源

g:Profiler APIは学術・非学術用途で利用できます。Gene OntologyデータはCC BY 4.0に従うため、出典表示、公開版、DOIを保持してください。KEGGとTRANSFACは照会しません。

- [https://biit.cs.ut.ee/gprofiler/page/apis](https://biit.cs.ut.ee/gprofiler/page/apis)
- [https://biit.cs.ut.ee/gprofiler/page/faq](https://biit.cs.ut.ee/gprofiler/page/faq)
- [https://geneontology.org/docs/go-citation-policy/](https://geneontology.org/docs/go-citation-policy/)

## 待機時間の上限

この提供元への各リクエストの上限は20秒です。処理全体の上限は120秒で、画面は最大125秒待機します。各リクエストは処理全体の残り時間を共有します。自動再試行は行いません。提供元が時間内に応答しない場合、分析は明示的なエラーで終了し、結果の推定や代替は行いません。
