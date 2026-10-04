# JaUI Design Principles v0.1

## 目的・位置づけ

Design Principlesは、JaUIの設計・仕様策定・実装・レビューにおける最上位の判断基準です。
個別コンポーネントや実装技術の都合に引っ張られず、一貫した設計判断を行うための原則として扱います。

具体的な実装方法を規定するものではなく、下位の仕様・設計判断が迷った場合の判断基準とします。

## 仕様体系

JaUIの仕様体系は以下の順序を基本とします。

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

## Design Principles v0.1

1. Web標準を置き換えない。拡張する。
2. アクセシビリティを後付けしない。
3. 「適合」より「検証可能性」を重視する。
4. フレームワークに依存しない。
5. 日本のWeb利用を第一級のユースケースとして扱う。
6. DADSを尊重するが、コピーにはしない。
7. 見た目より意味・セマンティクスを優先する。
8. カスタマイズ可能だが、壊しやすくしない。
9. AIが正しく使えるAPIを目指す。
10. 少数の高品質コンポーネントを優先する。
