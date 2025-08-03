# 一般原則

## 1. 指示は明確かつ具体的に
 • Claude 4は明確で具体的な指示に良く反応します。
 • 望む出力や「一歩踏み込んだ」応答が欲しい場合は、はっきりとその旨を伝えましょう。

例：
 • 効果が低い：「Create an analytics dashboard（分析ダッシュボードを作成して）」
 • 効果が高い：「Create an analytics dashboard. Include as many relevant features and interactions as possible. Go beyond the basics to create a fully-featured implementation.（分析ダッシュボードを作成してください。できるだけ多くの関連機能やインタラクションを含め、基本を超えたフル機能の実装にしてください。）」

## 2. 文脈や理由を加える
 • 指示の背景や理由を説明すると、Claude 4は意図をより深く理解し、的確な応答を返します。

例：
 • 効果が低い：「NEVER use ellipses（絶対に三点リーダーを使わないで）」
 • 効果が高い：「Your response will be read aloud by a text-to-speech engine, so never use ellipses since the text-to-speech engine will not know how to pronounce them.（あなたの応答は音声合成エンジンで読み上げられるので、三点リーダーは使わないでください。音声合成エンジンが正しく発音できません。）」

## 3. 例や細部に注意
 • Claude 4は例や細部をよく観察します。望む動作を例示し、避けたい動作は例示しないようにしましょう。

# 特定の状況へのガイダンス

## 1. 出力フォーマットの制御
 • 「○○しないで」よりも「○○してください」と肯定的に指示する方が効果的です。
 • XMLタグなどで出力形式を明示するのも有効です。
 • プロンプト自体の書式を、望む出力形式に合わせると効果が高まります。

例：
 • 「Your response should be composed of smoothly flowing prose paragraphs.（なめらかな文章の段落で構成してください）」
 • 「Write the prose sections of your response in <smoothly_flowing_prose_paragraphs> tags.（応答の文章部分は<smoothly_flowing_prose_paragraphs>タグで囲んでください）」

## 2. 思考・内省機能の活用
 • Claude 4はツール利用後の内省や複雑な推論も得意です。思考や内省を促す指示を加えると、より良い結果が得られます。

例：
 • 「After receiving tool results, carefully reflect on their quality and determine optimal next steps before proceeding.（ツールの結果を受け取ったら、その品質をよく考え、最適な次のステップを決めてから進めてください）」

## 3. 並列ツール実行の最適化
 • Claude 4は複数のツールを並列で使うのが得意です。明示的に並列実行を促すと、ほぼ100%並列でツールを使うようになります。

例：
 • 「For maximum efficiency, whenever you need to perform multiple independent operations, invoke all relevant tools simultaneously rather than sequentially.（複数の独立した操作が必要な場合は、順番にではなく同時にすべてのツールを呼び出してください）」

## 4. コーディング時のファイル生成を減らす
 • Claude 4は一時的なファイルやスクリプトを作成して試行錯誤することがあります。不要なファイルを残したくない場合は、最後に削除するよう指示しましょう。

例：
 • 「If you create any temporary new files, scripts, or helper files for iteration, clean up these files by removing them at the end of the task.（一時的なファイルやスクリプトを作成した場合は、タスク終了時に削除してください）」

## 5. フロントエンドやビジュアル生成の強化
 • 「遠慮せず全力で作って」「できるだけ多くの機能やインタラクションを含めて」「ホバーやトランジション、マイクロインタラクションも追加して」など、具体的な修飾語や要望を加えると、よりリッチな出力になります。

## 6. テスト通過やハードコーディングへの偏りを避ける
 • Claude 4はテスト通過に偏ったり、ハードコーディングしがちな場合があります。一般的で堅牢な解決策を求めることを明示しましょう。

例：
 • 「Please write a high quality, general purpose solution. Implement a solution that works correctly for all valid inputs, not just the test cases.（高品質で汎用的な解決策を書いてください。テストケースだけでなく、すべての有効な入力で正しく動作するように実装してください）」

# Claude 3.7からClaude 4への移行時の注意
 • 望む動作を具体的に記述する
 • 出力の質や詳細を高める修飾語を加える
 • アニメーションやインタラクティブ要素など、必要な機能は明示的にリクエストする

Claude 4のプロンプト設計では「明確・具体的・理由付け・例示・肯定的指示・出力形式の明示」が重要です。
詳細は公式ページ (https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices)をご覧ください。