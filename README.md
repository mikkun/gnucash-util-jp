gnucash-util-jp
===============

日本の商慣習下でGnuCashを使うためのツール

説明
----

GnuCashは個人向けのフリーな財務ソフトウエアですが、勘定科目として売掛金・買掛金を扱うことができ、また貸借対照表や損益計算書を生成できるなど、小規模ビジネスにおいても十分な機能を持っています。

確かにGnuCashのビジネス機能は強力で使いやすいですが、得意先に送る請求書を生成して印刷する際に、

1. HTML形式でスタイルシートが使えるものの、デザインの自由度が低い
2. 消費税について、「全売上金額の合計×税率」の様式で出力できない
3. 請求額について、繰越金額を加味した計算ができない

という弱点があり、特に2.と3.に関しては日本の商慣習下で使う場合、いささか不便なものがあります。

**gnucash-util-jp**の`convert_invoice-gnc2`および`convert_invoice-gnc3`は、これらの請求書生成における弱点をカバーするためのシェルスクリプトです。

特徴
----

* 日本の商慣習に対応した得意先請求書(PDFファイル)に変換

* 得意先請求書の変換時に、前回請求額ならびに入金額を追記可能

依存
----

* [GnuCash](https://www.gnucash.org/)

* [Inkscape](https://inkscape.org/)

* [IPA明朝・IPAゴシック](http://ipafont.ipa.go.jp/)

* [w3m](http://w3m.sourceforge.net/)

使い方
------

1. 作成者情報ファイル`company.txt`を適宜編集

2. GnuCashを起動し、\[帳票\]-\[ビジネス\]-\[印刷可能な請求書\]で得意先請求書を作成後、\[エクスポート\]でHTMLファイルとして保存

3. 保存したHTMLファイルを`convert_invoice-gnc2`あるいは`convert_invoice-gnc3`コマンドでPDFファイルに変換

    ```console
    # GnuCash 2.xで作成したHTMLファイルの場合
    $ ./convert_invoice-gnc2 example-gnc2.html
    # GnuCash 3.xで作成したHTMLファイルの場合
    $ ./convert_invoice-gnc3 example-gnc3.html
    ```

オプション
----------

* `-o`: 前回請求額

* `-p`: 入金額

インストール
------------

```console
$ git clone https://github.com/mikkun/gnucash-util-jp.git
```

ToDo
----

1. 売上件数が30件を超えた場合、残りを次ページに送るようにする

2. 作成者および提出先の会社名を大き目のフォントサイズで表示する

3. GnuCash 4.xで作成したHTMLファイルに対応する

作者
----

[日柳 光久](https://github.com/mikkun)

ライセンス
----------

[MIT License](./LICENSE)
