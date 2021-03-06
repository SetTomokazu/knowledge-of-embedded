.. index:: VS Code
    single: テキストエディタ; VS Code

.. _VS Code:

VS Code
==================
正直全部こいつでいいんじゃないかと思う


特徴
------
| Parserがとにかく優秀で、以下のようなソースもどこが有効行なのかを判別してくれる。

.. code-block:: c

    #define __DEBUG__
    #define __RELEASE__ 1

    #if (__DEBUG__ == 1)
        hoge = 1;
    #else
    #if (__RELEASE__ == 1)
        hoge = 2;
    #else
        hoge = 3;
    #endif
    #endif

| 拡張機能によってCソース以外に記述されているプロジェクトマクロも判別可能である。
| 通常のエディタでできる機能は当然のようにサポート

* 単語補完
* 検索、Grep
* 定義元へのジャンプ
* 単語フォーカス中にその定義内容表示
* プロジェクト毎の書式を定義し自動フォーマット調整
* バージョン管理ツールとの連携
* ターミナルを表示できるため画面上でビルドコマンド実行可能

| つまり、コード編集からビルド、コミットが単一ウィンドウ上で完結する。
