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
Version 0.1.0では文書管理情報と章構成を整備し、Web標準を基盤とする要求JAUI-WEB-001、意味・セマンティクスを優先する要求JAUI-WEB-002、Web標準の振る舞い・インターフェースを尊重する要求JAUI-WEB-003、アクセシビリティを設計要件として扱う要求JAUI-A11Y-001、標準的なアクセシビリティ基準を参照する要求JAUI-A11Y-002を定義します。

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

### JAUI-A11Y-001: アクセシビリティを設計要件として扱う

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則2「アクセシビリティを後付けしない。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-A11Y-001` で参照できます。

JAUI-WEB-001〜JAUI-WEB-003がWeb標準の利用、セマンティクスの選択、標準の振る舞い・インターフェースの尊重を扱うのに対し、本要求はアクセシビリティを設計段階から要求として扱い、下位仕様で明示することを扱います。

JaUIのComponent / Pattern SpecificationおよびReference Implementationは、アクセシビリティを実装後に追加する対応として扱わず、設計段階から要求として考慮しなければならない。

ComponentまたはPatternの意味、情報構造、状態、操作、視覚表現その他の利用方法を定義する際は、それらがアクセシビリティに与える影響を考慮しなければならない。

アクセシビリティ上の要求は、可能な範囲で下位仕様から確認・検証できる形で明示しなければならない。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- アクセシビリティが実装完了後の追加対応としてのみ扱われていない。
- 意味・情報構造・状態・操作・視覚表現を定義する段階で、アクセシビリティへの影響が検討されている。
- 下位仕様に必要なアクセシビリティ要求が、確認・検証可能な形で明示されている。
- 視覚上または実装上の都合だけを理由に、必要なアクセシビリティ要求が後回しにされていない。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法や適合判定手順は定義しません。

### JAUI-A11Y-002: 標準的なアクセシビリティ基準を参照する

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則2「アクセシビリティを後付けしない。」、原則3「「適合」より「検証可能性」を重視する。」、原則6「DADSを尊重するが、コピーにはしない。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-A11Y-002` で参照できます。

JAUI-A11Y-001がアクセシビリティを設計段階から扱い、下位仕様で明示することを扱うのに対し、本要求はアクセシビリティ要求の根拠となる外部基準、その具体化、およびJaUIの責務範囲を扱います。

JaUIのアクセシビリティ要求は、対象となる機能・利用方法に関連する標準的なアクセシビリティ仕様・ガイダンスを参照して定義しなければならない。

参照する外部基準は、JaUIの責務範囲とComponent / Patternの特性に応じて適用し、外部基準の要求をそのまま複製するのではなく、JaUIとして確認・検証可能な要求へ具体化しなければならない。

JaUIは、Component / PatternおよびReference Implementationとして提供・検証できる範囲を明確にし、利用先のWebコンテンツ全体に関するアクセシビリティ適合を、JaUI単体の利用だけを理由として保証してはならない。

#### 参照対象と責務範囲

主要な参照対象として、以下の標準・ガイダンスを対象となる機能・利用方法に応じて扱います。

- [W3C Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/)
- [WAI-ARIA](https://www.w3.org/TR/wai-aria/)
- [WAI-ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [HTML Standard](https://html.spec.whatwg.org/multipage/)および関連するWeb Platform仕様
- [デジタル庁デザインシステム（DADS）のアクセシビリティガイダンス](https://design.digital.go.jp/dads/guidance/accessibility/)
- その他、個別の要求に必要な標準・ガイダンス

参照時は、標準の要求とガイダンスの助言・例示を区別します。APGは関連仕様に基づくガイダンスとして扱います。
この一覧は、各文書の全要求を一括して取り込むことや、外部基準をJaUIの上位仕様として採用することを意味しません。
後続Requirementおよび個別Component / Pattern Specificationで、必要な項目を選択し、JaUIの要求として具体化します。

JaUI側では、提供する機能とその利用条件のもとで確認・検証できる事項を明確にします。
利用者側では、利用先固有のコンテンツ、Component / Patternの組み合わせ、およびページ全体の利用状況を踏まえた確認が必要です。
[WCAGの適合に関する説明](https://www.w3.org/WAI/WCAG22/Understanding/conformance)が示すページ全体や一連のプロセスの適合と、JaUIの提供範囲での検証は区別します。

本要求では、WCAGの具体的なバージョン・適合レベル・Success Criteriaとの対応、ARIA・キーボード・フォーカス等の個別要件は定義しません。
これらは後続Issueまたは個別Component / Pattern Specificationで定義します。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- アクセシビリティ要求の根拠となる標準・ガイダンスを説明できる。
- 外部基準を単に引用するだけでなく、JaUIとして確認・検証可能な要求へ具体化されている。
- Component / Pattern単体で確認できる事項と、利用先コンテンツ全体で確認すべき事項が区別されている。
- JaUIの提供範囲を超える適合を無条件に保証する表現になっていない。
- 外部基準との差異または追加要求がある場合、その理由を説明できる。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法や適合判定手順は定義しません。

本章のその他の要求・詳細は後続Issueで定義します。

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
| 0.1.0 | 文書管理情報、目的・適用範囲、仕様体系上の位置づけ、章構成を追加。Web標準を基盤とする要求JAUI-WEB-001とレビュー時の確認観点を追加。意味・セマンティクスを優先する要求JAUI-WEB-002とレビュー時の確認観点を追加。Web標準の振る舞い・インターフェースを尊重する要求JAUI-WEB-003とレビュー時の確認観点を追加。アクセシビリティを設計要件として扱う要求JAUI-A11Y-001とレビュー時の確認観点を追加。標準的なアクセシビリティ基準を参照する要求JAUI-A11Y-002、参照対象・責務範囲とレビュー時の確認観点を追加。 |
