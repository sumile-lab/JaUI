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
Version 0.1.0では文書管理情報と章構成を整備し、Web標準を基盤とする要求JAUI-WEB-001、意味・セマンティクスを優先する要求JAUI-WEB-002、Web標準の振る舞い・インターフェースを尊重する要求JAUI-WEB-003、アクセシビリティを設計要件として扱う要求JAUI-A11Y-001、標準的なアクセシビリティ基準を参照する要求JAUI-A11Y-002、UIの意味・状態を支援技術へ公開する要求JAUI-A11Y-003、キーボード操作可能性を確保する要求JAUI-A11Y-004、フォーカス順序と管理を適切に行う要求JAUI-A11Y-005、フォーカスの可視性を確保する要求JAUI-A11Y-006、状態変化・フィードバックを適切に伝達する要求JAUI-A11Y-007を定義します。

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

### JAUI-A11Y-003: UIの意味・状態を支援技術へ公開する

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則2「アクセシビリティを後付けしない。」、原則7「見た目より意味・セマンティクスを優先する。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-A11Y-003` で参照できます。

JAUI-A11Y-001はアクセシビリティを設計段階から扱い、下位仕様で明示することを扱い、JAUI-A11Y-002は外部基準を根拠としてJaUIの責務範囲へ具体化することを扱います。
JAUI-WEB-002がUIの目的・役割・期待される振る舞いに対応するセマンティクスの選択を扱うのに対し、本要求は利用者に必要な意味情報を支援技術へ公開することを扱います。
本要求は初期状態だけでなく、状態・値等の更新後も必要な意味情報を取得可能にすることを扱います。
JAUI-A11Y-007は、これを前提として、利用者が変化や処理結果を認識できる伝達方法とタイミングを扱います。

JaUIのComponent / Pattern SpecificationおよびReference Implementationは、利用者がUIを理解または操作するために必要な目的、役割、名前、状態、値その他の意味情報を、支援技術から取得可能な形で公開しなければならない。

これらの情報は、可能な場合は標準HTML要素その他のWeb標準が提供するネイティブなセマンティクスによって表現しなければならない。

ネイティブなセマンティクスだけでは必要な意味情報を表現できない場合は、関連するWAI-ARIA等の仕様・ガイダンスに基づいて補完しなければならない。

#### 外部基準との関係・対象範囲

本要求は、JAUI-A11Y-002に基づき、少なくとも以下の標準・ガイダンスを参照して具体化します。

- [WCAG 2.x Success Criterion 4.1.2 Name, Role, Valueの解説](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html)
- [WAI-ARIA](https://www.w3.org/TR/wai-aria/)
- [WAI-ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [HTML Standard](https://html.spec.whatwg.org/multipage/)および関連するWeb Platform仕様
- [デジタル庁デザインシステム（DADS）のアクセシビリティガイダンス](https://design.digital.go.jp/dads/guidance/accessibility/)

標準の要求とガイダンスの助言・例示を区別し、APGおよびWCAGの解説はガイダンスとして扱います。
本要求は必要な意味情報の公開を扱い、情報ごとに専用のARIA属性を要求するものではありません。
また、WCAG 4.1.2全体や利用先のWebコンテンツ全体への適合を保証するものではありません。

本要求では、個別ComponentのAccessible Name算出方法、個別のARIA role / state / propertyの割り当て、aria-label / aria-labelledby / aria-describedby等の利用ルール、Live Region、Screen Reader固有の読み上げ結果は定義しません。
キーボード操作、フォーカス管理・表示、色・コントラスト、Pointer / Touch Target、Motion / Animationの具体要件も定義しません。
これらは後続Issueまたは個別Component / Pattern Specificationで定義します。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- Component / Patternの目的・役割が支援技術から判別可能である。
- 利用者が識別するために必要な名前が、支援技術から取得可能である。
- 操作や理解に必要な状態・値等が、必要に応じて支援技術から取得可能である。
- 標準HTML等が提供するネイティブなセマンティクスを不要に上書き・置換していない。
- ARIA等を使用する場合、その必要性と適用するrole / state / property等の根拠を説明できる。
- 視覚的表現だけに依存して意味・状態を伝えていない。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法、支援技術ごとの検証手順や適合判定手順は定義しません。

### JAUI-A11Y-004: キーボード操作可能性を確保する

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則1「Web標準を置き換えない。拡張する。」、原則2「アクセシビリティを後付けしない。」、原則3「「適合」より「検証可能性」を重視する。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-A11Y-004` で参照できます。

