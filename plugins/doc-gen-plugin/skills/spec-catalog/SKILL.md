---
name: spec-catalog
description: AIエージェント実装用の仕様書カタログスキル。20種類のテンプレートから最適な仕様書を対話的に生成する。全テンプレートはAIコーディングエージェントが読んで実装するために最適化されており、人間向けの承認フロー・ステークホルダー管理・コミュニケーション計画等は含まない。「仕様書を作りたい」「RFCを書きたい」「テスト計画を作りたい」「ランブックを書きたい」「SLO を定義したい」「マイグレーション計画を書きたい」「デプロイ手順を作りたい」「ポストモーテムを書きたい」「クイックスペックを書きたい」「実装計画を作りたい」「プロジェクトの CLAUDE.md を作りたい」「Arc42 で設計書を書きたい」「プロダクトブリーフを書きたい」「仕様を一緒に考えたい」「壁打ちしたい」「仕様を探索したい」などのリクエスト時に使用。
---

# 仕様書カタログ

20種類のテンプレートから、AIコーディングエージェントが実装するための仕様書・設計書・運用ドキュメントを対話的に生成するスキル。

**設計方針**: 全テンプレートは「AIエージェントが読んで実装する」ことに特化。人間向けの承認フロー・ステークホルダー管理・担当者割り当て・コミュニケーション計画・変更履歴は含まない。技術的な制約・受入基準・変更禁止事項など、AIが正確に実装するために必要な情報に絞っている。

## テンプレートカタログ

### A. 要件・プロダクト定義系

| ID | テンプレート | パス | 用途 |
|:---|:------------|:-----|:-----|
| A1 | AI PRD | `assets/templates/requirements/ai-prd.md` | AI/MLプロダクトのPRD。モデル要件・倫理・ガードレール・HITL設計 |
| A2 | SRS（ソフトウェア要件仕様書） | `assets/templates/requirements/srs.md` | IEEE 830/ISO 29148準拠。機能要件・非機能要件・制約・検証方法 |
| A3 | ユーザーストーリーマップ | `assets/templates/requirements/user-story-map.md` | ストーリー一覧 + GIVEN/WHEN/THEN受入基準 |
| A4 | プロダクトブリーフ | `assets/templates/requirements/product-brief.md` | 1ページ概要。ビジョン・問題・解決策・成功指標 |

### B. 設計・アーキテクチャ系

| ID | テンプレート | パス | 用途 |
|:---|:------------|:-----|:-----|
| B1 | RFC（Request for Comments） | `assets/templates/design/rfc.md` | 技術提案書。問題→提案→代替案→トレードオフ→承認 |
| B2 | テクニカルデザインドキュメント | `assets/templates/design/technical-design.md` | 詳細技術設計。データモデル・シーケンス図・API契約・エラー戦略 |
| B3 | Arc42 | `assets/templates/design/arc42.md` | 12セクション構成のアーキテクチャ文書 |
| B4 | SDD（ソフトウェア設計記述） | `assets/templates/design/sdd.md` | IEEE 1016/ISO 42010準拠。設計ビューポイント・根拠・トレーサビリティ |
| B5 | 仕様探索ワークシート | `assets/templates/design/spec-exploration.md` | AIとの対話で仕様を段階的に深掘り。ゴール→探索エリア→決定ログ |

### C. AI実装駆動系

| ID | テンプレート | パス | 用途 |
|:---|:------------|:-----|:-----|
| C1 | AI実装仕様書（フェーズ型） | `assets/templates/implementation/ai-impl-spec.md` | AIエージェントが実行するフェーズ順の実装仕様。各フェーズに受入基準 |
| C2 | クイックスペック | `assets/templates/implementation/quick-spec.md` | 1ファイル完結。バグ修正・小機能追加・リファクタ用 |
| C3 | 実装計画 | `assets/templates/implementation/impl-plan.md` | 技術コンテキスト→フェーズ→アーティファクト |
| C4 | タスクリスト | `assets/templates/implementation/task-list.md` | 仕様/計画からタスク分解。依存順・並列可否・完了基準 |

### D. 運用・品質系

| ID | テンプレート | パス | 用途 |
|:---|:------------|:-----|:-----|
| D1 | テスト計画 | `assets/templates/operations/test-plan.md` | テスト戦略・スコープ・テストケース・自動化方針 |
| D2 | マイグレーション計画 | `assets/templates/operations/migration-plan.md` | 移行戦略・ステップ・ロールバック・データ検証 |
| D3 | デプロイメント計画 | `assets/templates/operations/deployment-plan.md` | リリース手順・環境・チェックリスト・ロールバック |
| D4 | ランブック（運用手順書） | `assets/templates/operations/runbook.md` | アラート対応・障害復旧・定期作業手順 |
| D5 | インシデント・ポストモーテム | `assets/templates/operations/post-mortem.md` | 障害報告。タイムライン→根本原因→影響→対策 |
| D6 | SLO/エラーバジェット定義 | `assets/templates/operations/slo-error-budget.md` | サービスレベル目標・エラーバジェット・バーンレート |

### E. プロジェクト基盤系

| ID | テンプレート | パス | 用途 |
|:---|:------------|:-----|:-----|
| E1 | プロジェクトコンテキスト | `assets/templates/foundation/project-context.md` | CLAUDE.md / AGENTS.md 形式。スタック・構造・ルール・ワークフロー |
| E2 | プロジェクト憲章 | `assets/templates/foundation/constitution.md` | プロジェクトの原則・技術基準・品質基準・変更禁止事項 |

