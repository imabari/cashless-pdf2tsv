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
