# 本番環境

## インフラ構成

| コンポーネント | サービス | URL |
|---|---|---|
| フロントエンド | Vercel | https://game-board.rictaworks.jp |
| バックエンド API | Railway（優先）/ Render | https://api.game-board.rictaworks.jp |
| DB | PostgreSQL（Railway 内蔵） | — |
| 画像ストレージ | Active Storage → S3 / R2 | — |

## 環境変数（Railway / Render で設定）

| キー | 説明 |
|---|---|
| `RAILS_ENV` | `production` |
| `SECRET_KEY_BASE` | Rails シークレットキー |
| `DATABASE_URL` | PostgreSQL 接続文字列 |
| `GOOGLE_CLIENT_ID` | Google OAuth クライアントID |
| `GOOGLE_CLIENT_SECRET` | Google OAuth シークレット |
| `FRONTEND_URL` | https://game-board.rictaworks.jp |
| `AWS_ACCESS_KEY_ID` | S3 / R2 アクセスキー（画像保存用） |
| `AWS_SECRET_ACCESS_KEY` | S3 / R2 シークレット |
| `AWS_BUCKET` | S3 / R2 バケット名 |

## デプロイ手順

ウェブアプリのため、**デプロイから先の作業は ClaudeDesktop で実施する**。

```bash
# フロントエンド（Vercel は git push で自動デプロイ）
git push origin main

# バックエンド（Railway は git push で自動デプロイ）
git push railway main
bin/rails db:migrate  # マイグレーションは手動確認必須
```

## ドメイン

原則 `rictaworks.jp` のサブドメインを使用する。
