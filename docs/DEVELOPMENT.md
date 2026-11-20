# 開発手順

## 基本

Node.js 26 / pnpm 9.14.2 を使用します。pnpmが未導入の場合は `npm install --global pnpm@9.14.2` などで導入後、`pnpm install --frozen-lockfile` を実行してください。
`naoiw/.github` の共通規約に従い、ユーザーの個別指示と本リポジトリの設計を優先します。

- `main` を本番ブランチにします。
- 短命ブランチを作り、PRでmainへ統合します。
- 必要な場合だけ `develop` を導入し、本番/プレビューを分離します。
- PR前に `pnpm lint`、`pnpm typecheck`、`pnpm build` を実行します。
- 依存変更後にはlockfileを更新し、CIでは `pnpm install --frozen-lockfile` を使用します。

## 新しいリポジトリを作ったら

[naoiw/react-vite-template](https://github.com/naoiw/react-vite-template) の **Use this template → Create a new repository** で作成した後、次の順に設定します。**GitHubのRulesetsやPages設定はテンプレートから継承されません。**

1. READMEの `__DISPLAY_NAME__`、`__OWNER__`、`__PROJECT_NAME__`、概要、公開URL、`package.json` のname、`index.html` のtitle、`src/App.tsx`、LICENSEの著作権者・年を実プロジェクトに変更する。
2. Node 26 / pnpm 9.14.2で `pnpm install --frozen-lockfile`、`pnpm lint`、`pnpm typecheck`、`pnpm build` を確認する。依存を追加したときだけ `pnpm install` でlockfileを更新する。
3. **Settings → Pages → Build and deployment → Source: GitHub Actions** を選ぶ。
4. main向けPRなどでActions **CI** を1回成功させて、必要なStatus Check名を確認する。
5. **Settings → Rules → Rulesets → New branch ruleset** で `main` を対象に、PR必須・Status Check必須（通常 `shared-check / validate`）・force push禁止・削除禁止を設定する。単独開発なら承認レビュー数0を検討する。
6. **Actions → Deploy GitHub Pages → Run workflow → main** で初回公開し、`https://<owner>.github.io/<repo>/` の表示と静的アセットを確認する。

保護ルールやプランによる制約、GitHub Pagesの異なる運用モードは [naoiw/.githubの新規アプリ設定ガイド](https://github.com/naoiw/.github/blob/main/standards/NEW_WEB_APP_SETUP.md) を参照してください。

## GitHub Pages

このテンプレートは `.github/workflows/deploy-pages.yml` から、SHA固定された `naoiw/.github/.github/workflows/reusable-vite-pages.yml` を呼び出します。GitHub Pagesの初期設定が済むまでは**手動実行のみ**です。

| 運用方法 | 設定変更 | 公開先 |
| --- | --- | --- |
| mainのみ・手動公開（初期状態） | 変更不要。Actionsから手動実行 | `/<repo>/` |
| mainのみ・pushで自動公開 | `deploy-pages.yml` のトリガーを変更 | `/<repo>/` |
| main + developプレビュー | develop作成、CI対象拡大、Pages workflowを変更 | `/<repo>/` と `/<repo>/develop/` |

### mainを自動デプロイにする

**mainのPR必須・CI必須を設定した後**、`.github/workflows/deploy-pages.yml` の `on` を次へ変更します。他の `permissions`、`jobs`、SHA、pnpmの入力値はそのままです。

```yaml
on:
  push:
    branches: [main]
  workflow_dispatch:
```

マージ後のmainへのpushで再デプロイします。PRを開いただけでは本番公開されません。

### developプレビューを追加する

1. 本当に必要な場合だけ `develop` ブランチを作成します。
2. `.github/workflows/ci.yml` の `push.branches` と `pull_request.branches` をどちらも `[main, develop]` にします。workflow名の **`CI` を変えない**でください。
3. `.github/workflows/deploy-pages.yml` を、共有Pagesの `publish-preview: true` と、developのCI成功時のみ発火する `workflow_run` 構成へ変更します。**単にdevelop用の別Pagesデプロイを追加してはいけません。** 1つの成果物に本番とプレビューをまとめる必要があります。
4. 呼び出し側は `package-manager: pnpm`、`node-version: "26"`、`pnpm-version: "9.14.2"` を維持し、`preview-branch: develop`、`preview-subpath: develop` を設定します。
5. **Pagesワークフローはmainにも配置**します（`workflow_run` はデフォルトブランチに定義が必要）。main/develop両方のCIと、`/<repo>/`、`/<repo>/develop/` の表示を確認します。必要に応じてdevelopにもRulesetを設定します。

コピー可能な **pnpm対応の完全なYAML例** と安全条件（`workflow_run`の同一リポジトリ判定を含む）は [共通セットアップガイド](https://github.com/naoiw/.github/blob/main/standards/NEW_WEB_APP_SETUP.md#c-main本番--developプレビュー両方を同時公開) を参照してください。古いv1.0.0の例を使用せず、[推奨Workflow SHA](https://github.com/naoiw/.github/blob/main/versions/workflows.json) を確認してください。

### 公開時の注意

- 共通Pages Workflowは `vite build --base=/<repo>/` に相当する処理を行います。通常のProject Pagesでは `vite.config.ts` のbase変更は不要ですが、アプリが記述した絶対アセットパスには注意してください。
- rootサイトや独自ドメインでは `base-path` 入力とPagesドメイン設定を公開先に合わせてください。
- PRで非公開の構成検証をする場合は `dry-run: true` を使用します。dry-runでも呼び出し側にPages用権限の宣言が必要です。
- SPAの直リンク/リロード、PWAキャッシュ、静的公開物への個人情報混入を個別に検証してください。

## AI指示

`AGENTS.md` などのAIルールを `naoiw/.github` の同期テンプレートから導入します。プロジェクト固有の指示は管理領域の外に記述します。

## Dependabot

`.github/dependabot.yml` はこのテンプレートから作成した新規リポジトリにも複製されます。pnpm管理の依存は `package-ecosystem: npm` で更新確認し、minor/patchのみグループ化、majorは個別PRにします。GitHub Actionsも月次確認します。**自動マージはしません**。

GitHub Settings → Advanced Security で `Dependency graph`、`Dependabot alerts`、`Dependabot security updates` が有効か確認します。共通workflowの参照SHA変更は、`naoiw/.github` の新しいリリースと動作検証を確認してから採用します。
