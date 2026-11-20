# __DISPLAY_NAME__

> ここにアプリの概要を記入してください。テンプレートから新規リポジトリを作成したら、`__DISPLAY_NAME__` と公開URLのプレースホルダーを置き換えます。

## 公開URL

| 環境 | ブランチ | URL | 状態 |
| --- | --- | --- | --- |
| 本番 | `main` | `https://__OWNER__.github.io/__PROJECT_NAME__/` | 未公開 |
| 開発プレビュー（任意） | `develop` | `https://__OWNER__.github.io/__PROJECT_NAME__/develop/` | 未使用 |

> **URL欄は記入例です。** GitHubの「Use this template」ではリポジトリ名・公開URLを自動置換しません。独自ドメインやCloudflare等を使う場合は公開先に合わせて編集してください。developを使用しない場合は2行目を削除してください。

## 主な機能

- （このアプリの主要機能を記入）
- （必要に応じて項目を追加）

## 技術スタック

- React 19 / TypeScript（strict）/ Vite
- Node.js 26 / **pnpm 9.14.2**
- ESLint / GitHub Actions / GitHub Pages（任意）

## ローカル開発

```bash
pnpm install --frozen-lockfile
pnpm dev
```

pnpmが未インストールの場合は、最初に `npm install --global pnpm@9.14.2` などで導入してください。

変更時のチェック：

```bash
pnpm lint
pnpm typecheck
pnpm build
```

依存関係を追加・更新した場合は`pnpm install`を実行し、`pnpm-lock.yaml`もコミットしてください。`package-lock.json`は使用しません。

## 公開と開発フロー

- 原則`main`を本番とし、作業ブランチで開発してPRを作成します。
- `develop`によるプレビューは必要なリポジトリにだけ追加します。
- Pagesを利用する場合は **Settings → Pages → Build and deployment → GitHub Actions** を設定し、Actionsの`Deploy GitHub Pages`を手動実行してください。テンプレート自体は自動公開しません。
- この雛形のCI・Pagesは`naoiw/.github`の共通ワークフローをSHA固定で参照します。
- **main保護、Pagesの自動デプロイ化、developプレビューの追加手順**は [開発・デプロイ](docs/DEVELOPMENT.md#新しいリポジトリを作ったら) に記載しています。詳細なYAML例は [共通セットアップガイド](https://github.com/naoiw/.github/blob/main/standards/NEW_WEB_APP_SETUP.md) を参照してください。

## 依存関係の保守

- `.github/dependabot.yml` でpnpm依存とGitHub Actionsを**月次**確認します（pnpmのエコシステム名は`npm`）。
- minor/patch更新をまとめ、major更新は個別PRで検証します。**自動マージはしません**。
- GitHub側の`Dependency graph`、`Dependabot alerts`、`Dependabot security updates`は各リポジトリのSettingsで別途確認してください。
- 共通workflowのSHA更新は、`naoiw/.github` のリリースを確認したうえでPRで検証します。

## ドキュメント

- [アーキテクチャ](docs/ARCHITECTURE.md)
- [開発・デプロイ](docs/DEVELOPMENT.md)
- [共通開発規約](https://github.com/naoiw/.github)

## ライセンス

[MIT License](LICENSE)。アプリの公開前に著作権者・年と外部素材のライセンスを確認してください。

---

<details>
<summary>テンプレートから作成した直後のチェックリスト</summary>

- [ ] READMEのアプリ名・概要・機能・公開URLを書き換える
- [ ] `package.json`の`name`を変更する
- [ ] `index.html`、`src/App.tsx`の表示名を変更する
- [ ] LICENSEの著作権者と年を確認する
- [ ] `pnpm install`でlockfileを更新し、`pnpm build`を確認する
- [ ] Pagesを使う場合は Settings → Pages → Source: GitHub Actions を設定し、初回の手動デプロイを確認する
- [ ] mainのPR必須・CI必須・force push/削除禁止のRulesetを設定する
- [ ] 手動公開 / main自動公開 / main+developプレビューのどの運用を使うか決める（初期状態は手動）
- [ ] GitHub側のDependabot/Dependency graph設定を確認する

</details>
