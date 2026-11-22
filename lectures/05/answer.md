# 第5回 解答

## 演習

- 回答モデル（実行時の`[model]`）：gemini-3.5-flash-lite
- 比較した質問：'第2回の説明では、LoRAは何を固定し何を学習しますか？ QLoRAは何を加えますか？'
- 対象資料（全文投入と他の方式で範囲が違う点も記録）：

### 各方式の結果

| 方式 | 回答の要点・正しさ | 引用ページと根拠 | 時間（秒） | 入力／出力トークン数 | モデル応答回数 | 生成API推定費用（USD） |
|---|---|---|---|---|---|---|
| 全文投入 | | `lec02-main / 基盤モデルの仕組み`（PDF p.52）|[time] 回答完了まで 3.06 秒（検索・埋め込みを含む）
[usage] 入力 117,025 tokens / 出力 202 tokens / モデル応答 1 回
[cost] 生成APIの推定コスト: $0.035612 USD（埋め込み・索引構築分は含まない）| | 
| ベクトル検索 | |[tool call]   search_materials({'query': 'LoRA 固定 学習 QLoRA 加える'})
[tool return] search_materials -> {"results": [{"page_id": "lec02-main-p052", "document_id": "lec02-main", "lecture": 2, "document_title": "基盤モデルの仕組み", "s…
[time] 回答完了まで 2.66 秒（検索・埋め込みを含む）
[usage] 入力 3,028 tokens / 出力 156 tokens / モデル応答 2 回
[cost] 生成APIの推定コスト: $0.001298 USD（埋め込み・索引構築分は含まない）| | | | |
| Tree | | [tool call]   browse_tree({'node_id': 'lec02-main-p052'})
[目次を開く] AIエンジニアリング実践講座2026 資料 → 基盤モデルの仕組み → 選んだモデルを、いつ・どう直すか → LoRA と QLoRA ：大きなモデルも GPU 1 台で調整できる
    （末端ページ・本文717文字を取得）
[time] 回答完了まで 4.83 秒（検索・埋め込みを含む）
[usage] 入力 9,214 tokens / 出力 329 tokens / モデル応答 5 回
[cost] 生成APIの推定コスト: $0.003587 USD（埋め込み・索引構築分は含まない）| | | | |
| Graph | |[tool call]   search_graph({'query': 'LoRA QLoRA 固定 学習 第2回'})
[tool return] search_graph -> {"seeds": [{"page_id": "lec02-main-p052", "document_id": "lec02-main", "lecture": 2, "document_title": "基盤モデルの仕組み", "sec…
[time] 回答完了まで 3.71 秒（検索・埋め込みを含む）
[usage] 入力 5,776 tokens / 出力 239 tokens / モデル応答 2 回
[cost] 生成APIの推定コスト: $0.002330 USD（埋め込み・索引構築分は含まない） | | | | |

<!-- 未実行・算定不可の場合は、その旨を書いてください。質問を追加した場合は、質問ごとに表を分けてください。 -->

- 検索だけを実行して見つかったページと、その本文で確認できたこと：
- `--trace`で見えたツール呼び出し（ツール名・引数・回数、Treeでたどった目次など）：
- 取得した情報が足りなかった例、取得できたのに回答へ使えなかった例：
- 今回の用途に採用したい方式と、その理由・比較条件の限界：
- 気づき・疑問：

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎 
- やったこと（変更したファイル・設定・処理、または設計した取得方法）：RAG_TOP_K = 10
- 比較した質問と、固定した条件（モデル・対象資料など）：gemini-3.5-flash-lite
- 結果（変更前後の回答・根拠、`--trace`の出力、時間・トークン数・生成API推定費用など）：[tool call]   search_graph({'query': 'LoRA QLoRA 固定 学習'})
[tool return] search_graph -> {"seeds": [{"page_id": "lec02-main-p052", "document_id": "lec02-main", "lecture": 2, "document_title": "基盤モデルの仕組み", "sec…
[time] 回答完了まで 3.76 秒（検索・埋め込みを含む）
[usage] 入力 5,771 tokens / 出力 206 tokens / モデル応答 2 回
- 改善した例と、残る失敗・制約：
- 気づき・疑問：時間や出力トークンが増えた
