# Claudeプロンプト設計：XMLタグ活用ガイド

## 概要

- プロンプトに「文脈」「指示」「例」など複数の要素が含まれる場合、**XMLタグ**で明示的に区切るとClaudeの理解度・出力品質が大きく向上します。
- ClaudeはXMLタグで囲まれた情報を正確に区別しやすくなり、誤解や混同を防げます。

---

## なぜXMLタグを使うのか？

- **明確さ**：各要素（指示、例、データなど）を明示的に分離できる
- **精度向上**：Claudeが指示や例を混同しにくくなる
- **柔軟性**：部分的な修正や追加がしやすい
- **パース容易性**：Claudeの出力もXMLタグで構造化すれば、後処理で必要な部分だけ抽出しやすい

---

## タグ設計のベストプラクティス

1. **一貫性**：同じタグ名は常に同じ意味で使う
2. **ネスト**：階層構造がある場合はタグを入れ子にする（例：`<examples><example>...</example></examples>`）
3. **意味のあるタグ名**：内容に合ったタグ名を使う（例：`<instructions>`, `<data>`, `<findings>`, `<recommendations>`など）

> Claudeは特定の「学習済みタグ」を持っているわけではないので、内容に合った分かりやすいタグ名を自由に設計してOKです。

---

## 具体例

### 1. 財務レポート生成

**XMLタグなし**
```
You’re a financial analyst at AcmeCorp. Generate a Q2 financial report for our investors. Include sections on Revenue Growth, Profit Margins, and Cash Flow, like with this example from last year: {{Q1_REPORT}}. Use data points from this spreadsheet: {{SPREADSHEET_DATA}}. The report should be extremely concise, to the point, professional, and in list format. It should and highlight both strengths and areas for improvement.
```

**XMLタグあり**
```xml
You’re a financial analyst at AcmeCorp. Generate a Q2 financial report for our investors.

<data>
{{SPREADSHEET_DATA}}
</data>

<instructions>
1. Include sections: Revenue Growth, Profit Margins, Cash Flow.
2. Highlight strengths and areas for improvement.
</instructions>

Make your tone concise and professional. Follow this structure:
<formatting_example>
{{Q1_REPORT}}
</formatting_example>
```

---

### 2. 契約書リスク分析

**XMLタグなし**
```
Analyze this software licensing agreement for potential risks and liabilities: {{CONTRACT}}. Focus on indemnification, limitation of liability, and IP ownership clauses. Also, note any unusual or concerning terms. Here’s our standard contract for reference: {{STANDARD_CONTRACT}}. Give a summary of findings and recommendations for our legal team.
```

**XMLタグあり**
```xml
<agreement>
{{CONTRACT}}
</agreement>

<standard_contract>
{{STANDARD_CONTRACT}}
</standard_contract>

<instructions>
1. Analyze these clauses:
   - Indemnification
   - Limitation of liability
   - IP ownership
2. Note unusual or concerning terms.
3. Compare to our standard contract.
4. Summarize findings in <findings> tags.
5. List actionable recommendations in <recommendations> tags.
</instructions>
```

---

## 応用テクニック

- **マルチショット例示**：`<examples>`や`<example>`タグで複数例を明示
- **Chain of Thought