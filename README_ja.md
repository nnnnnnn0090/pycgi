# pycgi

**pycgi**は、PythonコードをHTMLファイルに直接埋め込むことができる軽量なWebサーバーソリューションで、PHPのように動的なWebページを生成できます。`<?py ?>`タグを使用することで、Pythonの力を活用しながらWebページを生成できます。

## 特徴

- **HTMLにPythonを埋め込む**: `<?py ?>`タグを使ってHTMLファイル内にPythonコードを埋め込むことができます。
- **動的コンテンツ生成**: 静的なHTMLとPythonロジックを組み合わせて動的なWebページを生成します。
- **シンプルで直感的**: PHPのように複雑な設定は不要。HTMLとPythonを一つのファイルに書くだけです。
- **リクエスト処理**: リクエストヘッダー、クエリパラメータ、POSTデータに簡単にアクセスできます。
- **レスポンス操作**: Pythonコードから直接レスポンスヘッダーやボディコンテンツを設定できます。
- **柔軟な出力**: `echo`関数を使用して、HTML内の任意の位置でコンテンツを出力できます。
- **実行パスへのアクセス**: `_EXECUTE_PATH`を使用して、実行中の**pycgi**インスタンスの実行パスを表示できます。
- **ドキュメントルートへのアクセス**: `_DOCSROOT`を使用して、`.pycgi`ファイルが格納されているドキュメントルートディレクトリを取得できます。
- **ストレージAPI**: `Storage`オブジェクトを使用して、キー・バリューのペアを簡単に保存および取得できます。

## 例

以下は、リクエストデータを処理し、レスポンスヘッダーを設定し、`echo`関数を使用して出力する方法を示す例です。実行パスとドキュメントルートも表示します。

```html
<!DOCTYPE html>
<html>
<head>
    <title>My pycgi Page</title>
</head>
<body>
    <h1>Welcome to pycgi!</h1>
    
    <!-- 静的HTMLコンテンツ -->
    <p>This is a static message.</p>
    
    <!-- 埋め込まれたPythonコード -->
    <?py
      # レスポンスヘッダーを設定
      _RSP_HEADERS["Content-Type"] = "text/html; charset=utf-8"
      _RSP_HEADERS["Custom-Header"] = "MyHeaderValue"

      # 実行パスを表示
      echo(f"<p>Execution Path: {_EXECUTE_PATH}</p>")

      # ドキュメントルートを表示
      echo(f"<p>Document Root: {_DOCSROOT}</p>")

      # echoを使ってコンテンツをレンダリング
      echo("<p>This is rendered using echo.</p>")

      # リクエストヘッダーを表示
      for header, value in _REQ_HEADERS.items():
          echo(f"<p>{header}: {value}</p>")
      
      # GETクエリパラメータを表示
      if "name" in _GET:
          echo(f"<p>Hello, {_GET['name']}!</p>")
      
      # POSTデータを表示
      if _POST_DATA:
          echo("<p>POST Data:</p><pre>")
          echo(_POST_DATA)
          echo("</pre>")
      
      # JSON POSTデータを表示
      if _POST_JSON:
          echo("<p>JSON POST Data:</p><pre>")
          echo(_POST_JSON)
          echo("</pre>")

      # ストレージAPIの例
      # ストレージに値を設定
      Storage.setValue("nickname", "pycgi")

      # ストレージから値を取得（デフォルト値付き）
      nickname = Storage.getValue("nickname", "none")
      echo(f"<p>Stored Nickname: {nickname}</p>")
    ?>
    
</body>
</html>
```

この例では以下の機能を示しています：

- **ストレージAPI**: `Storage`オブジェクトを使用して値を保存および取得する方法を示しています。
- **実行パス**: `_EXECUTE_PATH`を使用して、現在の実行パスを表示します。
- **ドキュメントルート**: `_DOCSROOT`を使用して、ドキュメントルートディレクトリを表示します。
- **レスポンスヘッダー**: `_RSP_HEADERS`辞書を使用してレスポンスヘッダーを設定します。
- **動的出力**: `echo`関数を使用してHTMLコンテンツを直接出力し、HTML内の任意の位置で内容を注入できます。

