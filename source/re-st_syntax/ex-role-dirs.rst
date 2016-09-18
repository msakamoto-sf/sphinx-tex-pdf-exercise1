.. vim:set expandtab tabstop=2 shiftwidth=2 softtabstop=2 autoindent smartindent ft=rst:

==================================
ロールやディレクティブの練習
==================================


ロール
===========

詳細 : http://docs.sphinx-users.jp/markup/inline.html

サンプル::

  * これが :title:`titleロール` です。
  * これが :emphasis:`emphasisロール` です。
  * これが :literal:`literalロール` です。
  * これが :strong:`strong ロール` です。
  * これが :sub:`subscript ロール(下付き文字)` です。
  * これが :sup:`superscript ロール(上付き文字)` です。
  * これが rfc ロールです。 : :rfc:`2616`
  * これが abbr ロールです。 :abbr:`TLS (Transport Layer Security)`
  * これが command ロールです。 :command:`/usr/sbin/chkconfig`
  * これが file ロールです。 :file:`/etc/hosts`
  * これが kbd ロールです。 :kbd:`Ctrl-C`
  * これが manpage ロールです。 :manpage:`ls(1)`
  * これが mimetype ロールです。 :mimetype:`text/plain`
  * これが mailheader ロールです。 :mimetype:`Subject`
  * これが regexp ロールです。 :regexp:`abc.{3}[-_0-9][^ABC](?:hello\\s\'\"\`world\`\"\')`

→

* これが :title:`titleロール` です。
* これが :emphasis:`emphasisロール` です。
* これが :literal:`literalロール` です。
* これが rfc ロールです。 : :rfc:`2616`
* これが :strong:`strong ロール` です。
* これが :sub:`subscript ロール(下付き文字)` です。
* これが :sup:`superscript ロール(上付き文字)` です。
* これが abbr ロールです。 :abbr:`TLS (Transport Layer Security)`
* これが command ロールです。 :command:`/usr/sbin/chkconfig`
* これが file ロールです。 :file:`/etc/hosts`
* これが kbd ロールです。 :kbd:`Ctrl-C`
* これが manpage ロールです。 :manpage:`ls(1)`
* これが mimetype ロールです。 :mimetype:`text/plain`
* これが mailheader ロールです。 :mimetype:`Subject`
* これが regexp ロールです。 :regexp:`abc.{3}[-_0-9][^ABC](?:hello\\s\'\"\`world\`\"\')`

図表番号(numfig/numref)
=========================

* Sphinx 1.3 以上で対応された numfig (``:numref:``) を使っています。HTMLとLaTeXビルダーが対応。
* http://docs.sphinx-users.jp/markup/inline.html#cross-referencing-figures-by-figure-number
* http://docs.sphinx-users.jp/config.html#confval-numfig

* 図番号参照

  * :numref:`図の別名参照( %s ) <ex-role-dirs-fig1>`
  * :numref:`ex-role-dirs-fig2`

* 表番号参照

  * :numref:`表の別名参照( %s ) <ex-role-dirs-tbl1>`
  * :numref:`ex-role-dirs-tbl2`
  * :numref:`ex-role-dirs-tbl3`

* code-block参照

  * :numref:`code-blockの別名参照( %s ) <ex-role-dirs-src1>`
  * :numref:`ex-role-dirs-src2`
  * :numref:`ex-role-dirs-src3`

----

.. _ex-role-dirs-fig1:

.. figure:: /images/rgb.png

   画像のキャプション1
   画像のキャプション1

.. _ex-role-dirs-fig2:

.. figure:: /images/rgb.jpg

   画像のキャプション2
   画像のキャプション2

.. list-table:: 表キャプション1
  :name: ex-role-dirs-tbl1
  :header-rows: 1

  * - No
    - 名前
    - 値段
  * - 1
    - バナナ
    - 100
  * - 2
    - みかん
    - 150
  * - 3
    - りんご
    - 200

.. list-table:: 表キャプション2
  :name: ex-role-dirs-tbl2
  :header-rows: 1

  * - 日付
    - 場所
    - 天気
  * - 2016-08-01
    - レムリア
    - 晴れ
  * - 2016-09-01
    - アトランティス
    - 雨
  * - 2016-10-01
    - 東京
    - 曇りのち雨

.. list-table:: 表キャプション3
  :name: ex-role-dirs-tbl3
  :header-rows: 1

  * - 書籍タイトル
    - 値段
  * - ぐりとぐら
    - 1,000
  * - 母をたずねて三千里
    - 2,000
  * - 海底２万マイル
    - 1,500

