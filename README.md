# React / TypeScript / Vite Template

React 19・TypeScript・Viteを使用した、GitHub Pages対応のWebアプリ用テンプレートです。

**新規リポジトリ作成にはGitHubの [Use this template](https://github.com/naoiw/react-vite-template/generate) を利用してください。**
このリポジトリ自体はテンプレートのため、GitHub Pagesを自動公開しません。

## 含まれるもの

- React + TypeScript（strict）+ Vite
- ESLint / TypeScript型チェック / GitHub Actions CI
- naoiw共通のAI開発指示（AGENTS.md、Cursor、Copilot）
- 既定のCSSとページレイアウト
- README・docs・MIT LICENSEの雛形
- 手動実行専用のPagesワークフロー（公開時のみ利用）

## 新規プロジェクトを作った後

1. **Use this template** でリポジトリを作成します。
2. `package.json` と `package-lock.json` の `name`、READMEのタイトル、`index.html` と `src/App.tsx` の表示名を変更します。
3. LICENSEの著作権者と年を確認します。第三者の素材には別途ライセンスが適用されます。
4. `npm install` を実行してlockfileを更新し、コミットします。
5. `npm run lint && npm run typecheck && npm run build` で検証します。
6. Pagesを使用する場合はSettings → Pages → Build and deploymentを **GitHub Actions** に変更し、Actions → Deploy GitHub Pagesを手動実行します。定期公開が必要ならworkflowの`push`トリガーを追加してください。

## 開発コマンド

```bash
npm ci
npm run dev
npm run lint
npm run typecheck
npm run build
npm run preview
```

Node.js 26系を使用します。CI・Pagesは `naoiw/.github` の[共通ワークフロー v1.0.0](https://github.com/naoiw/.github/releases/tag/workflows-v1.0.0)の**検証済みコミットSHA**に固定しています。

## ドキュメント

- [アーキテクチャ](docs/ARCHITECTURE.md)
- [開発・デプロイ](docs/DEVELOPMENT.md)
- [共通開発規約](https://github.com/naoiw/.github)

## ライセンス

MIT License（[LICENSE](LICENSE)）。このテンプレートの元となった共通規約・雛形は `naoiw/.github` で管理されています。
