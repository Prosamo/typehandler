# typehandler

`typehandler` は、タイピングゲーム用のPythonモジュールです。このモジュールは、ひらがなをローマ字に変換し、タイピングゲームの入力パターンを生成します。また、pygameやtkinterなどでキーイベントを検知し、入力されたキーを渡すことで、正誤判定などができます。これにより、タイピングゲームに必要な処理を行うことができます。

## インストール

```sh
pip install typehandler
```

## 使用方法

### 基本的な使い方

まず、`typehandler` モジュールをインポートし、`Process` クラスを使用します。Processクラスは、お題とそのフリガナの辞書を受け取ります。

```python
import typehandler

# お題とフリガナの辞書
words = {
    "西瓜": "すいか",
    "いちご": "いちご",
    "バナナ": "ばなな"
}

# Processクラスのインスタンスを作成
game_process = typehandler.Process(words)
```
辞書を設定するためのメソッドもあるので、必ずしもインスタンス作成のタイミングで辞書を渡す必要はありません。

#### 1. 新しい文章の設定

新しい文章を設定するには、`set_new_sentence` メソッドを使用します。このメソッドが呼び出されると、辞書からランダムに文章を選び、正誤判定に必要な準備まで行います。このメソッドを呼び出す以外に、文章の更新に必要な手順はありません。文章を打ち終わったときや、制限時間を過ぎたときに呼び出すことを想定しています。

```python
game_process.set_new_sentence()
```
通常は引数を受け取らずに使用することを想定しています。しかし、このメソッドは辞書を受け取ることができ、その場合、一度だけその辞書から文章を選びます。このモジュールでは完全ランダム以外に文章を選ぶ機能は実装していない関係で、一部のプロジェクトには使用できない場合があり、それを解決するための機能です。自分で文章を選んだあと、このメソッドに要素が1つの辞書を渡すことで、疑似的に文章を選ぶ機能を入れ替えることができます。

#### 2. 別の辞書を設定

別の辞書を設定するには、`set_new_words` メソッドを使用します。このメソッドを呼び出すと、`set_new_sentence`が呼び出され、次に表示する文章を選ぶところまで実行します。

```python
new_words = {
    "林檎": "りんご",
    "ぶどう": "ぶどう",
    "レモン": "れもん"
}
game_process.set_new_words(new_words)
```

#### 3. 入力の判定

入力が正しいかどうかを判定するには、`check_correct_input` メソッドを使用します。このメソッドは引数にキーの名前を受け取り、`True`か`False`を返します。基本的に`if`文の条件に使うことを想定しています。

```python
key = 'k'
is_correct = game_process.check_correct_input(key)
print(is_correct)  # True または False
```

#### 4. ひらがなの完了判定
ひらがなが完了したかどうかを判定するには`check_chunk_completion`メソッドを使用します。`check_correct_input`が`True`を返した後の`if`文の条件に使う事を想定しています。
```python
is_completed = game_process.check_chunk_completion()
print(is_completed)  #True または False
```

#### 5. 文章の完了判定

文章が完了したかどうかを判定するには、`check_sentence_completion` メソッドを使用します。`check_chunk_completion`が`True`を返した後の`if`文の条件に使うことを想定しています。

```python
is_completed = game_process.check_sentence_completion()
print(is_completed)  # True または False
```

#### 6. 画面に表示するローマ字の更新

　このモジュールでは、画面に描画するための、入力パターンの一例として`show_roman`というものを用意しています。直接このインスタンス変数にアクセスしていただくだけで利用できますが、あくまで一例を表示するだけなので、適宜更新しないとずれが生じてきます。
　画面に表示するローマ字を更新するには、`update_show_roman` メソッドを使用します。リアルタイムに反映させるために、ゲームループの中で、適切に更新することが求められます。毎フレーム呼び出すか、入力を検知するたびに呼び出すか、都合の良い方を選んで使ってください。このメソッドは、戻り値に入力パターンの一例を返しますが、必ずしも受け取る必要はありません。

```python
show_roman = game_process.update_show_roman()
print(show_roman)
```

#### 7. 全てこれで完結
上記の正誤判定から文章の更新までのメソッドを全てまとめた`main`というメソッドを用意してあります。これはキーの名前を受け取り、正誤判定から、文章の更新までの全てを行います。音声などの処理をそれぞれ追加する需要に応えるため、上記のメソッドを用意しています。しかし、音声も何もいらないという人は、これだけを呼び出せば、ゲームシステムは完成します。
```python
key = 'k'
game_process.main(key)
```

#### 8.利用可能なインスタンス変数
画面に描画するための文字列など、自由にご使用いただけます。（描画機能自体はこのモジュールには実装していません。）
```python
self.input              #入力済みのローマ字
self.show_roman         #入力パターンの一例
self.sentence           #現在の文章
self.words              #文章のフリガナの辞書
```

#### 9.ローマ字の生成だけ使いたい場合
メインの使用方法からは逸れますが、ひらがなからローマ字の生成を行う部分だけを使いたい人もいると思うので、`divide`というメソッドを用意しておきました。
```python
game_process.divide('あいうえお')
```

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。詳細は`LICENSE`ファイルを参照してください。