## ワークフロー

```
1. テンプレートを選択（自動判定 or ユーザー選択）
   ↓
2. ヒアリング（バッチ質問）
   ↓
3. テンプレートを読み込み、ヒアリング結果で埋める
   ↓
4. Write ツールでファイルを書き出し
   ↓
5. 完了報告
```

## Step 1: テンプレート選択

### 自動判定キーワード

| キーワード | テンプレート |
|:----------|:-----------|
| 「AI PRD」「MLプロダクト要件」 | A1: AI PRD |
| 「SRS」「ソフトウェア要件仕様」「IEEE」 | A2: SRS |
| 「ユーザーストーリー」「ストーリーマップ」「受入基準」 | A3: ユーザーストーリーマップ |
| 「ブリーフ」「概要」「1ページ」「サマリー」 | A4: プロダクトブリーフ |
| 「RFC」「技術提案」「提案書」 | B1: RFC |
| 「技術設計」「テクニカルデザイン」「詳細設計」 | B2: テクニカルデザインドキュメント |
| 「Arc42」「アーキテクチャ文書」 | B3: Arc42 |
| 「SDD」「ソフトウェア設計」「設計記述」 | B4: SDD |
| 「探索」「壁打ち」「仕様検討」「深掘り」「一緒に考えて」「相談」 | B5: 仕様探索ワークシート |
| 「AI実装」「フェーズ型」「エージェント仕様」「実装仕様」 | C1: AI実装仕様書 |
| 「クイック」「簡易仕様」「バグ修正」「小さい修正」 | C2: クイックスペック |
| 「実装計画」「技術計画」「開発計画」 | C3: 実装計画 |
| 「タスク分解」「タスクリスト」「作業分解」 | C4: タスクリスト |
| 「テスト計画」「テスト戦略」「QA」 | D1: テスト計画 |
| 「マイグレーション」「移行計画」「データ移行」 | D2: マイグレーション計画 |
| 「デプロイ」「リリース手順」「リリース計画」 | D3: デプロイメント計画 |
| 「ランブック」「運用手順」「オペレーション」 | D4: ランブック |
| 「ポストモーテム」「障害報告」「インシデント」 | D5: ポストモーテム |
| 「SLO」「SLI」「エラーバジェット」「信頼性」 | D6: SLO/エラーバジェット |
| 「CLAUDE.md」「AGENTS.md」「プロジェクトコンテキスト」 | E1: プロジェクトコンテキスト |
| 「憲章」「プロジェクト原則」「コンスティテューション」 | E2: プロジェクト憲章 |

### 判定不能な場合

AskUserQuestion でカテゴリを選ばせてから、テンプレートを選択させる。

```
質問1: どのカテゴリのドキュメントですか？
  - 要件・プロダクト定義
  - 設計・アーキテクチャ
  - AI実装駆動（AIエージェントに実装させる）
  - 運用・品質
  - プロジェクト基盤

質問2: （カテゴリ内のテンプレートを選択肢として提示）
```

## Step 2: ヒアリング

`references/hearing-patterns.md` を Read ツールで読み、テンプレートIDに対応するヒアリングパターンに従う。

ルール:
- 1回のバッチで1〜4問を AskUserQuestion で質問
- ユーザーが既に回答済みの質問はスキップ
- ユーザーの言語に合わせる

## Step 3: ドキュメント生成

1. テンプレートIDに対応するファイルを Read ツールで読む
2. ヒアリング結果でテンプレートのプレースホルダーを埋める
3. **不要なセクションは削除**、**必要なセクションは自由に追加**してよい
4. Mermaid図がある場合、内容に合わせて正確に描画する

## Step 4: ファイル書き出し

**Write ツールで書き出す。**

## Step 5: 完了報告

書き出したファイルのパスと概要を表示する。

## 出力先

**デフォルト出力先**: `docs/`
**カスタム出力**: ユーザーが指定した場合はそのパスを使用。

ファイル名規則:
| テンプレート | ファイル名 |
|:------------|:----------|
| AI PRD | `docs/ai-prd-{name}.md` |
| SRS | `docs/srs-{name}.md` |
| ユーザーストーリーマップ | `docs/user-stories-{name}.md` |
| プロダクトブリーフ | `docs/brief-{name}.md` |
| RFC | `docs/rfc-{NNN}-{name}.md` |
| テクニカルデザイン | `docs/design-{name}.md` |
| Arc42 | `docs/arc42-{name}.md` |
| SDD | `docs/sdd-{name}.md` |
| 仕様探索ワークシート | `docs/exploration-{name}.md` |
| AI実装仕様書 | `docs/impl-spec-{name}.md` |
| クイックスペック | `docs/quick-{name}.md` |
| 実装計画 | `docs/impl-plan-{name}.md` |
| タスクリスト | `docs/tasks-{name}.md` |
| テスト計画 | `docs/test-plan-{name}.md` |
| マイグレーション計画 | `docs/migration-{name}.md` |
| デプロイメント計画 | `docs/deploy-{name}.md` |
| ランブック | `docs/runbook-{name}.md` |
| ポストモーテム | `docs/postmortem-{YYYY-MM-DD}-{name}.md` |
| SLO/エラーバジェット | `docs/slo-{name}.md` |
| プロジェクトコンテキスト | `CLAUDE.md` または `AGENTS.md`（プロジェクトルート） |
| プロジェクト憲章 | `docs/constitution.md` |