JAUI-WEB-001はWeb標準を基盤とする判断、JAUI-WEB-002はセマンティクスの選択、JAUI-WEB-003は標準の状態・操作・イベント等の契約維持を扱います。
本要求は、これらをキーボード操作に具体化し、適用可能な標準の操作モデルを尊重するとともに、利用者が操作する機能のキーボードからの利用可能性を扱います。
JAUI-A11Y-001は設計段階からのアクセシビリティ要求、JAUI-A11Y-002は外部基準の参照と責務範囲、JAUI-A11Y-003は意味・状態の支援技術への公開を扱います。
本要求では、意味情報の公開に加えて、機能をキーボードから操作可能とすることを要求します。

JaUIのComponent / Pattern SpecificationおよびReference Implementationは、利用者が操作する機能について、ポインティングデバイスを必須とせず、キーボードから利用可能であることを要求しなければならない。

標準HTMLその他のWeb標準が提供するキーボード操作の振る舞いが適用できる場合、それを尊重し、不必要に独自の操作モデルへ置き換えてはならない。

独自の操作モデルが必要な場合は、その必要性を説明し、対象となるComponent / Patternの性質と関連するアクセシビリティ基準・ガイダンスを踏まえ、期待されるキーボード操作を下位仕様で明示しなければならない。

#### 外部基準との関係・対象範囲

本要求は、JAUI-A11Y-002に基づき、少なくとも以下の標準・ガイダンスを参照して具体化します。

