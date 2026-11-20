# アーキテクチャ

- `src/main.tsx` — Reactのエントリポイント
- `src/App.tsx` — 画面ルート
- `src/styles.css` — 色・余白・レイアウトの初期CSS
- `public/` — 追加の静的ファイルを置く場合に作成する
- `src/components/`、`src/features/`、`src/lib/` — 必要になってから作る

過剰なフォルダや状態管理ライブラリを初期状態で追加しません。
設計が複雑になった場合は機能単位で分離してください。
