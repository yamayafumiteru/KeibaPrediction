# 競馬予想モデル
pythonを用いて作成しました。

主に使用したフレームワーク

「pandas, numpy, sklearn, tensorflow, lightGBM」

# 使用方法
仮想環境orAnaconda起動後本モデルで使用するモジュールをインストールする。
```
pip intall -r requirements.txt
```

次に以下2つのファイルを作成すること
```
Keiba/datafile/
Keiba/datafile/pred_data/
```
1つ目のファイルはデータを格納するファイル、
もう1つは前処理後のファイルを格納するファイルである。
別のところに保管したい場合はファイルパスを変更の上別のファイル名を使用すること。


インストール後データを格納する。格納先は
```
Keiba/datafile/
```
直下にデータを格納する。データ名は「main.csv」とするが変更する際は
setup.pyからmain_dataのパスを書き換えること。なお本データはJRA-VANからダウンロードしているが、スクレイピングなど別の方法で得る方法でも可。スクレイピングをする際は著作権や使用方法をまもること。
本モデルで使用するデータはブログに記載してあります。

[競馬予測で使用する際のCSVデータ](https://kashiwapro.hatenablog.com/entry/2021/10/29/162155)

予想したいデータはmain.csvの【result,time,rank3,rank4,3ftime,basetime】の所に[999]の値を入れること、
legtypeは空欄のままで大丈夫です。

※一部データに先頭に空欄や*,&などが入っている場合がありますのでその際はExcel上で取り除いて頂けますようお願い致します。

準備が完了したら
```
python setup.py
```
で起動します。

予想終了後「ans.csv」が出力されます。

# 予想方法
「ans.csv」を開く。

開いたら、gbm_pred, tf_pred, flagのカラムを参照する。

flagはgbm_pred, tf_predを参照し、3着以内の確率が50％以上の物を0-1フラグで出力しています。

gbm_predはLightGBMモデルで予想した出力結果を返しています。

tf_predはTensorflowモデルで予想した出力結果を返しています。

どちらを参照して予想しても構いませんが、最初にflagを確認してその後gbm_flag、tf_pred
を確認する方法をおすすめしております。

※重複が出る可能がありますが、その際はexcel上で重複削除をしていただけると幸いです。

# 免責条項
・本モデルを通して発生した損失や損害については一切責任を負うことができません。予めご了承ください。
ご自身の判断で慎重に馬券の購入をお願いいたします。

・本モデルの情報の完全性・正確性・有用性等についていかなる保証も致しません。

# その他注意事項
・起動確認時のPCスペック

メモリ：16.0GB

CPU：Intel(R)Corei7-8700CPU@3.20GHz 3.19 GHz

GPU：NVIDIA GeForce GTX1070Ti

これ以下のPCスペックの場合正常に予想ができない恐れがあります。

・Tensorflowを使った予想をしている際、極端に確率が低くならないようmodels内の284行目付近にあるforループで正常に予想できているのか確認の処理をしております。
前処理から処理をしていた際にお使いのPCスペックによっては処理が重くなる可能性があります。その際は,
一度処理を中断してから【csvdataframe.csv】があるのを確認してからsetup.pyにあるcreate_keiba_prediction関数の
flag=Falseにすると前処理が省略されてモデルの予想からになりますので、そちらで対応をしていただけると幸いです。

・前処理が省略できるタイミングはdataprocess.pyのformatting_data_process関数がreturnを返したタイミングです。
保存方法はcsvデータでされますのでデータによっては容量が多くなる可能性があります。

・データ集計日は2013年の1月1週目のレースからにしています。過去の戦績もデータに入れていますので、
少なすぎると正常な集計ができない可能性があります。その点ご了承ください。


# 更新履歴
2021年11月8日：v1.0を公開

2022年1月11日：v2.0を公開 tensorflowモデル周りを大幅更新、それに加えてReadmeも更新


# リンク
ブログ ：https://kashiwapro.hatenablog.com/

Qiita ：https://qiita.com/KHTTakuya/items/35ea5e710f0fb3aa86e4

予想サイト【Proheter】　: https://django-keiba-site.herokuapp.com/