- [WCAG 2.2 Success Criterion 2.1.1 Keyboard](https://www.w3.org/TR/WCAG22/#keyboard)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html)
- [WCAG 2.2 Success Criterion 2.1.2 No Keyboard Trap](https://www.w3.org/TR/WCAG22/#no-keyboard-trap)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap.html)
- [WAI-ARIA APG: Developing a Keyboard Interface](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/)
- [HTML Standard](https://html.spec.whatwg.org/multipage/interaction.html)および関連するWeb Platform仕様
- [デジタル庁デザインシステム（DADS）のアクセシビリティガイダンス](https://design.digital.go.jp/dads/guidance/accessibility/)

WCAGの達成基準およびHTML Standardの規範的要求と、WCAGの解説、APG、DADSのガイダンスによる助言・例示を区別します。
これらの文書の全要求を一括して取り込むものではなく、本要求単独でWCAG 2.1.1・2.1.2全体や利用先のWebコンテンツ全体への適合を保証するものではありません。
WCAGのバージョン・適合レベルに関する全体方針も、本要求では確定しません。

Keyboard Trapについては、キーボードだけで操作対象から離脱または終了でき、操作不能な状態に閉じ込められないことをレビューで確認します。
操作中のフォーカスを一定の範囲に制限すること自体を禁止するものではなく、キーボードによる離脱・終了が可能であることと、独自の離脱操作が必要な場合に利用者がその方法を知ることができることを確認します。
具体的な離脱キーやフォーカス移動先は、JAUI-A11Y-005等の関連要求を踏まえて下位仕様で定義します。

本要求はキーボード操作の成立に不可欠なフォーカスの存在を前提としますが、フォーカス順序・移動・維持・復帰の横断要求はJAUI-A11Y-005で扱い、フォーカスの可視性はJAUI-A11Y-006で扱います。
個別Componentのキー割当、roving tabindex / aria-activedescendant等の実装手法、個別のARIA role / state / property、ショートカットの衝突回避・カスタマイズ、実機・Screen Reader別の試験手順は定義しません。
個別Componentの実装、テストコード、Lit等のフレームワークに依存するAPIも、本要求の対象に含めません。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- 利用者が操作する機能について、キーボードから利用可能であることが要求されている。
- マウス・タッチ・ホバーだけを必須の操作手段としていない。
- 適用可能な標準HTMLその他のWeb標準のキーボード操作を不要に妨げていない。
- 独自の操作モデルが必要な場合、その理由と期待されるキーボード操作を下位仕様で説明できる。
- キーボードだけで操作対象から離脱または終了でき、操作不能な状態に閉じ込められないことが考慮されている。独自の離脱操作が必要な場合、利用者がその方法を知ることができる。
- 必要なキーボード操作の要求と確認観点が、要求ID `JAUI-A11Y-004` を通じて下位仕様から追跡可能である。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法、環境別の検証手順や適合判定手順は定義しません。

### JAUI-A11Y-005: フォーカス順序と管理を適切に行う

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則1「Web標準を置き換えない。拡張する。」、原則2「アクセシビリティを後付けしない。」、原則3「「適合」より「検証可能性」を重視する。」、原則4「フレームワークに依存しない。」、原則7「見た目より意味・セマンティクスを優先する。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-A11Y-005` で参照できます。

JAUI-WEB-001はWeb標準を基盤とする判断、JAUI-WEB-002はセマンティクスの選択、JAUI-WEB-003は標準の状態・操作・イベント等の契約維持を扱います。
本要求は、これらをフォーカス順序と管理に具体化します。
JAUI-A11Y-001は設計段階からのアクセシビリティ要求、JAUI-A11Y-002は外部基準の参照と責務範囲、JAUI-A11Y-003は意味・状態の支援技術への公開を扱います。
JAUI-A11Y-004が機能のキーボードからの利用可能性と離脱・終了を含むKeyboard Trap回避を扱うのに対し、本要求は操作対象への合理的な到達と、状態変化に伴うフォーカス移動・維持・復帰による操作の継続を扱います。

JaUIのComponent / Pattern SpecificationおよびReference Implementationは、キーボード等によるフォーカス移動が、対象となるUIの意味、情報構造および操作の流れと整合するように設計しなければならない。

Component / Patternの表示・非表示、状態変化、操作の開始・終了等に伴ってフォーカス管理が必要な場合、利用者が操作を継続できるよう、適切なフォーカス移動・維持・復帰の条件を下位仕様で明示しなければならない。

標準HTMLその他のWeb標準が提供するフォーカスの振る舞いを尊重し、合理的な理由なくフォーカス順序や移動を妨げる独自の仕組みへ置き換えてはならない。

#### 外部基準との関係・対象範囲

本要求は、JAUI-A11Y-002に基づき、少なくとも以下の標準・ガイダンスを参照して具体化します。

- [WCAG 2.2 Success Criterion 2.4.3 Focus Order](https://www.w3.org/TR/WCAG22/#focus-order)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/focus-order.html)
- [WCAG 2.2 Success Criterion 2.1.2 No Keyboard Trap](https://www.w3.org/TR/WCAG22/#no-keyboard-trap)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap.html)
- [WAI-ARIA APG: Developing a Keyboard Interface](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/)
- [HTML Standard — Focus](https://html.spec.whatwg.org/multipage/interaction.html#focus)
- [デジタル庁デザインシステム（DADS）のアクセシビリティガイダンス](https://design.digital.go.jp/dads/guidance/accessibility/)

WCAGの達成基準およびHTML Standardの規範的要求と、WCAGの解説、APG、DADSのガイダンスによる助言・例示を区別します。
SC 2.4.3は意味・操作可能性を保つ順序の根拠として、SC 2.1.2はJAUI-A11Y-004の離脱・終了要求との関係を確認するために参照します。
フォーカスを一定の範囲に制限すること自体を禁止するものではなく、JAUI-A11Y-004に従ってキーボードによる離脱・終了が可能であることを前提とします。
これらの文書の全要求を一括して取り込むものではなく、本要求単独でWCAG 2.4.3・2.1.2全体や利用先のWebコンテンツ全体への適合を保証するものではありません。
WCAGのバージョン・適合レベルに関する全体方針も、本要求では確定しません。

JaUI側は、提供するComponent / Patternの利用条件におけるフォーカス順序・管理の条件と、利用先アプリケーション側で決定する事項を下位仕様で明示します。
利用先側は、固有のコンテンツ構成、Component / Patternの組み合わせ、画面遷移等を踏まえ、ページ全体のフォーカス順序と操作の継続を確認します。

本要求では、フォーカスインジケーターの視覚的な表示・コントラスト・面積・遮蔽は定義せず、可視性の横断要求はJAUI-A11Y-006で扱います。
個別ComponentのTab / 矢印キー / Escape等のキー割当、モーダルやメニュー等の初期フォーカス位置・復帰先、roving tabindex / aria-activedescendant等の実装手法、個別のARIA属性設計も定義しません。
テストツール・ブラウザー・支援技術ごとの詳細手順、個別Componentの実装、テストコード、Lit等のフレームワークに依存するAPIは、本要求の対象に含めません。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- フォーカス順序がUIの意味・情報構造・操作の流れに沿っている。
- フォーカスを必要とする操作対象に到達し、操作を継続できる。
- 開閉・表示切替・終了等の状態変化に伴うフォーカス移動・維持・復帰の条件が、必要に応じて下位仕様で明示されている。
- 標準HTML等が提供するネイティブなフォーカス挙動を不要に妨げていない。
- 独自のフォーカス制御が必要な場合、その理由を説明できる。
- Component / Pattern側の責務と、利用先アプリケーション側で決定する責務が区別されている。
- 必要なフォーカス順序・管理の要求と確認観点が、要求ID `JAUI-A11Y-005` を通じて下位仕様から追跡可能である。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法、環境別の検証手順や適合判定手順は定義しません。

### JAUI-A11Y-006: フォーカスの可視性を確保する

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則1「Web標準を置き換えない。拡張する。」、原則2「アクセシビリティを後付けしない。」、原則3「「適合」より「検証可能性」を重視する。」、原則4「フレームワークに依存しない。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-A11Y-006` で参照できます。

JAUI-WEB-001はWeb標準を基盤とする判断、JAUI-WEB-002はセマンティクスの選択、JAUI-WEB-003は標準の状態・操作・イベント等の契約維持を扱います。
本要求は、これらに基づいて標準のフォーカス表示を尊重し、現在のフォーカス位置の視覚的な識別可能性を扱います。
JAUI-A11Y-001は設計段階からのアクセシビリティ要求、JAUI-A11Y-002は外部基準の参照と責務範囲、JAUI-A11Y-003は意味・状態の支援技術への公開を扱います。
JAUI-A11Y-004は機能のキーボードからの利用可能性とKeyboard Trap回避、JAUI-A11Y-005はフォーカス順序・移動・維持・復帰を扱います。
本要求は、操作可能性やフォーカス管理とは分離して、キーボード操作中に現在フォーカスされている対象を視覚的に識別できることを要求します。

JaUIのComponent / Pattern SpecificationおよびReference Implementationは、キーボード操作時にフォーカスを受ける対象について、利用者が現在のフォーカス位置を視覚的に識別できるようにしなければならない。

標準HTML要素およびブラウザーが提供するフォーカス表示を合理的な理由なく除去・抑制してはならない。
独自のフォーカス表示を設ける場合は、対象や状態を識別できる視認性を確保し、その要件を下位仕様で明示しなければならない。
標準表示を変更する合理的な理由がある場合も、現在のフォーカス位置の視覚的な識別可能性を確保しなければならない。

JaUIが提供するComponent / Patternの構造・スタイル・表示制御によって、フォーカスインジケーターが不必要に隠れたり識別不能になったりしないようにしなければならない。

#### 外部基準との関係・対象範囲

本要求は、JAUI-A11Y-002に基づき、以下の標準・ガイダンスを参照して具体化します。

- [WCAG 2.2 Success Criterion 2.4.7 Focus Visible（AA）](https://www.w3.org/TR/WCAG22/#focus-visible)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html)
- [WCAG 2.2 Success Criterion 2.4.11 Focus Not Obscured (Minimum)（AA）](https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html)
- [WCAG 2.2 Success Criterion 1.4.11 Non-text Contrast（AA）](https://www.w3.org/TR/WCAG22/#non-text-contrast)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)
- [WCAG 2.2 Success Criterion 2.4.13 Focus Appearance（AAA）](https://www.w3.org/TR/WCAG22/#focus-appearance)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance.html) — 参考情報
- [HTML Standard — Focus](https://html.spec.whatwg.org/multipage/interaction.html#focus)
- [デジタル庁デザインシステム（DADS）のアクセシビリティガイダンス](https://design.digital.go.jp/dads/guidance/accessibility/)

WCAGの達成基準およびHTML Standardの規範的要求と、WCAGの解説、DADSのガイダンスによる助言・例示を区別します。
SC 2.4.7はフォーカス表示の可視性の根拠として参照します。
SC 2.4.11はフォーカスを受ける対象自体が作成者のコンテンツによって完全に隠れないことを扱う基準であり、フォーカスインジケーターの完全な非遮蔽を要求する基準としては扱いません。
対象が部分的に見えていても、現在のフォーカス位置を識別できるかは別途確認します。
SC 1.4.11は独自のフォーカス表示の視認性に関連する基準として、隣接する色とのコントラストや、ユーザーエージェントが決定し作成者が変更していない表示等の例外を含め、その適用範囲を確認します。
SC 2.4.13はAAAの参考情報として扱い、面積等の数値基準をAAの必須条件として導入しません。
これらの文書の全要求を一括して取り込むものではなく、本要求単独で各達成基準全体や利用先のWebコンテンツ全体への適合を保証するものではありません。
WCAGのバージョン・適合レベルに関する全体方針も、本要求では確定しません。

JaUI側は、提供するComponent / Patternの利用条件におけるフォーカス表示の視認性と、自身が制御する構造・スタイル・表示制御による不要な遮蔽の回避を扱います。
下位仕様では、確認した色・背景・状態等の利用条件と、利用先アプリケーション側で決定・確認する事項を明示します。
利用先側は、固有の背景、追加CSS、レイアウト、スクロール、重なり順、Component / Patternの組み合わせ等を踏まえ、ページ全体でフォーカス位置を識別できるか確認します。
利用先固有の条件による遮蔽と、JaUI自身が生じさせる遮蔽を区別し、JaUI単体で制御できない条件まで無条件に保証しません。

本要求では、フォーカス順序・移動・維持・復帰の詳細、Component固有のリングの太さ・形・余白・色の具体値やDesign Token割当、CSS実装・フォーカス制御コードは定義しません。
利用先アプリケーション全体のスクロール・重なり順・適合判定、実機・ブラウザー・支援技術ごとの詳細試験手順、Lit等のフレームワークに依存するAPIも、本要求の対象に含めません。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- キーボード操作時に、現在のフォーカス位置を視覚的に識別できる。
- 標準HTML要素・ブラウザーが提供するネイティブなフォーカス表示を合理的な理由なく消していない。
- 独自のフォーカス表示を用いる場合、対象や状態を識別できる視認性の条件を下位仕様で説明できる。
- JaUI自身の構造・スタイル・表示制御により、フォーカス表示を不必要に隠したり識別不能にしたりしていない。
- 色・背景・状態等の変化も踏まえて、現在のフォーカス位置の識別可能性を確認できる。
- 利用先固有のレイアウトや重なり順による遮蔽等について、JaUI側と利用先側の責務・利用条件が区別されている。
- 必要なフォーカス可視性の要求と確認観点が、要求ID `JAUI-A11Y-006` を通じて下位仕様から追跡可能である。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法、環境別の検証手順や適合判定手順は定義しません。

### JAUI-A11Y-007: 状態変化・フィードバックを適切に伝達する

本要求は、[JaUI Design Principles v0.1](./design-principles.md)の原則1「Web標準を置き換えない。拡張する。」、原則2「アクセシビリティを後付けしない。」、原則3「「適合」より「検証可能性」を重視する。」、原則4「フレームワークに依存しない。」、原則6「DADSを尊重するが、コピーにはしない。」、原則7「見た目より意味・セマンティクスを優先する。」を具体化する共通要求です。
Component / Pattern SpecificationおよびReference Implementationから、要求ID `JAUI-A11Y-007` で参照できます。

JAUI-WEB-001はWeb標準を基盤とする判断、JAUI-WEB-002はセマンティクスの選択、JAUI-WEB-003は標準の状態・操作・イベント等の契約維持を扱います。
本要求は、これらに基づいて、動的な状態変化・処理結果・フィードバックの認識可能性と伝達タイミングを扱います。
JAUI-A11Y-001は設計段階からのアクセシビリティ要求、JAUI-A11Y-002は外部基準の参照と責務範囲を扱います。
JAUI-A11Y-003は更新後の状態・値等を含む意味情報の支援技術への公開を扱い、本要求はその公開を前提として、必要な変化や結果を利用者が適切なタイミングで認識できる伝達方法を扱います。
JAUI-A11Y-004はキーボード操作可能性とKeyboard Trap回避、JAUI-A11Y-005はフォーカス順序・移動・維持・復帰、JAUI-A11Y-006はフォーカスの可視性を扱います。
通知が操作やフォーカスへ与える影響はこれらの要求を踏まえて検討し、既存要求を再定義しません。

JaUIのComponent / Pattern SpecificationおよびReference Implementationは、利用者の理解または次の操作に影響する状態変化、処理結果およびフィードバックについて、利用者が適切なタイミングで認識できる伝達方法を設計しなければならない。

伝達方法は、情報の重要度、緊急性、操作文脈および支援技術による利用を考慮し、視覚的な変化のみに依存してはならない。

動的な通知が必要な場合は、関連するWeb標準およびアクセシビリティ基準・ガイダンスを踏まえ、通知すべき条件と情報、利用者の操作・フォーカスへの影響、JaUIと利用先の責務を下位仕様で明示しなければならない。

#### 外部基準との関係・対象範囲

本要求は、JAUI-A11Y-002に基づき、以下の標準・ガイダンスを参照して具体化します。

- [WCAG 2.2 Success Criterion 4.1.3 Status Messages（AA）](https://www.w3.org/TR/WCAG22/#status-messages)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html)
- [WCAG 2.2 Success Criterion 4.1.2 Name, Role, Value（A）](https://www.w3.org/TR/WCAG22/#name-role-value)および[その解説](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html)
- [WAI-ARIA](https://www.w3.org/TR/wai-aria/)
- [WAI-ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [HTML Standard](https://html.spec.whatwg.org/multipage/)および関連するWeb Platform仕様
- [デジタル庁デザインシステム（DADS）のアクセシビリティガイダンス](https://design.digital.go.jp/dads/guidance/accessibility/)

WCAGの達成基準、WAI-ARIAおよびHTML Standardの規範的要求と、WCAGの解説、APG、DADSのガイダンスによる助言・例示を区別します。
SC 4.1.3のステータスメッセージは、文脈の変化を伴わず、操作の成功・結果、アプリケーションの待機状態、処理の進行、エラーの存在を伝える内容の変化を指します。
マークアップ言語で実装したコンテンツにおける該当メッセージについて、フォーカスを受けずに支援技術が利用者へ提示できるよう、役割またはプロパティを通じてプログラムから判定可能にすることを根拠として参照します。
一般的なUI状態変化すべてをSC 4.1.3のステータスメッセージとして扱うものではありません。
本要求は、非同期処理の完了、保存成功・失敗、検証結果、読み込み状態の変化等から、利用者の理解や次の操作に影響する情報を特定し、その伝達方法を設計することを扱います。
すべての状態変化への一律のライブ通知や、既存のセマンティクスによる伝達に加えて常に別の通知を設けることは要求しません。
SC 4.1.2は状態・値等の変更通知も含む基準であり、JAUI-A11Y-003を静的な意味情報だけの要求として扱いません。

これらの文書の全要求を一括して取り込むものではなく、本要求単独でSC 4.1.2・4.1.3全体や利用先のWebコンテンツ全体への適合を保証するものではありません。
WCAGのバージョン・適合レベルに関する全体方針も、本要求では確定しません。

JaUI側は、提供する伝達・通知の仕組み、その利用条件、操作・フォーカスへの影響と、利用先側が決定する事項を下位仕様で明示します。
利用先側は、アプリケーション固有のイベント、通知文言、発生タイミング、Component / Patternの組み合わせを踏まえ、画面全体で必要な情報が適切に伝わることを確認します。
具体的な責務分担は、提供する機能と利用条件に応じて下位仕様で明示し、JaUI単体で制御できない条件まで無条件に保証しません。
通知を認識させるためだけの不必要なフォーカス移動や操作妨害を避ける観点を持ち、フォーカス管理が必要な場合はJAUI-A11Y-005に基づいて下位仕様で条件を明示します。

本要求では、aria-live、role=status、role=alert等の個別割当・優先度・読み上げ仕様、個別Componentの通知文言・表示時間・トースト配置・非同期処理APIは定義しません。
フォームの個別エラー表示・入力補助・検証ルール、色だけに依存しない情報伝達・コントラストの詳細は後続要求で扱います。
フォーカス順序・管理と可視性の再定義、実機・ブラウザー・Screen Reader別の詳細試験手順、個別Componentの実装、テストコード、Lit等のフレームワークに依存するAPIも、本要求の対象に含めません。

#### 検証可能性

下位仕様またはReference Implementationのレビューでは、少なくとも以下を確認できることを目指します。

- 利用者に伝達すべき状態変化・処理結果・フィードバックが特定されている。
- 情報の重要度・緊急性と操作文脈に応じて、伝達方法とタイミングを説明できる。
- 必要な情報を視覚的な変化だけに依存させていない。
- 支援技術への伝達が必要な場合、適用する標準・ガイダンスとその適用範囲の根拠を説明できる。
- 通知による不必要なフォーカス移動や操作妨害を避ける観点がある。
- JaUIが提供する伝達・通知の仕組みと、利用先が与える文言・タイミング・イベントの責務が区別されている。
- 必要な伝達の要求と確認観点が、要求ID `JAUI-A11Y-007` を通じて下位仕様から追跡可能である。

ここではレビュー時の確認観点のみを示し、具体的なテスト方法、環境別の検証手順や適合判定手順は定義しません。

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
| 0.1.0 | 文書管理情報、目的・適用範囲、仕様体系上の位置づけ、章構成を追加。Web標準を基盤とする要求JAUI-WEB-001とレビュー時の確認観点を追加。意味・セマンティクスを優先する要求JAUI-WEB-002とレビュー時の確認観点を追加。Web標準の振る舞い・インターフェースを尊重する要求JAUI-WEB-003とレビュー時の確認観点を追加。アクセシビリティを設計要件として扱う要求JAUI-A11Y-001とレビュー時の確認観点を追加。標準的なアクセシビリティ基準を参照する要求JAUI-A11Y-002、参照対象・責務範囲とレビュー時の確認観点を追加。UIの意味・状態を支援技術へ公開する要求JAUI-A11Y-003、外部基準との関係・対象範囲とレビュー時の確認観点を追加。キーボード操作可能性を確保する要求JAUI-A11Y-004、外部基準との関係・対象範囲とKeyboard Trap回避を含むレビュー時の確認観点を追加。フォーカス順序と管理を適切に行う要求JAUI-A11Y-005、外部基準との関係・対象範囲、利用先との責務境界とレビュー時の確認観点を追加。JAUI-A11Y-004のフォーカス関連要求への参照を更新。フォーカスの可視性を確保する要求JAUI-A11Y-006、外部基準との関係・対象範囲、利用先との責務境界とレビュー時の確認観点を追加。JAUI-A11Y-004・JAUI-A11Y-005の可視性要求への参照を更新。状態変化・フィードバックを適切に伝達する要求JAUI-A11Y-007、外部基準との関係・対象範囲、利用先との責務境界とレビュー時の確認観点を追加。JAUI-A11Y-003に更新後の意味情報の公開とJAUI-A11Y-007との関係を明記。 |
