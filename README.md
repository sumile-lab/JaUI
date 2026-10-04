# JaUI

JaUIのSpecification、Reference Implementation、Testingを同じリポジトリで管理するmonorepoです。
Reference ImplementationにはLit + TypeScriptを使用します。
現在は開発環境の初期構成のみで、コンポーネントは未実装です。

## ディレクトリ構成

```text
JaUI/
├── README.md
├── LICENSE
├── specs/
│   ├── core/         # 共通仕様
│   ├── components/   # コンポーネント仕様
│   └── decisions/    # 設計判断の記録
└── packages/
    └── core/         # Lit + TypeScriptによるReference Implementation
        └── src/
```

仕様は`specs/`、対応する実装は`packages/core/src/`に配置します。
今後、仕様と実装の変更を同じコミットで追跡し、関連する仕様へのリンクを実装やテストに記載します。
テスト構成はコンポーネント実装と合わせて追加します。

## 開発環境の準備

- Node.js: **24.21.0**（`.nvmrc`と`package.json`の`engines`で固定）
- pnpm: **10.34.6**（`packageManager`と`engines`で固定）

Node.jsのバージョンマネージャー（例: nvm）をあらかじめ用意し、fresh clone後に以下を実行します。

```sh
git clone https://github.com/sumile-lab/JaUI.git
cd JaUI
nvm install
nvm use
npm install --global pnpm@10.34.6
pnpm install --frozen-lockfile
```

nvmを使用しない場合も、Node.js 24.21.0をインストールしてから同じpnpmの準備・依存関係のインストールを実行してください。
`.npmrc`でNode.js / pnpmの指定バージョンを検証します。依存関係の更新時は`pnpm install`でlockfileも更新してください。

## 開発コマンド

リポジトリのルートで実行します。

```sh
pnpm typecheck                  # workspace全体の型チェック
pnpm build                      # JavaScript・型定義・source mapを生成
pnpm dev                        # coreのTypeScriptを監視して再ビルド
pnpm --filter @jaui/core build   # coreのみビルド
pnpm list -r --depth 0           # workspaceと依存関係を確認
```

`packages/core`内でも`pnpm typecheck`、`pnpm build`、`pnpm dev`を実行できます。
ビルド成果物は`packages/core/dist/`に出力されます。
`pnpm dev`はTypeScriptのwatchモードです。ブラウザー用の開発サーバーはまだありません。

TypeScriptはstrictモードとES modulesを使用します。
Litのexperimental decoratorsを利用できるよう、`experimentalDecorators: true`と
`useDefineForClassFields: false`を設定しています（[Lit公式ドキュメント](https://lit.dev/docs/components/decorators/)）。
パッケージ内の相対importには、出力先に対応する`.js`拡張子を付けてください。
`src/index.ts`は将来の公開API用の空のエントリーポイントです。

## ライセンス

[MIT License](./LICENSE)
