.. index:: Linker

.. _Linker:

Linker(リンカ)
============================
| コンパイルされたオブジェクトを繋ぎ合わせ配置する。
| 担当は主に以下の二つ

* 他オブジェクトへの参照の解決
    externあなたです。

* 指定された :ref:`Section` へのオブジェクト配置

引数
--------

* コンパイルしたオブジェクトファイル共

* 対象マイコン名
    | マイコンによってROMやRAMの場所が違うのだから当然必要である。
    | 無い場合はそもそものROMやRAMの領域を :ref:`Section` 共々渡している

*  :ref:`Section` 定義

出力
-------
* :ref:`MAPファイル`
* :ref:`HEXファイル`
