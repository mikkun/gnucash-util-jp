# gnucash-util-jp

![GitHub license](https://img.shields.io/github/license/mikkun/gnucash-util-jp)

> :chart: 日本の商慣習下でGnuCashを使うためのツール

## 説明

GnuCashは個人向けのフリーな財務ソフトウエアですが、勘定科目として売掛金・買掛金を扱うことができ、また貸借対照表や損益計算書を生成できるなど、小規模ビジネスにおいても十分な機能を持っています。

確かにGnuCashのビジネス機能は強力で使いやすいですが、得意先に送る請求書を生成して印刷する際に、

1. HTML形式でスタイルシートが使えるものの、デザインの自由度が低い
2. 消費税について、「全売上金額の合計×税率」の様式で出力できない
3. 請求額について、繰越金額を加味した計算ができない

<!-- markdownlint-disable-next-line no-inline-html -->
という弱点があり、特に<strong>2.</strong>と<strong>3.</strong>に関しては日本の商慣習下で使う場合、いささか不便なものがあります。

**gnucash-util-jp**の`convert_invoice`は、これらの請求書生成における弱点をカバーするためのシェルスクリプトです。

## 特徴

- 日本の商慣習に対応した得意先請求書(PDFファイル)に変換
- 得意先請求書の変換時に、前回請求額ならびに入金額を追記可能

## 依存

- [GnuCash](https://www.gnucash.org/) (&gt;= 2.6.15)
- [Inkscape](https://inkscape.org/) (&gt;= 0.92.1)
- [IPA明朝・IPAゴシック](https://moji.or.jp/ipafont/)
- [w3m](https://github.com/tats/w3m)

## インストール

```shell
git clone https://github.com/mikkun/gnucash-util-jp.git
```

## 使い方

1. 作成者情報ファイル`company.txt`を適宜編集
2. GnuCashで得意先請求書を作成し、HTMLファイルとしてエクスポート
    1. \[ビジネス\]→\[得意先\]→\[得意先請求書を新規作成\]で得意先請求書を作成
    2. 得意先請求書を編集し、記帳
    3. \[ビジネス\]→\[得意先\]→\[得意先請求書を検索\]で印刷したい得意先請求書を選択
    4. 得意先請求書の表示後、\[ファイル\]→\[得意先請求書を印刷\]で印刷可能な請求書を出力
    5. \[ファイル\]→\[エクスポート\]→\[帳票をエクスポート\]でHTMLファイルとしてエクスポート
3. エクスポートしたHTMLファイルを`convert_invoice`コマンドでPDFファイルに変換

    ```shell
    ./convert_invoice example-gnc3.html
    ```

:warning: なお、テンプレートファイル`template.svg`を編集する必要は通常ありませんが、編集する場合は必ず「プレーンSVG」形式で保存してください。

## オプション

- `-o`: 前回請求額
- `-p`: 入金額

## TODO

1. 売上件数が30件を超えた場合、残りを次ページに送るようにする
2. 作成者および提出先の会社名を大きめのフォントサイズで表示する

## ライセンス

[MIT License](./LICENSE)

## 作者

[日柳 光久](https://github.com/mikkun)
