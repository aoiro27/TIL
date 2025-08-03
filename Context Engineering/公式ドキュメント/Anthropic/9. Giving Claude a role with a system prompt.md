https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/system-prompts

# Claudeに「役割」を与えるシステムプロンプトの使い方

## 概要

- Claudeの「system」パラメータで“役割”を与えると、出力の精度・専門性・一貫性が大きく向上します。
- これを「ロールプロンプティング（role prompting）」と呼び、Claudeを汎用アシスタントから「バーチャル専門家」へと変身させる最強のテクニックです。

---

## なぜロールプロンプティングを使うのか？

- **精度向上**：法務分析や財務モデリングなど、専門性が求められる場面でClaudeのパフォーマンスが大幅にアップ
- **トーンの調整**：CFOのような簡潔さ、コピーライターのような表現力など、役割に応じて出力の雰囲気が変わる
- **タスクへの集中**：役割を明示することで、Claudeがタスクの枠組みから逸脱しにくくなる

---

## 使い方

Claude APIの`system`パラメータに役割を記述します。  
タスク固有の指示やデータは`user`ターンに記述します。

**例（Python）**
```python
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-3-7-sonnet-20250219",
    max_tokens=2048,
    system="You are a seasoned data scientist at a Fortune 500 company.",  # ここで役割を指定
    messages=[
        {"role": "user", "content": "Analyze this dataset for anomalies: <dataset>{{DATASET}}</dataset>"}
    ]
)

print(response.content)
```

> **コツ**：役割はできるだけ具体的に！  
> 例：「データサイエンティスト」よりも「Fortune 500企業で顧客インサイト分析を専門とするデータサイエンティスト」の方が、より専門的な出力が得られます。

---

## 例

### 1. 契約書リスク分析

- **役割なし**：一般的な要約や表面的な指摘のみ
- **役割あり**：「あなたはFortune 500の法務責任者です」と指定すると、重大なリスクや具体的な修正案まで踏み込んだ専門的な分析が得られる

### 2. 財務分析

- **役割なし**：数字の羅列や一般的なコメント
- **役割あり**：「あなたは急成長B2B SaaS企業のCFOです」と指定すると、経営判断に直結するアクションや投資家向けの戦略的コメントが得られる

---

## ポイント

- Claudeの「役割」は`system`パラメータで指定
- タスク指示やデータは`user`ターンで与える
- 役割を変えるだけで、同じデータでも出力内容や視点が大きく変わる
- 役割はできるだけ具体的に書くと効果大

---

## 参考

- [プロンプトライブラリ](https://docs.anthropic.com/en/resources/prompt-library/library)
- [GitHubプロンプトチュートリアル](https://github.com/anthropics/prompt-eng-interactive-tutorial)

---

Claudeに「役割」を与えることで、あなたのタスクに最適化された専門家AIとして活用できます。