# 開発環境

## 必要条件

| ツール | バージョン |
|---|---|
| Node.js | 20.x 以上 |
| Ruby | 3.3.x |
| SQLite | 3.x |
| npm / yarn | 最新安定版 |
| gh CLI | 最新安定版 |

## セットアップ

```bash
# フロントエンド
cd game-board-frontend
npm install
cp .env.example .env.local
npm run dev        # http://localhost:3000

# バックエンド
cd game-board-backend
bundle install
cp .env.example .env
bin/rails db:create db:migrate db:seed
bin/rails server  # http://localhost:3001
```

## 環境変数（.env）

| キー | 説明 |
|---|---|
| `GOOGLE_CLIENT_ID` | Google OAuth クライアントID |
| `GOOGLE_CLIENT_SECRET` | Google OAuth シークレット |
| `RAILS_ENV` | `development` |
| `DATABASE_URL` | SQLite パス（開発時省略可） |
| `FRONTEND_URL` | `http://localhost:3000` |

## 開発環境の自動ログイン

`RAILS_ENV=development` 時は認証をバイパスし、固定の開発ユーザーで自動ログインする。

```
開発ユーザー: dev@example.com / Dev User
```

## 図解ツール

```bash
npm install -g @mermaid-js/mermaid-cli
# SPEC/ 以下の .md を PNG に変換
mmdc -i SPEC/er.md -o SPEC/er.png
```
