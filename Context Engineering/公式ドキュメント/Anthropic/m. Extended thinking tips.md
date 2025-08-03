https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/extended-thinking-tips

# Extended Thinking（拡張思考）活用のためのプロンプト設計Tips（要約・翻訳）

## 概要

- Claudeの「拡張思考」機能は、複雑な問題をステップバイステップでじっくり考えさせることで、難しいタスクの精度と一貫性を大きく向上させます。
- このページは、拡張思考モデルで最大限の効果を引き出すための実践的テクニックを解説します。

---

## 拡張思考を使う前の準備

- 拡張思考モードを利用する目的やユースケースを明確にしておきましょう。
- [拡張思考モデルの概要](https://docs.anthropic.com/en/docs/about-claude/models/extended-thinking-models)や[実装ガイド](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking)も参照してください。

### 技術的注意点

- **思考トークン最小値**：最低1024トークン。まずは最小値からスタートし、必要に応じて増やすのが推奨。
- **32K超の長考はバッチ処理推奨**：32Kトークンを超える場合はネットワーク・タイムアウト等の対策としてバッチ処理を推奨。
- **英語が最適**：思考処理自体は英語が最も高精度。最終出力は多言語対応可。
- **短い思考や通常のCoTは通常モード＋XMLタグで**。

---

## プロンプト設計のコツ

### 1. **まずは「一般的な指示」からスタート**

- 拡張思考では「詳細な手順」よりも「じっくり考えて」という大まかな指示の方が、Claudeの独自の思考力を活かせることが多い。
- 例：  
  ```
  Please think about this math problem thoroughly and in great detail.
  Consider multiple approaches and show your complete reasoning.
  Try different methods if your first approach doesn't work.
  ```

- うまくいかない場合は、番号付きリストで手順を細かく指示してもOK。

### 2. **マルチショット（例示）との組み合わせ**

- `<thinking>`や`<scratchpad>`タグで思考例を示すと、Claudeはそのパターンを参考に推論します。
- ただし「自由に考えさせる」方が良い結果になることもあるので、両方試してみるのがオススメ。

### 3. **指示遵守の強化**

- 複雑な指示は「明確に・具体的に」書く
- 長い指示や複数ステップは番号付きリストで
- 思考トークン予算（thinking budget）は十分に確保

### 4. **思考過程のデバッグ・チューニング**

- Claudeの思考出力（thinking block）を見て、どこで誤解やエラーが起きているか確認できる
- ただし、思考出力をuserターンで再入力したり、手動で編集するのは推奨されない（性能低下の原因）

### 5. **長文出力・長考タスクの工夫**

- 例：「2万語超の詳細なレポート」などは、段落ごとのワード数指定やアウトライン作成→本稿作成の2段階で指示
- まずは思考トークン・出力トークンともに小さく設定し、必要に応じて増やす

---

## 具体例

- **複雑な数学・プログラミング問題**：詳細な思考・検証ステップを明示
- **制約条件の多いタスク**：全ての条件をリストし「全て満たすように」と指示
- **戦略策定や長文レポート**：複数の分析フレームワークやシナリオプランニングを順番に適用させる

---

## 反省・自己チェックの活用

- Claudeに「最後に必ず検算・テストケース実行・自己レビューをしてから完了宣言せよ」と指示することで、ミスやバグを減らせる

---

## 参考

- [拡張思考クックブック（実例集）](https://github.com/anthropics/anthropic-cookbook/tree/main/extended_thinking)
- [拡張思考の実装ガイド](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking)

---

拡張思考機能を活用することで、Claudeは「人間でも悩むような複雑なタスク」を高精度・高一貫性で遂行できるようになります。