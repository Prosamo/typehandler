```markdown
# typehandler

`typehandler` は、タイピングゲーム用のPythonモジュールです。このモジュールは、ひらがなをローマ字に変換し、タイピングゲームの入力パターンを生成します。また、pygameやtkinterなどでキーイベントを検知し、入力されたキーを渡すことで、正誤判定などができます。これにより、タイピングゲームに必要な処理を行うことができます。

## インストール

```sh
pip install typehandler
```

## 使用方法

### 基本的な使い方

まず、`typehandler` モジュールをインポートし、`Process` クラスを使用します。

```python
import typehandler

# Processクラスのインスタンスを作成
game_process = typehandler.Process()
```

#### 1. 新しい文章の設定

新しい文章を設定するには、`set_new_sentence` メソッドを使用します。

```python
game_process.set_new_sentence()
```

#### 2. 別の辞書を設定

別の辞書を設定するには、`set_new_words` メソッドを使用します。

```python
new_words = {
    "林檎": "りんご",
    "ぶどう": "ぶどう",
    "レモン": "れもん"
}
game_process.set_new_words(new_words)
```

#### 3. 入力の判定

入力が正しいかどうかを判定するには、`check_correct_input` メソッドを使用します。

```python
key = 'k'
is_correct = game_process.check_correct_input(key)
print(is_correct)  # True または False
```

#### 4. 文章の完了判定

文章が完了したかどうかを判定するには、`check_sentence_completion` メソッドを使用します。

```python
is_completed = game_process.check_sentence_completion()
print(is_completed)  # True または False
```

#### 5. 画面に表示するローマ字の更新

画面に表示するローマ字を更新するには、`update_show_roman` メソッドを使用します。

```python
show_roman = game_process.update_show_roman()
print(show_roman)
```

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。詳細は`LICENSE`ファイルを参照してください。
```
