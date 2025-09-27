# Repository Guidelines

## プロジェクト構成とモジュール配置
本リポジトリは Next.js 15 App Router と Cloudflare 向け OpenNext を採用しています。主なアプリコードは src/app 配下にあり、layout.tsx で全体レイアウト、page.tsx でトップページを定義します。スタイルは globals.css と必要に応じたモジュール CSS を想定してください。静的アセットは public ディレクトリに配置し、設定ファイル類は next.config.ts、open-next.config.ts、wrangler.jsonc、biome.json がルート直下にまとまっています。開発ツールのバージョンは mise.toml で pnpm 10.17.1、Node.js 24.9.0 を固定しています。

## ビルド・テスト・開発コマンド
- `pnpm install`: lockfile を基に依存関係を同期します。
- `pnpm dev`: Turbopack で開発サーバーを起動し、http://localhost:3000 を監視します。
- `pnpm build`: Next.js の本番ビルドを生成します。
- `pnpm start`: `pnpm build` の成果物をローカルで検証します。
- `pnpm deploy`: `opennextjs-cloudflare build` 後に Cloudflare 環境へデプロイします。
- `pnpm preview`: デプロイ前プレビューを Cloudflare Pages/Workers で確認します。
- `pnpm precommit`: Biome フォーマットと TypeScript 型チェックをまとめて実行します。
- `pnpm cf-typegen`: `cloudflare-env.d.ts` に基づき Wrangler の型定義を再生成します。

## コーディングスタイルと命名
Biome の設定でタブインデントと二重引用符が強制されるため、フォーマッターは `pnpm biome check .` かエディタ統合で常時実行してください。React コンポーネントは PascalCase、フックやユーティリティは camelCase とし、環境変数は CF_ や EDGE_ など用途が分かる接頭辞を付けます。共有スタイルは globals.css または Tailwind CSS 4 のプラグイン経由で定義し、ARIA 属性やメタデータを用いてアクセシビリティを意識したマークアップを心掛けてください。

## テストガイドライン
現時点で package.json に公式テストスクリプトは未登録です。UI ロジックを追加する際は Vitest の導入を検討し、`src/app/**/__tests__/*.test.tsx` 形式で配置してください。重要なユーティリティとサーバーアクションは最小でもブランチカバレッジ 70% を目標とし、スナップショットを使う場合は差分レビューが容易になるようファイルを機能単位で分割します。CI を導入するまでは `pnpm precommit` の成功ログとともに PR を提出してください。E2E 検証が必要な場合は Playwright を利用し、`tests/e2e` ディレクトリを新設してシナリオを管理します。

## コミットと Pull Request
履歴では「CLAUDE.md追加」「Biome追加」のように 1 つの変更目的を短い命令形でまとめています。先頭に対象領域 (例: feat, fix, docs) を付けた上で 50 文字以内を目安に具体的な差分を記述し、必要ならサブコマンドで補足してください。Pull Request では概要、関連 Issue、ローカルで実施したコマンド、UI 変更がある場合のスクリーンショットを含めます。デプロイに影響する場合は Cloudflare の環境名、変更したバインディング、ロールバック手順を明記してください。

## Cloudflare設定とセキュリティ
デプロイ前に wrangler.jsonc のバインディングと cloudflare-env.d.ts の型定義を同期し、不要になったキーは `pnpm wrangler secret delete` で即時削除します。シークレットは `pnpm wrangler secret put` で投入し、ローカル環境には .env を残さない方針です。外部エンドポイントの URL や API キーはサーバーコンポーネントもしくは Edge Runtime でのみ参照し、クライアントへの露出を避けてください。Workers KV や D1 を追加する際は、バインディング名を PascalCase で定義し、型安全に扱うため cf-typegen を再実行することを推奨します。
