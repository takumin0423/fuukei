# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

fuukei（風景）は、自分だけが知っているお気に入りの風景を共有できるWebサービスです。

## アーキテクチャ

モノレポ構成（pnpm workspace）で、以下のパッケージで構成されています：

- `packages/web`: Next.js 15 + React 19によるフロントエンド（Cloudflare Workersデプロイ対応）
- `packages/server`: Hono + Cloudflare Workersによるバックエンドサーバー

## 開発コマンド

### パッケージ管理
```bash
# 依存関係のインストール（ルートディレクトリで実行）
pnpm install
```

### Webアプリケーション（packages/web）
```bash
# 開発サーバー起動
pnpm --filter @fuukei/web dev

# ビルド
pnpm --filter @fuukei/web build

# Cloudflareへのデプロイ
pnpm --filter @fuukei/web deploy

# Cloudflareプレビュー
pnpm --filter @fuukei/web preview
```

### APIサーバー（packages/server）
```bash
# 開発サーバー起動
pnpm --filter @fuukei/server dev

# Cloudflare Workersへのデプロイ
pnpm --filter @fuukei/server deploy
```

## 技術スタック

- **フロントエンド**: Next.js 15, React 19, Tailwind CSS v4
- **バックエンド**: Hono (Cloudflare Workers対応)
- **デプロイ**: Cloudflare Workers
- **パッケージマネージャー**: pnpm

## コード規約

- TypeScriptを使用
- 日本語でのコメント・ドキュメント記述を推奨
- コンポーネントやファイル名は英語、UIテキストは日本語
