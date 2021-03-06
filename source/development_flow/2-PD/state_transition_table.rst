.. index:: 状態遷移表
    single: PD; 状態遷移表

.. _状態遷移表:

状態遷移表
================
| 何かと作成する図の一つ

概要
----------
| 何かがあった時にこれをする。といった仕様を表に纏めることで検討漏れをなくす手法の一つ。
| 設計においてこれが作れれば後は消化試合のようなものである。

目的
------------
| 変更、追加する処理に関して、一定のシーケンスがある場合や他との連携や競合を考える必要がある場合に
| 起こり得る全てを列挙しそれらへの対応を決定する為に作成する。
| 例えば異常検知を一つ追加した場合に、ざっと以下の事が考えられる。

* 他の異常検知と同時に発生した場合どちらを優先させるのか。
* 他の異常検知が発生しフェールや復帰処理中の場合は本検知は行うのか。
* 本検知でのフェール実行中に既存の異常検知が発生した場合、制御はどうするのか。

| 基本的に変更、追加にてバグが発生する場合とはこれらの事を網羅しきれていない場合が大半であり、
| それを未然に防ぐ為には最初に起こりそうな事象を全て網羅する必要がある。
| 状態遷移表はそれに対して非常に有用な手段である。

作成方法
---------------
| 仕様や母体のソフトからあり得る状態と、起こり得るイベントを全て書き出す。
| そして、表の縦軸に状態を、横軸にイベントを並べる。

| この時、状態とイベントに寄って示されるセルには単一の事象しか存在しないようにすること。
| 例えば以下のような仕様があったとする。

* 電源を付けると起動する。消すと終了する。
* 異常を検知すると再起動する。
    但し電源を付けたままで異常が3回発生した場合は動作を停止した状態で何もしないようにする。

|
| 以下の表は駄目な例である。

.. csv-table:: **【状態遷移図】駄目な例**
    :file: bad_example.csv
    :encoding: 'shift_jis'
    :header-rows: 1
    :stub-columns: 2
    :widths: 4, 15,10,10,10,40

| この場合、太字で表現したセル内において、単一セル内に条件分岐が存在する。
| これをすると項目の洗い出しに不備が生じる可能性がある。
| たとえここだけでしか分岐しないと明確であっても、きちんと状態を分割する必要がある。
| また、登場するバッファについても記述しておくことで制御タイミング起因の不具合を防止する事が出来る。

.. note::
 | 必要なのは毒も食らわば皿まで精神である。
 | しつこいくらいに全部書くことが大切である。

.. csv-table:: **【状態遷移図】マシな例**
    :file: good_example.csv
    :encoding: 'shift_jis'
    :header-rows: 1
    :stub-columns: 3
    :widths: 4, 15,10,25,25,25,25

| 登場するバッファの初期化、アクセス、判断タイミングを明記することで、順番の入れ違いや初期化漏れを回避する。
| 今回特に数字の判断を要しない個所は*で省略してある。

.. note::
 | 書いた後に、きちんとどのルートも期待する最後まで順繰りに辿れることを確認する事!!

注意事項
--------------
* 制御に関連する登場人物は全て登場させる事。
* イベントの優先度は分かるようにしておく事。出来るなら左から優先度降順に並べると分かり易い。同時に発生した場合どちらを優先するのかを明記する手間が省ける。
* 状態は隙間が無いようにする事。例えば外部にデータを保存する場合、保存開始から保存完了までにラグがある為、きちんと保存中と言った状態を用意すること。
* イベントが発生しない個所と、発生しても無視をする個所は説明時にはっきりと言えるようにする。可能ならば表内に書いてしまう。

.. note::
 | ちょっと作るとすぐに表が大きくなる為、レビュー時にはすぐに分かってもらえるよう説明の順番や見せ方等工夫しよう。

