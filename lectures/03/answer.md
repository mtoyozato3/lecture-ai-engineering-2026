# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：回答の参照元が示されている
- `--trace` で見えたツール呼び出し（ツール名と引数）：
[tool call]get_lecture_summary({'lecture': 2})
[tool return] get_lecture_summary -> # 第2回ファインチューニングとLoRA
- 1つの質問での LLM 呼び出し回数（`requests`）：requests=2, tool_calls=2
- 追加したツールと、docstring に書いた説明：
make_quiz
旨定した回の用語から1つを選び、確認問題と答えを返す。
「第2回の確認問題を出して」のように、復習用の問題を求められたときに使う。
#1.load
、glossary ()からlectureが一致する用語を集める
#2 .1 つ選ぶ(randcm . uhci tie )
#3.問題と答えを文字列で返す(json.dumpsなど)


## 宿題

- 取り組んだレベル：基礎
- やったこと：docstringの「用語を1つだけ入れる」を「まとめて入れる」に変えた
- 結果：トークン数が半分に減った。tool_calls=1に変わった
- 気づき・疑問：いろいろな工夫が可能であることがわかった
