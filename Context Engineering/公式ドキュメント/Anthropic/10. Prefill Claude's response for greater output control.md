https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prefill-claudes-response

# Claudeの出力をプリフィル（事前入力）して出力制御を強化する方法

## 概要

- Claudeは、**Assistantメッセージをプリフィル（事前入力）**することで、出力の冒頭やフォーマット、キャラクター性を細かくコントロールできます。
- これにより、例えば「前置きなしでJSONだけ返す」「キャラクターを維持する」「特定のテンプレートで出力させる」などが可能です。
- Claudeの期待通りの動作が得られない場合、最初の数文をプリフィルするだけで大きな改善が見込めます。

---

## プリフィルのやり方

- Assistantメッセージの`content`に、続けてほしい冒頭部分を記述します。
- Claudeはその部分から続きを生成します。

**例（Python）**
```python
import anthropic

client = anthropic.Anthropic()
response = client.messages.create(
    model="claude-opus-4-20250514",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "What is your favorite color?"},
        {"role": "assistant", "content": "As an AI assistant, I don't have a favorite color, but if I had to pick, it would be green because"}  # ←ここでプリフィル
    ]
)
print(response.content)
```

> **注意**：プリフィルの末尾に空白（スペース）があるとエラーになるので注意！

---

## 代表的な用途と例

### 1. 構造化出力・前置き省略

- JSONやXMLだけを返したい場合、プリフィルで`{`や`<root>`などを指定すると、Claudeは前置きなしでそのフォーマットで出力を始める。

**例**
- ユーザー：「この商品説明からname, size, price, colorをJSONで抽出して」
- Assistantプリフィル：`{`
- Claudeの出力：
  ```json
  "name": "SmartHome Mini",
  "size": "5 inches wide",
  "price": "$49.99",
  "colors": ["black", "white"]
  }
  ```

### 2. キャラクター維持（ロールプレイ）

- 役割を演じ続ける必要がある場合、`[Sherlock Holmes]`のようなプリフィルを使うと、長い会話でもキャラクター性を保ちやすい。

**例**
- Assistantプリフィル：`[Sherlock Holmes]`
- Claudeの出力：キャラクターになりきった応答

---

## ポイント

- プリフィルは「ちょっとした補助」でも効果絶大
- 特に「前置きが邪魔」「フォーマット厳守」「キャラ維持」などが必要な場面で有効
- 拡張思考モード（Extended Thinking Models）ではプリフィルは未対応

---

## 参考

- [プロンプトライブラリ](https://docs.anthropic.com/en/resources/prompt-library/library)
- [GitHubプロンプトチュートリアル](https://github.com/anthropics/prompt-eng-interactive-tutorial)

---

Claudeの出力冒頭をプリフィルすることで、より思い通りの出力制御が可能になります。