# JaUI Core Specification

## 1. 文書管理情報

| 項目 | 値 |
|---|---|
| Document ID | JAUI-CORE-001 |
| Title | JaUI Core Specification |
| Version | 0.1.0 |
| Status | Draft |

## 2. 目的・適用範囲

Core Specificationは、全コンポーネント・パターン・Reference Implementationに共通する横断的な要求を定義する文書です。
要求は後続Issueで段階的に追加し、小さな単位でレビューできるようにします。
Version 0.1.0では文書管理情報と章構成を整備し、Web標準を基盤とする要求JAUI-WEB-001、意味・セマンティクスを優先する要求JAUI-WEB-002、Web標準の振る舞い・インターフェースを尊重する要求JAUI-WEB-003を定義します。

本仕様は、最上位の判断基準である[JaUI Design Principles v0.1](./design-principles.md)の直下に位置します。
Design Principlesに基づいて共通要求を定義し、原則の内容を重複して再定義しません。
個別コンポーネント仕様やLit固有の実装仕様は、本仕様の対象に含めません。

仕様体系は以下の順序を基本とします。

```text
JaUI Design Principles
        ↓
JaUI Core Specification
        ↓
Component / Pattern Specification
        ↓
Decision Records
        ↓
Reference Implementation
        ↓
Test Specification / Results
```

## 3. Web Standards

### JAUI-WEB-001: Web標準を基盤とする

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則1「Web標準を置き換えない。拡張する。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-WEB-001` で参照できます。

JaUIの仕様およびReference Implementationは、Web標準が提供する既存の意味、振る舞い、機能を基盤として使用しなければならない。

同等の目的を満たすWeb標準の仕組みが存在する場合、合理的な理由なく独自の仕組みで置き換えてはならない。

独自の抽象化または実装を採用する場合、その必要性を説明可能でなければならない。
JaUIによる抽象化または拡張は、基盤となるWeb標準との関係を説明可能でなければならない。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- 対象となる標準HTML要素やWeb Platformの機能が存在するか検討されている。
- 独自の抽象化・実装を採用する場合、その必要性を説明できる。
- 基盤となるWeb標準との関係を説明でき、その意味や期待される振る舞いを不必要に失っていない。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法や適合判定手順は定義しません。

### JAUI-WEB-002: 意味・セマンティクスを優先する

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則7「見た目より意味・セマンティクスを優先する。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-WEB-002` で参照できます。

JAUI-WEB-001がWeb標準を基盤として使用することと独自実装の必要性の説明を扱うのに対し、本要求はUIの目的・役割・期待される振る舞いに対応するセマンティクスの選択を扱います。

JaUIの仕様およびReference Implementationは、UIの視覚表現ではなく、その目的、役割、期待される振る舞いに基づいて、適切なWeb標準の意味・セマンティクスを選択しなければならない。

スタイルまたは視覚上の類似性のみを理由として、本来の目的と異なる意味を持つHTML要素またはWeb Platformの仕組みを使用してはならない。

JaUIによる抽象化またはスタイリングは、基盤となるWeb標準の意味を不必要に変更または曖昧にしてはならない。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- UIの目的・役割・期待される振る舞いが明確になっている。
- 採用する標準HTML要素やWeb Platformの仕組みが、その意味に基づいて選択されている。
- 視覚表現やスタイル上の都合だけで、本来の目的と異なるセマンティクスを採用していない。
- JaUIの抽象化やスタイリングによって、基盤となる意味が不必要に失われたり曖昧になったりしていない。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法や適合判定手順は定義しません。

### JAUI-WEB-003: Web標準の振る舞い・インターフェースを尊重する

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則1「Web標準を置き換えない。拡張する。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-WEB-003` で参照できます。

JAUI-WEB-001はWeb標準を基盤として使用することと独自実装の必要性の説明を扱い、JAUI-WEB-002はUIの目的・役割・期待される振る舞いに対応するセマンティクスの選択を扱います。
本要求は、これらに基づいて適切なWeb標準を選択した後に、その標準が提供する既存の状態・操作・イベント等の契約を維持することを扱います。

JaUIの仕様およびReference Implementationは、基盤となるWeb標準が提供する既存の状態、操作、イベントその他のインターフェースを尊重しなければならない。

同等の目的を満たすWeb標準の振る舞いまたはインターフェースが存在する場合、合理的な理由なく、それと矛盾する独自のモデルへ置き換えてはならない。

JaUIによる抽象化または拡張は、基盤となるWeb標準から利用者が合理的に期待する振る舞いを不必要に変更してはならない。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- 基盤となるWeb標準が提供する状態・操作・イベント等が確認されている。
- 既存のWeb標準で表現可能なものに対して、不要な独自モデルを導入していない。
- 独自の抽象化・拡張を採用する場合、標準の仕組みをそのまま利用できない理由を説明できる。
- 抽象化・拡張によって、基盤となるWeb標準から期待される振る舞いが不必要に失われたり変更されたりしていない。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法や適合判定手順は定義しません。

本章のその他の要求・詳細は後続Issueで定義します。

## 4. Accessibility

本章の要求・詳細は後続Issueで定義します。

## 5. Theme

本章の要求・詳細は後続Issueで定義します。

## 6. Internationalization

本章の要求・詳細は後続Issueで定義します。

## 7. Localization

本章の要求・詳細は後続Issueで定義します。

## 8. Bidirectional Text

本章の要求・詳細は後続Issueで定義します。

## 9. Design Tokens

本章の要求・詳細は後続Issueで定義します。

## 10. Interoperability

本章の要求・詳細は後続Issueで定義します。

## 11. Japanese Web UX

本章の要求・詳細は後続Issueで定義します。

## 12. AI Usage

本章の要求・詳細は後続Issueで定義します。

## 13. Testing

本章の要求・詳細は後続Issueで定義します。

## 14. Conformance

本章の要求・詳細は後続Issueで定義します。

## 15. Specification Feedback Process

本章の要求・詳細は後続Issueで定義します。

## 16. Change History

| Version | 変更内容 |
|---|---|
| 0.1.0 | 文書管理情報、目的・適用範囲、仕様体系上の位置づけ、章構成を追加。Web標準を基盤とする要求JAUI-WEB-001とレビュー時の確認観点を追加。意味・セマンティクスを優先する要求JAUI-WEB-002とレビュー時の確認観点を追加。Web標準の振る舞い・インターフェースを尊重する要求JAUI-WEB-003とレビュー時の確認観点を追加。 |
