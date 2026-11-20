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
corepack enable
pnpm install --frozen-lockfile
pnpm dev
```

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
- [ ] Pagesを使う場合だけ公開先を設定する

</details>
