---
name: api-spec
description: API仕様書を対話的に生成。Markdown・OpenAPI (YAML)・GraphQLスキーマの3形式に対応。
disable-model-invocation: true
allowed-tools: Read, Write, AskUserQuestion
argument-hint: "[API名]"
---

# API仕様書ジェネレーター

API仕様書を対話的に作成するスキル。3つの出力フォーマットに対応。

## 出力フォーマット

| フォーマット | テンプレート | 用途 |
|:------------|:------------|:-----|
| Markdown | `assets/templates/api-spec.md` | 人が読むためのAPIドキュメント |
| OpenAPI | `assets/templates/openapi.yaml` | 機械可読なREST API定義（OpenAPI 3.1） |
| GraphQL | `assets/templates/graphql-schema.md` | ドキュメント付きGraphQLスキーマ定義 |

## ワークフロー

```
1. 出力フォーマットを判定
   ↓
2. ヒアリング（AskUserQuestionでバッチ質問）
   ↓
3. テンプレートからスペックを生成
   ↓
4. ユーザーに提示してレビュー
   ↓
5. 修正があれば反映 → 最終版を書き出し
```

## Step 1: フォーマット判定

ユーザーのリクエストから検出:
- 「API仕様書」「APIドキュメント」「REST API」 → **Markdown**
- 「OpenAPI」「Swagger」「YAML定義」 → **OpenAPI**
- 「GraphQL」「スキーマ定義」「schema」 → **GraphQL**
- 曖昧な場合 → AskUserQuestion で確認

1回のヒアリングから複数フォーマットを生成することも可能。

## Step 2: ヒアリング

`references/hearing-patterns.md` を Read ツールで読み、**共通ルール**とバッチ形式のヒアリングフローに従う。

### ルール

0. **AskUserQuestion を必ず使う**。ヒアリングを行わずに Step 3 に進んではならない
1. **バッチ質問を起点に掘り下げる**。バッチ質問で得た回答に対し、不明点があれば追加で深掘りする
2. **1回の AskUserQuestion で1〜3問**。ユーザーが多くの情報を一度に出してくれた場合は、確認質問だけでよい
3. **回答を要約して確認**してから次のトピックに進む
4. **曖昧シグナルを検知**したら必ず掘り下げる（hearing-patterns.md の「曖昧シグナルと対応」参照）
5. **十分性を判断**する: そのトピックについて**不明点が完全にゼロ**か？ 1つでも「たぶんこうだろう」と推測する箇所があるなら掘り下げが足りない
6. **全トピックについて不明点がゼロになるまで** Step 3 に進まない
7. **ユーザーが「もう十分」と言った場合**はそこで止める。ただし不明点が残っていれば「〜についてはまだ不明ですが、スキップしてよいですか？」と具体的に列挙して確認
8. ユーザーが既に回答済みの質問はスキップ
9. ユーザーの言語に合わせる
10. OpenAPI: リクエスト/レスポンススキーマの正確さを重視
11. GraphQL: 型、クエリ、ミューテーション、サブスクリプションを重視

## Step 3: ドキュメント生成

### 前提条件（ゲート）
- Step 2 で**最低1回は AskUserQuestion を実行済み**であること
- 全トピックについて**不明点がゼロ**であること（推測・仮定で埋めた箇所がないこと）
- ユーザーが明示的にスキップを宣言したトピックは除く
- 上記を満たさない場合、ドキュメント生成に進んではならない

1. `assets/templates/` からテンプレートを読む
2. ヒアリング結果に基づいてセクションを記入
3. セクション適応（`references/hearing-patterns.md` 参照）
4. フォーマット別のルール:
   - **Markdown**: データフローのMermaidシーケンス図、エンドポイントのテーブル
   - **OpenAPI**: OpenAPI 3.1仕様に準拠したYAML、再利用可能なスキーマは `$ref` を使用
   - **GraphQL**: SDL構文、説明はdocコメントとして記載、リゾルバーの補足は別セクション

## Step 4: 提示とレビュー

1. 生成したスペックのサマリーを表示
2. 修正が必要か確認
3. 修正があれば反映 → 再提示
4. 承認されたらファイルに書き出し

## 出力先

**デフォルト出力先**: `docs/`
**カスタム出力**: ユーザーが指定した場合はそのパスを使用。

ファイル名:
- `docs/api-spec-{name}.md`
- `docs/openapi-{name}.yaml`
- `docs/graphql-schema-{name}.md`
