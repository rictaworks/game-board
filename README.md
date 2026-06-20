# game-board

ゲームUIUX応用ビジネスホワイトボード（MVP）

ゲームUIのパターン（ホットバー・ラジアルメニュー・クエストリスト・ラウンドタイマー等）をビジネス会議用ホワイトボードに応用した、リアルタイム協調編集ウェブアプリ。

---

## 自動ログイン（開発環境）

`RAILS_ENV=development` では認証をバイパスし、以下の開発ユーザーで自動ログインします。

```
URL:  http://localhost:3000
User: Dev User (dev@example.com)
```

本番環境では Google ログインのみ有効です。

---

## ページ一覧

| ページ名 | URL |
|---|---|
| ログイン | [http://localhost:3000/login](http://localhost:3000/login) |
| ボード一覧 | [http://localhost:3000/boards](http://localhost:3000/boards) |
| テンプレート選択（新規作成） | [http://localhost:3000/boards/new](http://localhost:3000/boards/new) |
| ボード編集 | [http://localhost:3000/boards/:id](http://localhost:3000/boards/:id) |

本番 URL: `https://game-board.rictaworks.jp`

---

## API 一覧

詳細仕様: [SPEC/api.md](SPEC/api.md)

| タイトル | エンドポイント |
|---|---|
| ボード一覧 | `GET /api/v1/boards` |
| ボード作成 | `POST /api/v1/boards` |
| ボード詳細 | `GET /api/v1/boards/:id` |
| ボード更新 | `PUT /api/v1/boards/:id` |
| ボード削除 | `DELETE /api/v1/boards/:id` |
| オブジェクト一覧 | `GET /api/v1/boards/:board_id/objects` |
| オブジェクト追加 | `POST /api/v1/boards/:board_id/objects` |
| オブジェクト更新 | `PUT /api/v1/boards/:board_id/objects/:id` |
| オブジェクト削除 | `DELETE /api/v1/boards/:board_id/objects/:id` |
| バルク操作 | `POST /api/v1/boards/:board_id/objects/bulk` |
| アジェンダ一覧 | `GET /api/v1/boards/:board_id/agenda_items` |
| アジェンダ追加 | `POST /api/v1/boards/:board_id/agenda_items` |
| アジェンダ更新 | `PUT /api/v1/boards/:board_id/agenda_items/:id` |
| アジェンダ削除 | `DELETE /api/v1/boards/:board_id/agenda_items/:id` |
| PDF エクスポート | `POST /api/v1/boards/:board_id/export` |
| WebSocket (ActionCable) | `wss://api.game-board.rictaworks.jp/cable` |

---

## 仕様書

| ドキュメント | 内容 |
|---|---|
| [SPEC/api.md](SPEC/api.md) | API 仕様 |
| [SPEC/er.md](SPEC/er.md) | ER 図 |
| [SPEC/dfd.md](SPEC/dfd.md) | DFD |
| [SPEC/sequence.md](SPEC/sequence.md) | シーケンス図 |
| [SPEC/class.md](SPEC/class.md) | クラス図 |
| [SPEC/state.md](SPEC/state.md) | 状態遷移図 |
| [SPEC/usecase.md](SPEC/usecase.md) | ユースケース図 |

---

## 技術スタック

| レイヤー | 技術 |
|---|---|
| フロントエンド | Next.js 14 (App Router) + TypeScript + react-konva |
| 状態管理 | Zustand |
| リアルタイム | ActionCable (WebSocket) |
| バックエンド | Ruby on Rails 7 (API mode) |
| DB（開発） | SQLite |
| DB（本番） | PostgreSQL |
| 認証 | Google OAuth2 (OmniAuth) |
| デプロイ | Vercel（フロント）/ Railway（バックエンド） |
