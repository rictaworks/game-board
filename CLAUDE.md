# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## プロジェクト概要

**game-board** — ゲームUIUX応用ビジネスホワイトボード（MVP）

ゲームUIのパターン（ホットバー・ラジアルメニュー・クエストリスト・ラウンドタイマー等）をビジネス会議用ホワイトボードに応用した、リアルタイム協調編集ウェブアプリ。

| レイヤー | 技術 |
|---|---|
| フロントエンド | Next.js 14 (App Router) + TypeScript + react-konva |
| 状態管理 | Zustand |
| リアルタイム | ActionCable (WebSocket) |
| バックエンド | Ruby on Rails 7 (API mode) |
| DB（開発） | SQLite |
| DB（本番） | PostgreSQL |
| 認証 | Google OAuth2 (OmniAuth) |
| デプロイ | Vercel（フロント）/ Railway（バックエンド・管理画面） |

仕様書: @game-whiteboard-mvp-spec.md

---

## AI 役割分担

| フェーズ | 担当 |
|---|---|
| 設計・Issue 発行・コードレビュー | Claude (Sonnet) — このファイルを読んでいる AI |
| 1次実装 | Antigravity 3.5 Flash — 詳細は @.agents/agents.md |
| セキュリティレビュー | Codex GPT5.5 — 詳細は AGENTS.md |

Claude はコードの 1次実装を行わず、設計・指示出し・レビューに集中する。

---

## ブランチ・PR 規約

- **main ブランチでの作業禁止**
- `src/*` の変更は必ず PR を作成する（main への直接 push 禁止）
- `src/*` 以外（ドキュメント類）は main への直接 push を許可
- PR 本文には非エンジニア向けのユーザーテスト手順を丁寧に記載すること

---

## ディレクトリ管理

| ディレクトリ | 用途 |
|---|---|
| `TASKS/` | タスク管理 |
| `DEBUG/` | バグ報告 |
| `CLIENT/` | クライアント要望 |
| `WORK/` | 作業報告 |
| `ENV/DEVELOPMENT.md` | 開発環境設定 |
| `ENV/PRODUCTION.md` | 本番環境設定 |
| `SPEC/` | 仕様書・ER図・DFD・シーケンス図・クラス図・状態遷移図・ユースケース図 |
| `DELETE/` | ゴミ箱（削除対象ファイルは手動でここへ移動） |
| `test/pr***/` | PR ごとのテストファイル |

図解は Mermaid で記述する。

---

## 開発フロー

- **TDD 厳守**：plan → red test → coding → green test
- **commit 前に必ず security review を実施**（@.claude/OWASP10.md ベース）
- 品質チェックリスト: @.claude/QC10.md
- 開発原則（YAGNI / KISS / DRY / SOLID）: @.claude/development-principles.md
- UI 変更時は CRAP 原則（Contrast / Repetition / Alignment / Proximity）を確認: @.claude/CRAP.md
- フロントエンドの動作確認は curl / wget / Playwright を使うこと
- 環境変数は `.env` を参照すること

---

## テスト方針

| 対象 | フレームワーク |
|---|---|
| フロントエンド | Jest |
| バックエンド | RSpec |
| E2E / UI | Playwright |

- テストファイルは `test/pr***/` に作成し、対象は開発サーバーとする
- テストメソッド詳細: @.claude/TM.md

---

## コーディング規約

- ネイティブの `alert()` / `confirm()` / `prompt()` は**プロジェクト全体で使用禁止**
- グローバル変数禁止（セキュリティ要件）
- 文字列リテラルは設定ファイル・DB・i18n に分離すること
- フォールバック禁止。例外処理を明確に書くこと
- デバッグトレースできるようにログ・エラー情報を残すこと
- 制御構文・条件構文以外はクラスまたは関数に書くこと
- ハードコードが残っていないかテストを書いて確認すること

---

## 多言語対応

当初から 7言語で開発する：**日本語・英語・フランス語・中国語・ロシア語・スペイン語・アラビア語**

管理画面のみ日本語（単一言語で可）。

---

## 安全ルール — 削除系コマンドの禁止（重要）

以下のルールはこのワークスペース内のすべての会話で絶対に守られる：

- Claude はファイルまたはディレクトリを削除するコマンドを一切生成してはならない。
  例：rm, rm -rf, rm *, rmdir, unlink, cache --delete,
      lftp mirror --delete, rsync --delete, git clean -df, find -delete 等。

- 削除が必要な場合でも、Claude は削除コマンドを提案せず、
  「手動で削除してください」といった説明に留めること。

- 削除の推奨・削除操作の自動判断も禁止。

- ssh / lftp / デプロイ系スクリプトを生成する場合でも、
  削除コマンドの生成は禁止。

これらはすべての会話・コード生成に適用される。
