# cashless-pdf2tsv
キャッシュレス・消費者還元事業事務局審査を通過した加盟店一覧のPDFをTSV変換

# Download

キャッシュレス・消費者還元事業事務局審査を通過した加盟店一覧
https://cashless.go.jp/assets/doc/kameiten_touroku_list.pdf

tabula-java
https://github.com/tabulapdf/tabula-java

# Command

$ java -jar -Xmx2G tabula-1.0.3-jar-with-dependencies.jar -f TSV -o list.tsv -l -p 3-6360 kameiten_touroku_list.pdf

※Windowsの場合は64bitのJavaをインストールしてください

「Exception in thread "main" java.lang.OutOfMemoryError: Java heap space」で落ちます

# Google Colaboratory

https://colab.research.google.com/drive/1vBYxRVFAoNm1enniAsxNOr232LFMfl7E

ダウンロードのところでエラー「MessageError: TypeError: Failed to fetch」が発生します

ダウンロードをもう一度実行するとダウンロードされます

# PDF => TSV

+ pdfbox.tsv

java -jar pdfbox-app-2.0.16.jar ExtractText -startPage 3 -sort -encoding UTF-8 %1

※textからtsvに変換

+ tabula090.tsv

java -jar tabula-0.9.0-jar-with-dependencies.jar -f TSV -o tabula090.tsv -r -p 3-6360 %1

+ tabula103.tsv

java -jar tabula-1.0.3-jar-with-dependencies.jar -f TSV -o tabula103.tsv -l -p 3-6360 %1

# tabulaについて

+ tabula0.9.0までは文字変換なし
+ 0.9.1以降はJAVAのNormalizerが働いて全角英数字記号を半角、半角カナを全角、機種依存文字を変更　例Ⅰ→I、Ⅱ→II、①→1、℃→゜C、㈱→(株)等
+ 罫線をオーバーしたものや文字が重なっているところはカットされる
  + 0821-pdfbox.tsv
  + 0821-tabula090.tsv

zaimの変換結果を見ているとtabulaで一括変換後、?部分を手動で訂正してる？

# ソフト比較

| ソフト | 種類 | ファイル形式 | 抽出範囲 | ワークシート | 文字オーバー | 文字正規化 | 備考 | URL |
|-------------------|------------|--------------|----------|--------------|--------------|------------|----------------------------------------------|-----------------------------------------------------------|
| pdftotext -raw | バイナリ | text | 全体 | － | － | なし | 順番がずれる場合あり | https://poppler.freedesktop.org/ |
| pdftotext -layout | バイナリ | text | 全体 | － | － | なし | スペース多め | https://poppler.freedesktop.org/ |
| pdfbox -sort | java | text | 全体 | － | － | なし |  | https://pdfbox.apache.org/2.0/commandline.html |
| tabula0.9.0 | java | csv,tsv | 表のみ | － | 消える | なし |  | https://github.com/tabulapdf/tabula-java |
| tabula1.0.3 | java | csv,tsv | 表のみ | － | 消える | あり |  | https://github.com/tabulapdf/tabula-java |
| camelot | python | excel,csv | 表のみ | 複数 | 隣のセル | なし |  | https://camelot-py.readthedocs.io/en/master/user/cli.html |
| smallpdf | オンライン | excel | 全体 | 複数 | 消える | なし | 全角スペースが半角スペース、スペース多め | https://smallpdf.com/jp/ |
| ilovepdf | オンライン | excel | 表のみ | ひとつ | 消える | なし | 全角スペースが半角スペース、スペース少し多め | https://www.ilovepdf.com/ja |
| cloverpdf | オンライン | excel | 全体 | ひとつ | 消える | なし | 全角スペースが半角スペース | https://www.cleverpdf.com/jp |
| hipdf | オンライン | excel | 全体 | 複数 | 隣のセル | なし | 文字オーバーの文字と重なるとずれる | https://www.hipdf.com/ |
| justpdf | 商用ソフト | excel | 全体 | 複数 | 正常 | なし | 丁目がT目になったり変換ミスもあり | https://www.justsystems.com/jp/products/jl_justpdf/ |
