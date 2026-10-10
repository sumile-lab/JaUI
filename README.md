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

## 設計原則

[JaUI Design Principles v0.1](./specs/core/design-principles.md)は、
JaUIの設計・仕様策定・実装・レビューにおける最上位の判断基準です。
Core Specificationをはじめとする下位の仕様・設計判断は、この原則に基づきます。

## Core Specification

[JaUI Core Specification](./specs/core/core-specification.md)は、Design Principlesに基づき、
全コンポーネント・パターン・Reference Implementationに共通する横断的な要求を定義する文書です。
現在はVersion 0.1.0 / Status Draftで、Web標準を基盤とする`JAUI-WEB-001`、意味・セマンティクスを優先する`JAUI-WEB-002`、Web標準の振る舞い・インターフェースを尊重する`JAUI-WEB-003`、アクセシビリティを設計要件として扱う`JAUI-A11Y-001`、標準的なアクセシビリティ基準を参照する`JAUI-A11Y-002`、UIの意味・状態を支援技術へ公開する`JAUI-A11Y-003`を定義しています。
その他のCore要求は後続Issueで段階的に追加します。

## 開発環境の準備

- Node.js: **24.21.0**（`.nvmrc`と`package.json`の`engines`で固定）
- pnpm: **12.8.1**（`packageManager`と`engines`で固定）
- TypeScript: **7.0.2**（`packages/core/package.json`で固定）
- Lit: **3.3.3**（`packages/core/package.json`で固定）

Node.jsのバージョンマネージャー（例: nvm）をあらかじめ用意し、fresh clone後に以下を実行します。

```sh
git clone https://github.com/sumile-lab/JaUI.git
cd JaUI
nvm install
nvm use
npm install --global pnpm@12.8.1
pnpm install --frozen-lockfile
```

nvmを使用しない場合も、Node.js 24.21.0をインストールしてから同じpnpmの準備・依存関係のインストールを実行してください。
`.npmrc`でNode.js / pnpmの指定バージョンを検証します。依存関係の更新時は`pnpm install`でlockfileも更新してください。
固定しているpnpm 12.8.1は、pnpm自身とプロジェクトの依存関係を2つのYAML文書として`pnpm-lock.yaml`に記録します。これはpnpmが生成する正規の形式です。

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
ブラウザー向けのReference Implementationとして、`module: ESNext`と
`moduleResolution: Bundler`を使用します。ES modulesを保持し、パッケージの
`exports`を解決しつつ、Node.js固有の解決規則を前提にしない設定です
（[TypeScript公式ドキュメント](https://www.typescriptlang.org/tsconfig/moduleResolution.html)）。
バンドラーはまだ導入しておらず、将来のブラウザー向けビルド構成で選定します。
Litのexperimental decoratorsを利用できるよう、`experimentalDecorators: true`と
`useDefineForClassFields: false`を設定しています（[Lit公式ドキュメント](https://lit.dev/docs/components/decorators/)）。
相対importの拡張子はこの設定では必須ではありませんが、現在のビルドはバンドルせずに
出力するため、ブラウザーで直接読み込む相対importには出力先に対応する`.js`拡張子を付けてください。
`src/index.ts`は将来の公開API用の空のエントリーポイントです。

## ライセンス

[MIT License](./LICENSE)