## 始め方

### 1. ダウンロードと実行

1. **pycgi**の最新バージョンを[リリースページ](https://github.com/nnnnnnn0090/pycgi/releases)からダウンロードします。

2. ダウンロード後、以下のコマンドでサーバーを実行します。

    ```bash
    ./pycgi
    ```

   このコマンドを実行すると、同じディレクトリに`docs`フォルダが自動的に作成されます。ここに`.pycgi`ファイルを置くことができます。

### 2. 最初の`.pycgi`ファイルを作成

1. `docs`フォルダ内に`index.pycgi`という名前の新しいファイルを作成し、以下の内容を追加します。

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>My First pycgi Page</title>
    </head>
    <body>
        <h1>Hello pycgi!</h1>
        
        <?py
          echo("<p>This is Python inside HTML!</p>")
        ?>
    </body>
    </html>
    ```

2. ウェブブラウザを開いて、`http://localhost:8000/index.pycgi`にアクセスして、新しく作成したページを確認します。

## ストレージAPI

**pycgi**には、Webアプリケーションの実行中にキー・バリューのペアを保存および取得できるシンプルなストレージAPIが含まれています。

- **値を保存する**: 値をストレージに保存するには、`Storage.setValue(key, value)`を呼び出します。

  ```python
  Storage.setValue("nickname", "pycgi")
  ```

- **値を取得する**: ストレージから値を取得するには、`Storage.getValue(key, default)`を使用します。キーが見つからない場合は、指定したデフォルト値が返されます。

  ```python
  nickname = Storage.getValue("nickname", "none")
  echo(f"Stored Nickname: {nickname}")
  ```

この機能は、リクエストの実行中にユーザーのセッション情報やその他の動的コンテンツを一時的に保存するのに役立ちます。

## リクエスト処理

**pycgi**は、さまざまなタイプのリクエストをシームレスに処理できます：

- **リクエストヘッダー**: `_REQ_HEADERS`辞書を介してヘッダーにアクセスできます。

  ```python
  echo(_REQ_HEADERS["Header-Name"])
  ```

- **GETパラメータ**: `_GET`辞書を使用してGETパラメータにアクセスします。

  ```python
  echo(_GET["parameter_name"])
  ```

- **POSTデータ**: 生のPOSTデータには`_POST_DATA`変数を使用します。

  ```python
  echo(_POST_DATA)
  ```

- **JSON POSTデータ**: POSTリクエストでJSONデータを送信した場合、`_POST_JSON`変数を使用してアクセスします。

  ```python
  echo(_POST_JSON["key_name"])
  ```

## レスポンス操作

HTTPレスポンスをクライアントに送信する前に変更できます：

- **レスポンスヘッダーを設定**: `_RSP_HEADERS`辞書を使用してレスポンスヘッダーを追加または変更できます。

  ```python
  _RSP_HEADERS["Header-Name"] = "Header Value"
  ```

- **レスポンスボディを設定**: `_RSP_BODY`変数を使用してレスポンスボディを定義できます。ただし、`echo`を使用すると、HTML構造内でコンテンツを出力できます。

  ```python
  _RSP_BODY = "<h2>This is the response body.</h2>"
  ```

## 仕組み

**pycgi**は、`.pycgi`拡張子を持つファイルを処理し、`<?py ?>`タグ内のPythonコードブロックをスキャンします。Pythonコードを実行し、タグをHTML出力に置き換え、最終結果をユーザーのブラウザにレンダリングします。

## ライセンス

このプロジェクトはMITライセンスの下でライセンスされています - 詳細は[LICENSE](LICENSE)ファイルを参照してください。

## お問い合わせ

質問やフィードバックがある場合は、issueを立てるか、`nnnnnnn0090@gmail.com`までご連絡ください。