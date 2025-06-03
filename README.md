# pdflib-test

PDF_LIB を用いて、kintone アプリのレコードから PDF ファイルへ文言および画像を描画する。

## 使い方

1.  **開発ビルドとデプロイ**
    * `npm run build:dev`: `sourcemap:inline` でソースマップを作成します。
    * `npm run deploy`: kintone の対象アプリへアップロードします。

2.  **本番ビルドとデバッグ**
    * `npm run build`: `sourcemap:true` でソースマップ (`js.map`) を別ファイルで作成します。
    * デベロッパーツールでソースマップを追加し、デバッグに利用してください。

## フォントの取得方法

フォントは、パラメーターに応じて以下の通りに取得されます。

* **`app.font.url.value` を指定した場合:**
    GitHub Pages からフォントファイルを取得します。
* **上記以外の場合:**
    `app.font.id.value` (アプリ ID)、`app.font.recordId.value` (レコード ID)、`app.font.attachment.value` (フィールド名) で指定した kintone アプリの添付ファイルフィールドからフォントファイルを取得します。

## 文字が一部消えてしまう場合の対応

文字がPDFに正しく表示されない場合は、以下の対応を試してください。

1.  **フォントのサブセット化の解除:**
    * `customFont = await pdfDoc.embedFont(fontBytes, { subset: true });`
        上記のコードを、以下の様に変更します。
    * `customFont = await pdfDoc.embedFont(fontBytes);`
    * `subset: true` を削除することで、フォント全体が埋め込まれ、一部の文字が欠ける問題を解消できる場合があります。

2.  **フォントの変更:**
    * 使用しているフォントを `ipaexg.ttf` (IPAexゴシック) など、別のフォントに変更してみてください。フォントによっては、PDFへの埋め込みや描画に問題がある場合があります。
