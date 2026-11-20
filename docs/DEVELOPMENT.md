# 開発手順

## 基本

Node.js 26 / pnpm 9.14.2 を使用します。pnpmが未導入の場合は `npm install --global pnpm@9.14.2` などで導入後、`pnpm install --frozen-lockfile` を実行してください。
`naoiw/.github` の共通規約に従い、ユーザーの個別指示と本リポジトリの設計を優先します。

- `main` を本番ブランチにします。
- 短命ブランチを作り、PRでmainへ統合します。
- 必要な場合だけ `develop` を導入し、本番/プレビューを分離します。
- PR前に `pnpm lint`、`pnpm typecheck`、`pnpm build` を実行します。
- 依存変更後にはlockfileを更新し、CIでは `pnpm install --frozen-lockfile` を使用します。

## GitHub Pages
- `naoiw/.github/.github/workflows/reusable-vite-pages.yml` を呼び出します。
- PRでの構成検証は `dry-run: true` を使用し、本番デプロイを発生させません。
- `develop` のプレビューは単一Pages成果物にまとめる必要があります。
- READMEの公開URLがカスタムドメインの場合はURL欄を適切に修正してください。

## AI指示
`AGENTS.md` などのAIルールを `naoiw/.github` の同期テンプレートから導入します。プロジェクト固有の指示は管理領域の外に記述します。

## Dependabot

`.github/dependabot.yml` はこのテンプレートから作成した新規リポジトリにも複製されます。pnpm管理の依存は `package-ecosystem: npm` で更新確認し、minor/patchのみグループ化、majorは個別PRにします。GitHub Actionsも月次確認します。**自動マージはしません**。

GitHub Settings → Advanced Security で `Dependency graph`、`Dependabot alerts`、`Dependabot security updates` が有効か確認します。共通workflowの参照SHA変更は、`naoiw/.github` の新しいリリースと動作検証を確認してから採用します。
