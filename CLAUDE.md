# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

**fuukei** - Next.js 15とCloudflare Workersを使用したWebアプリケーション

### 技術スタック
- Next.js 15.4.6 (App Router, Turbopack)
- React 19.1.0
- TypeScript 5.x (strict mode)
- Tailwind CSS v4
- Biome (リンター/フォーマッター)
- Cloudflare Workers (@opennextjs/cloudflare)
- pnpm 10.17.1

## よく使うコマンド

### 開発
```bash
pnpm run dev        # 開発サーバー起動 (http://localhost:3000)
pnpm run build      # プロダクションビルド
pnpm run precommit  # コミット前チェック（Biome + TypeScript）
```

### デプロイメント
```bash
pnpm run preview    # Cloudflareプレビュー
pnpm run deploy     # Cloudflareデプロイ
```

### コード品質
```bash
pnpm run precommit        # リント・フォーマット・型チェック
```

## アーキテクチャ構成

### ディレクトリ構造
```
src/
└── app/           # Next.js App Router
    ├── layout.tsx # ルートレイアウト
    ├── page.tsx   # ページコンポーネント
    └── globals.css # グローバルスタイル
```

### 重要な設定ファイル
- `biome.json` - コードフォーマット・リント設定
  - インデント: タブ文字
  - クォート: ダブルクォート
  - import自動整理: 有効

- `tsconfig.json` - TypeScript設定
  - strict mode: 有効
  - パスエイリアス: `@/*` → `./src/*`

- `wrangler.jsonc` - Cloudflare Workers設定
- `open-next.config.ts` - OpenNextJS Cloudflare設定

### Cloudflare統合
- OpenNextJS Cloudflareアダプターを使用してNext.jsをCloudflare Workers上で動作
- `getCloudflareContext()`を使用してCloudflare環境変数にアクセス可能
- `.dev.vars`ファイルでローカル開発時の環境変数を設定

## 開発時の注意点

1. **コミット前に必ず実行**: `pnpm precommit`
2. **フォーマット規則**:
   - タブインデント使用
   - ダブルクォート使用
3. **TypeScript**: strict modeが有効なため、型安全性を確保すること
4. **除外ディレクトリ**: `.git/`, `node_modules/`, `.next/`, `.open-next/`, `.wrangler/`は編集対象外