.. code-block:: none
  :caption: シェル操作その1
  :name: ex-role-dirs-src1
  :linenos:

  $ cd /etc
  $ sudo yum update
  $ sudo systemctl start httpd

.. code-block:: java
  :caption: Main.java
  :name: ex-role-dirs-src2
  :linenos:

  public class Main {
      public staic void main(String[] args) {
          System.out.println("Hello, Java");
      }
  }

.. code-block:: c
  :caption: hello.c
  :name: ex-role-dirs-src3
  :linenos:

  #include <stdio.h>

  int main(int argc, char *argv[]) {
      printf("Hello, C\n");
      return 0;
  }


ディレクティブ
================

HTML定義
------------

reST::

    .. meta::
       :token1: 1234567890 ABCD
       :token2: 1234567890 ABCD

    .. title:: <s>"ロール'&</s>やディレクティブの練習
       タイトルの上書き

.. meta::
   :token1: 1234567890 ABCD
   :token2: 1234567890 ABCD

.. title:: <s>"ロール'&</s>やディレクティブの練習
   タイトルの上書き

HTMLベタ書き
-------------

reST::

    .. raw:: html

      <s>HTMLベタ書き</s>
      <s>HTMLベタ書き</s>

      <s>HTMLベタ書き</s>
      <s>HTMLベタ書き</s>

→

.. raw:: html

  <s>HTMLベタ書き</s>
  <s>HTMLベタ書き</s>

  <s>HTMLベタ書き</s>
  <s>HTMLベタ書き</s>

置換機能を使ったHTMLベタ書きのライブラリ化
--------------------------------------------

reST::

    .. |mycheck| raw:: html

      <input type="checkbox" name="mycheckbox" value="on">My CheckBox</input>

    .. |myradio| raw:: html

      <input type="radio" name="myradio">My RadioButton</input>

    ====== ==========
    name   form
    ====== ==========
    radio1 |myradio|
    radio2 |myradio|
    radio3 |myradio|
    check1 |mycheck|
    check2 |mycheck|
    check3 |mycheck|
    ====== ==========

→

.. |mycheck| raw:: html

  <input type="checkbox" name="mycheckbox" value="on">My CheckBox</input>

.. |myradio| raw:: html

  <input type="radio" name="myradio">My RadioButton</input>

====== ==========
name   form
====== ==========
radio1 |myradio|
radio2 |myradio|
radio3 |myradio|
check1 |mycheck|
check2 |mycheck|
check3 |mycheck|
====== ==========

環境変数(envvar)ディレクティブ
-------------------------------

.. envvar:: PATH
  PATH環境変数の説明
  PATH環境変数の説明
  PATH環境変数の説明

.. envvar:: EDITOR
  EDITOR環境変数の説明
  EDITOR環境変数の説明
  EDITOR環境変数の説明

.. envvar:: PAGER
  PAGER環境変数の説明
  PAGER環境変数の説明
  PAGER環境変数の説明

.. envvar:: JAVA_HOME
  JAVA_PATH環境変数の説明
  JAVA_PATH環境変数の説明
  JAVA_PATH環境変数の説明

ロールから参照::

  * :envvar:`PATH`
  * :envvar:`EDITOR`
  * :envvar:`PAGER`
  * :envvar:`JAVA_HOME`

→

* :envvar:`PATH`
* :envvar:`EDITOR`
* :envvar:`PAGER`
* :envvar:`JAVA_HOME`

include, literalinclude ディレクティブ
---------------------------------------

restとしてそのままinclude:

.. include:: /include_demos/demo.rst
  :start-line: 9
  :end-line: 13

リテラルとしてinclude:

.. include:: /include_demos/demo.rst
  :literal:

Cソースのinclude:

.. include:: /include_demos/demo.c
  :code: c

Cソースのliteralinclude:

.. literalinclude:: /include_demos/demo.c
  :language: c
  :linenos:

Javaソースのliteralinclude:

.. literalinclude:: /include_demos/demo.java
  :language: java
  :linenos:

.. _`ex-role-dirs_admonitions-dir`:

Admonitions ディレティブ
--------------------------

.. attention:: attentionディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. caution:: cautionディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. danger:: dangerディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. error:: errorディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. hint:: hintディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. important:: importantディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. note:: noteディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. tip:: tipディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

.. warning:: warningディレクティブです。
   どんな風に見えますか？

   - item1
   - item2
   - item3

