.. index:: pragma

.. _pragma:

pragma
============================
| コンパイラやリンカに対して特別な命令を指定する。
| 組み込みでの主な用途はセクションの配置指定である。

.. code-block:: c

    /* 記述例 */
    #pragma section=DATA
    unsigned int buffer;

    #pragma section=CODE
    void func(void);

.. note:: この記述はコンパイラ依存の為、マイコンが変われば記述書式も大きく異なる。
