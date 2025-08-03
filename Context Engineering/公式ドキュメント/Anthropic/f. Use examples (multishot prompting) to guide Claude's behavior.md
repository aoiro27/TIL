# マルチショットプロンプト（例示プロンプト）の使い方（要約・翻訳）

## 概要

- Claudeに「こうしてほしい！」を伝える最強の武器は「例（サンプル）」です。
- 3～5個の良質な例をプロンプトに含めることで、Claudeの出力精度・一貫性・品質が大幅に向上します。
- これは「few-shot（マルチショット）プロンプティング」と呼ばれ、特に構造化出力やフォーマット厳守が必要なタスクで効果的です。

---

## なぜ例を使うのか？

- **精度向上**：例があると指示の誤解が減る
- **一貫性**：例があると出力のスタイルや構造が揃う
- **パフォーマンス**：複雑なタスクでもClaudeが正しく対応しやすくなる

---

## 効果的な例の作り方

- **関連性**：実際のユースケースに近い例を使う
- **多様性**：エッジケースやバリエーションも含める（Claudeが「パターン化」しすぎないように）
- **明確さ**：`<example>`タグ（複数なら`<examples>`タグで囲む）で例を明示的に区切る

> Claudeに「この例は適切か？多様性・明確さは十分か？」と評価させたり、追加例を自動生成させることも可能です。

---

## 例：顧客フィードバックの分析

| 役割 | 例なし | 例あり |
|---|---|---|
| ユーザー | Analyze this customer feedback and categorize the issues. Use these categories: UI/UX, Performance, Feature Request, Integration, Pricing, and Other. Also rate the sentiment (Positive/Neutral/Negative) and priority (High/Medium/Low).<br>Here is the feedback: {{FEEDBACK}} | CSチームが未整理のフィードバックに困っています。<br>あなたのタスクは、フィードバックを分析し、下記カテゴリで分類・評価することです：UI/UX, Performance, Feature Request, Integration, Pricing, Other。<br>さらに、感情（Positive/Neutral/Negative）と優先度（High/Medium/Low）も評価してください。<br>**例：**<br>&lt;example&gt;<br>Input: The new dashboard is a mess! It takes forever to load, and I can’t find the export button. Fix this ASAP!<br>Category: UI/UX, Performance<br>Sentiment: Negative<br>Priority: High&lt;/example&gt;<br>Now, analyze this feedback: {{FEEDBACK}} |
| Claudeの応答 | 指示通りに分類するが、複数カテゴリを正しく出さなかったり、説明が冗長 | 例に沿ったフォーマット・複数カテゴリ・簡潔な出力 |

---

## ポイント

- 例を入れるだけで、Claudeの出力が「例の通り」になりやすい
- 例は3～5個が目安。多いほど複雑なタスクで効果大
- 例はタグで明示的に区切るとより効果的

---

## 参考

- [プロンプトライブラリ](https://docs.anthropic.com/en/resources/prompt-library/library)：多様なプロンプト例
- [GitHubプロンプトチュートリアル](https://github.com/anthropics/prompt-eng-interactive-tutorial)：実践的な例題集

---

例示プロンプト（マルチショットプロンプト）を活用することで、Claudeの出力品質・安定性が大きく向上します。