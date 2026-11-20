# 開発手順

## 基本
`naoiw/.github` の共通規約に従い、ユーザーの個別指示と本リポジトリの設計を優先します。

- `main` を本番ブランチにします。
- 短命ブランチを作り、PRでmainへ統合します。
- 必要な場合だけ `develop` を導入し、本番/プレビューを分離します。
- PR前に `npm run lint`、`npm run typecheck`、`npm run build` を実行します。
- 依存変更後にはlockfileを更新し、CIでは `npm ci` を使用します。

## GitHub Pages
- `naoiw/.github/.github/workflows/reusable-vite-pages.yml` を呼び出します。
- PRでの構成検証は `dry-run: true` を使用し、本番デプロイを発生させません。
- `develop` のプレビューは単一Pages成果物にまとめる必要があります。
- READMEの公開URLがカスタムドメインの場合はURL欄を適切に修正してください。

## AI指示
`AGENTS.md` などのAIルールを `naoiw/.github` の同期テンプレートから導入します。プロジェクト固有の指示は管理領域の外に記述します。
