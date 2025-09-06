# fuukei - 風景

自分だけが知っている、お気に入りの風景を共有できるサービス

## 🌄 コンセプト

誰もが心に秘めている特別な場所があります。

**fuukei（風景）** は、そんな「自分だけが知っている風景」を大切に共有できる場所です。

観光地ではない、ガイドブックには載っていない、でも誰かの心に残る風景。
そんな特別な瞬間と場所を、同じように風景を好きな人たちと共有できるサービスです

## 🚀 セットアップ

### 必要な環境

- Node.js 20以上
- pnpm 10.15.1以上

### インストール

```bash
# リポジトリのクローン
git clone git@github.com:takumin0423/fuukei.git
cd fuukei

# 依存関係のインストール
pnpm install
```

### 開発

```bash
# Webアプリケーションの開発サーバー起動
pnpm --filter @fuukei/web dev

# APIサーバーの開発サーバー起動
pnpm --filter @fuukei/server dev
```

## 📦 プロジェクト構成

```
fuukei/
├── packages/
│   ├── web/        # Next.js フロントエンド
│   └── server/     # Hono APIサーバー
├── pnpm-workspace.yaml
└── package.json
```

## 🛠 技術スタック

- **フロントエンド**: Next.js 15, React 19, Tailwind CSS
- **バックエンド**: Hono, Cloudflare Workers
- **インフラ**: Cloudflare Workers
- **パッケージ管理**: pnpm workspace
