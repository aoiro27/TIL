https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/long-context-tips

# 長文（ロングコンテキスト）プロンプト設計のコツ

## 概要

Claude 3シリーズは最大20万トークンの長大なコンテキストウィンドウを持ち、大量のデータや複雑なタスクに対応できます。  
このページは、長文や大量ドキュメントを扱う際にClaudeの性能を最大限に引き出すためのテクニックを解説しています。

---

## 長文プロンプトの基本テクニック

### 1. **長文データはプロンプトの冒頭に置く**

- 2万トークン以上の長文や大量データは**プロンプトの最上部**に配置し、その後にクエリや指示、例を書くのが効果的です。
- これにより、Claudeの出力品質が最大30％向上することもあります。

### 2. **ドキュメントはXMLタグで構造化する**

- 複数ドキュメントを扱う場合は、各ドキュメントを`<document>`タグで囲み、`<document_content>`, `<source>`などのサブタグで内容やメタデータを明示します。

**例：**
```xml
<documents>
  <document index="1">
    <source>annual_report_2023.pdf</source>
    <document_content>
      {{ANNUAL_REPORT}}
    </document_content>
  </document>
  <document index="2">
    <source>competitor_analysis_q2.xlsx</source>
    <document_content>
      {{COMPETITOR_ANALYSIS}}
    </document_content>
  </document>
</documents>
Analyze the annual report and competitor analysis. Identify strategic advantages and recommend Q3 focus areas.
```

### 3. **引用で根拠を明示させる**

- 長文ドキュメントから要素を抽出・分析させる場合、まず「該当箇所を引用させてから」分析や要約をさせると、ノイズを減らし、根拠のある出力が得られます。

**例：**
- 「まず該当箇所を<quotes>タグで抜き出し、その後<info>タグで分析結果をまとめよ」と指示

---

## その他ポイント

- **複数ドキュメントや大量データの際は、XMLタグで明確に区切ることでClaudeの誤解や混同を防げる**
- **クエリや指示はプロンプトの末尾に置くと効果的**
- **長文コンテキストは、構造化・明示的なラベル付け・引用指定がカギ**

---

## 参考

- [プロンプトライブラリ](https://docs.anthropic.com/en/resources/prompt-library/library)
- [GitHubプロンプトチュートリアル](https://github.com/anthropics/prompt-eng-interactive-tutorial)

---

長文・大量データを扱う場合は、「冒頭配置」「XMLタグ」「引用指示」でClaudeの理解力と出力精度を最大化しましょう。