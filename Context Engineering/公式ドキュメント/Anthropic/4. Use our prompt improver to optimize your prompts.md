# プロンプトインプルーバー（Prompt Improver）の使い方・概要

## 概要

- **プロンプトインプルーバー**は、あなたのプロンプト（AIへの指示文）を自動で分析・改善し、より高精度で複雑なタスクにも強いプロンプトに仕上げてくれるツールです。
- 特に「高い精度が求められる」「複雑な推論が必要」なタスクで効果を発揮します。

---

## 使い始める前に

- 改善したい[プロンプトテンプレート](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompt-templates-and-variables)が必要です。
- Claudeの出力に関するフィードバック（例：「要約が専門家向けとしては簡素すぎる」など）があると、より良い改善が可能です（任意）。
- 入力例と理想的な出力例も用意できるとベストです（任意）。

---

## プロンプトインプルーバーの仕組み

1. **例の抽出**  
   プロンプトテンプレートから例（input/output）を見つけて抽出します。
2. **初期ドラフト作成**  
   明確なセクション分けやXMLタグを使った構造化テンプレートを作成します。
3. **思考連鎖（Chain of Thought）強化**  
   詳細な推論手順（思考連鎖）を追加・洗練します。
4. **例の強化**  
   新しい推論プロセスに合わせて例をアップデートします。

---

## 得られるもの

- Claudeの推論プロセスを明確に誘導する「思考連鎖」指示
- XMLタグによる明確な構造化
- 入力から出力までのステップを示す標準化された例
- Claudeの初期応答を誘導するためのプリフィル（事前入力）

---

## 使い方

1. 改善したいプロンプトテンプレートを提出
2. Claudeの出力に関するフィードバック（任意）を追加
3. 入力例と理想的な出力例（任意）を追加
4. 改善されたプロンプトを確認

---

## テスト用例の生成

- まだ例がない場合は、[テストケースジェネレーター](https://docs.anthropic.com/en/docs/test-and-evaluate/eval-tool#creating-test-cases)を使って
  1. サンプル入力を生成
  2. Claudeの応答を取得
  3. 理想的な出力に編集
  4. その例をプロンプトに追加
  という流れで作成できます。

---

## どんな時に使うべき？

- 複雑な推論や詳細な説明が必要なタスク
- 精度重視（スピードよりも正確さが大事な場合）
- Claudeの現状の出力に大きな改善が必要な場合

> ※ レイテンシやコスト重視の場合は、よりシンプルなプロンプトを使うのが推奨されます。プロンプトインプルーバーは丁寧で長めの出力を生みやすいです。

---

## 改善例

**元のプロンプト例（Wikipedia記事分類タスク）**
```plaintext
From the following list of Wikipedia article titles, identify which article this sentence came from.
Respond with just the article title and nothing else.

Article titles:
{{titles}}

Sentence to classify:
{{sentence}}
```

**改善後のプロンプト例（抜粋）**
```plaintext
You are an intelligent text classification system specialized in matching sentences to Wikipedia article titles. Your task is to identify which Wikipedia article a given sentence most likely belongs to, based on a provided list of article titles.

<article_titles>
{{titles}}
</article_titles>

<sentence_to_classify>
{{sentence}}
</sentence_to_classify>

Your goal is to determine which article title from the provided list best matches the given sentence. Follow these steps:
1. List the key concepts from the sentence
2. Compare each key concept with the article titles
3. Rank the top 3 most relevant titles and explain why they are relevant
4. Select the most appropriate article title that best encompasses or relates to the sentence's content

Wrap your analysis in <analysis> tags. Include the following:
- List of key concepts from the sentence
- Comparison of each key concept with the article titles
- Ranking of top 3 most relevant titles with explanations
- Your final choice and reasoning

After your analysis, provide your final answer: the single most appropriate Wikipedia article title from the list.

Output only the chosen article title, without any additional text or explanation.
```

**改善ポイント**
- ステップバイステップの推論指示を追加
- XMLタグで構造化
- 出力フォーマットを明示
- Claudeの思考プロセスを誘導

---

## トラブルシューティング

- **例が出力に現れない**：XMLタグで正しくフォーマ