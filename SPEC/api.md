# API 仕様

最終更新: 2026-06-20  
ベースURL（開発）: `http://localhost:3001`  
ベースURL（本番）: `https://api.game-board.rictaworks.jp`

認証: JWT（Authorizationヘッダー `Bearer <token>`）。全エンドポイント必須。

---

## ボード

| タイトル | メソッド | エンドポイント |
|---|---|---|
| ボード一覧（自分のみ） | GET | `/api/v1/boards` |
| ボード作成 | POST | `/api/v1/boards` |
| ボード詳細 | GET | `/api/v1/boards/:id` |
| ボード更新（タイトル等） | PUT | `/api/v1/boards/:id` |
| ボード削除 | DELETE | `/api/v1/boards/:id` |

---

## オブジェクト

| タイトル | メソッド | エンドポイント |
|---|---|---|
| オブジェクト一覧 | GET | `/api/v1/boards/:board_id/objects` |
| オブジェクト追加 | POST | `/api/v1/boards/:board_id/objects` |
| オブジェクト更新 | PUT | `/api/v1/boards/:board_id/objects/:id` |
| オブジェクト削除 | DELETE | `/api/v1/boards/:board_id/objects/:id` |
| バルク操作 | POST | `/api/v1/boards/:board_id/objects/bulk` |

---

## アジェンダ

| タイトル | メソッド | エンドポイント |
|---|---|---|
| アジェンダ一覧 | GET | `/api/v1/boards/:board_id/agenda_items` |
| アジェンダ追加 | POST | `/api/v1/boards/:board_id/agenda_items` |
| アジェンダ更新 | PUT | `/api/v1/boards/:board_id/agenda_items/:id` |
| アジェンダ削除 | DELETE | `/api/v1/boards/:board_id/agenda_items/:id` |

---

## エクスポート

| タイトル | メソッド | エンドポイント |
|---|---|---|
| PDF 生成（サーバー側） | POST | `/api/v1/boards/:board_id/export` |

---

## WebSocket（ActionCable）

チャンネル: `BoardChannel`  
接続: `wss://api.game-board.rictaworks.jp/cable`（本番）

| イベント | 方向 | ペイロード |
|---|---|---|
| `cursor_moved` | broadcast | `{ user_id, x, y }` |
| `object_created` | broadcast | `{ object }` |
| `object_updated` | broadcast | `{ object }` |
| `object_deleted` | broadcast | `{ object_id }` |
| `object_locked` | broadcast | `{ object_id, user_id }` |
| `object_unlocked` | broadcast | `{ object_id }` |
| `user_joined` | broadcast | `{ user }` |
| `user_left` | broadcast | `{ user_id }` |
| `operation_sync` | broadcast | `{ operations[] }` |
