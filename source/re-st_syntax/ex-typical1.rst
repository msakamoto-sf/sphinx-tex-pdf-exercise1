.. vim:set expandtab tabstop=2 shiftwidth=2 softtabstop=2 autoindent smartindent ft=rst:

.. include:: /definitions.txt

==================================
restructured text の練習
==================================

.. contents:: このページ内の目次
   一覧

段落とHTMLエスケープ
=====================

<s>"こんにちは改行'&</s>
<s>"こんにちは改行'&</s>
<s>"こんにちは改行'&</s>

----

こんにちは改行
こんにちは改行
こんにちは改行

----

.. _`label - quote block`:

引用
==========

これは実は、定義リストになってしまう。::

    こんにちは改行
      (indent)こんにちは改行引用a
        (indent)こんにちは改行引用b
          (indent)こんにちは改行引用c
        (indent)こんにちは改行引用b

引用をするなら、行を開けてからインデント。

こんにちは改行

  (indent)こんにちは改行引用a
  (indent)こんにちは改行引用b

    (indent)こんにちは改行引用c
    (indent)こんにちは改行引用d

      (indent)こんにちは改行引用c
      (indent)こんにちは改行引用e

    (indent)こんにちは改行引用f
    (indent)こんにちは改行引用g

  (indent)こんにちは改行引用h
  (indent)こんにちは改行引用i

.. _`label - newline and indent`:

改行とインデントをそのまま表示
-------------------------------

| 改行とインデントを
|   そのまま表示
|      しますん。


.. _`label - code block`:

脚注
=====

脚注を作成するためのマークアップは、``[#]_`` で自動採番 [#]_ することができます。 [#]_

もちろん手動採番 [3]_ することも可能 [5]_ ですが、ちょっとややこしくなりそうですね。

脚注を番号ではなくラベル [#footnote-label1]_ で作ることもできます。大きめの文書ならこっちが良いですね。


コードブロック
================

コードブロック::

  ほげ::

    コードブロック

  ぼへ

----

``code-block`` ディレクティブ:

ハイライトバリエーション : http://pygments.org/docs/lexers/

.. code-block:: none
  :linenos:

  $ cd /etc
  $ sudo yum update
  $ sudo systemctl start httpd

.. code-block:: java
  :linenos:

  public class Main {
      public staic void main(String[] args) {
          System.out.println("Hello, Java");
      }
  }

.. code-block:: c
  :linenos:

  #include <stdio.h>

  int main(int argc, char *argv[]) {
      printf("Hello, C\n");
      return 0;
  }

.. code-block:: python
  :caption: this.py
  :name: hello.py
  :linenos:
  :emphasize-lines: 3,5

  def some_function():
    interesting = False
    print 'This line is highlighted.'
    print 'This one is not...'
    print '...but this one is.'

.. code-block:: php
  :linenos:

  <?php
  header('Content-Type: text/html');
  phpinfo();

.. code-block:: sql
  :linenos:

  CREATE DATABASE testdb1;
  CREATE TABLE tb1 (
    id integer primary key auto_increment,
    name varchar(255) not null,
    age integer
    );
  INSERT INTO tb1 (name, age) VALUES ('jon', 10), ('job', 20), ('bob', 30);
  SELECT id, name, age FROM tb1 WHERE age > 10 ORDER BY id DESC;

.. _`label - colon variation`:

コロンのバリエーション
------------------------

普通にコロン::

  code block1

----

コロン1こだけ。:

  code block2

----

ソースコード上はいきなりコロンはできない。(Unexpected indentation.)::

  ほげ
  ::

    code block3

----

段落最初がいきなりコロン（これがリテラルブロックの標準）

::

  code block 4

----

コロンの前に空白 ::

  code block 5

----

段落最初が空白 + コロン（これがベストか。）

 ::

   code block 6

----

もしかしてインデント要らなくね？ ::

  もしかしてインデント要らなくね？

   ::

  code block 7

→駄目だった・・・。(``Literal block expected; none found.``)

.. _`label - comment out`:

コメントアウト
================

行単位::

  .. comment-outed1
  .. comment-outed2
  .. comment-outed3

.. comment-outed1
.. comment-outed2
.. comment-outed3

複数行ならインデントしてまとめられる::

  ..
    blocked comment-outed1
    blocked comment-outed2
    blocked comment-outed3

..
  blocked comment-outed1
  blocked comment-outed2
  blocked comment-outed3


.. _`label - list samples`:

リスト
=======

.. _`label - list without number`:

番号無し
----------

* item1

  * item1-1
    foo
    bar
    baz

    * item1-1-1
      ::

        code block AAAA
        code block BBB
        code block BBB
        code block BBB

      * item1-1-1-1
        FOO

          BAR

            BAZ

        * item1-1-1-1-1

          | 改行とインデントを
          |   そのまま表示
          |       しますん。

          * item1-1-1-1-1-1

  * item1-2

    .. code-block:: python
      :caption: this.py
      :name: hello2.py
      :emphasize-lines: 3,5

      def some_function():
        interesting = False
        print 'This line is highlighted.'
        print 'This one is not...'
        print '...but this one is.'

  * item1-3

* item 2

複数種類のbullet listsを連続させることはできない。::

  * item1
  + item2
  - item3

→ ``WARNING: Bullet list ends without a blank line; unexpected unindent.``

+ item 3a

  * item3a-1

    - item3a-1-1

+ item 3b

- item 4a
  ネストで、別の種類のbullet listsを混ぜる事はできる。
- item 4b

.. _`label - list with number`:

番号あり。
----------

#. ordered-1

   #. ordered-1a

     #. ordered-1aa

       #. ordered-1aaa

     #. ordered-1ab
     #. ordered-1ac

   #. ordered-1b
   #. ordered-1c

#. ordered-2
#. ordered-3

----

OK:

1. ordered-1

   1. ordered-1a

     #. ordered-1aa

       #. ordered-1aaa

     #. ordered-1ab
     #. ordered-1ac

   2. ordered-1b
   3. ordered-1c

2. ordered-2
3. ordered-3

NG:

1. ordered-1

   1-1. ordered-1a

     #. ordered-1aa

       #. ordered-1aaa

     #. ordered-1ab
     #. ordered-1ac

   1-2. ordered-1b
   1-3. ordered-1c

1. ordered-2
1. ordered-3

番号あり/なし混在
-------------------

* item1

  #. item1a
  #. item1b

    * item1b-1
    * item1b-2

      1. item1b-2a
      2. item1b-2a
         ::

          code-blockAAA

            code-blockBBB

          code-blockCCC

      3. item1b-2a

    * item1b-3

  #. item1b

* item2

.. _`label - definition list`:

定義リスト
-------------

term1
    description
    description

    description

    .. code-block:: python
      :caption: this.py
      :name: hello3.py
      :emphasize-lines: 3,5

      def some_function():
        interesting = False
        print 'This line is highlighted.'
        print 'This one is not...'
        print '...but this one is.'

    description

term2
    description
    description

    * item1
    * item2

      * item2a
      * item2b

    * item3

    description
    ::

      codeblock AAA
      codeblock BBB
      codeblock CCC

    description

.. _`label - inline format`:

*italic*/**bold**/``literal``
==================================

*強調(italic)*/**強い強調(bold)**/``リテラル表記``::

  * *強調(italic)*
  * **強い強調(bold)**
  * ``リテラル表記``

→

* *強調(italic)*
* **強い強調(bold)**
* ``リテラル表記``

.. _`label-escape-rest-markup`:

reSTマークアップのエスケープ
=============================

\* あああ \*, \** ううう \**, \`えええ\`, \``おおお\``

\.. かかか \:ABCDEF\:\`abcdef\`

\= aaa

\# bbb

\- ccc

\+ ddd


.. _`label - table block notation`:

テーブル
=========

簡単な書き方
---------------

====== ========== ======
col1   col2       col3
====== ========== ======
val1   val2       val3
val1   val2       val3
val1   val2       val3
val1   val2       val3
val1   val2       val3
====== ========== ======

=====  =====  ======
   Inputs     Output
------------  ------
  A      B    A or B
=====  =====  ======
False  False  False
True   False  True
False  True   True
True   True   True
=====  =====  ======


URLリンクとラベルと参照と画像
=================================

.. _label_url_link_writing:

URLリンクの書き方
--------------------

コード::

  * http://sphinx-doc.org/
  * `sphinx-doc <http://sphinx-doc.org>`_
  * Sphinx-doc_
  * `example.com site`_

  (...)

  .. _Sphinx-user: http://docs.sphinx-users.jp/
  .. _example.com site: http://www.example.com/

→

* http://sphinx-doc.org/
* `sphinx-doc <http://sphinx-doc.org>`_
* Sphinx-user_
* `example.com site`_

.. _Sphinx-user: http://docs.sphinx-users.jp/
.. _example.com site: http://www.example.com/


.. _label_link_in_page:

同じページ内のラベル参照
---------------------------

コード::

  .. _`label sample`:

  ページ内リンクのテスト見出し
  ##############################
  hello

  ここで :ref:`label sample` を参照。

  ページ先頭の方にある :ref:`引用ブロックのサンプル<label - quote block>` を参照。

→

.. _`label sample`:

ページ内リンクのテスト見出し
##############################
hello

ここで :ref:`label sample` を参照。

ページ先頭の方にある :ref:`引用ブロックのサンプル<label - quote block>` を参照。



置換機能による共通化・省力化
=============================

インラインの置換::

  * |ssl|
  * |tls|
  * |rest|
  * |http|
  * |https|
  * |chkconfig|
  * |systemctl|
  * |hosts|
  * |crontab|
  * |passwd|
  * |kbd_ctrl-c|
  * |kbd_ctrl-v|
  * |kbd_esc|
  * |kbd_meta|
  * |man_ls|

→

* |ssl|
* |tls|
* |rest|
* |http|
* |https|
* |chkconfig|
* |systemctl|
* |hosts|
* |crontab|
* |passwd|
* |kbd_ctrl-c|
* |kbd_ctrl-v|
* |kbd_esc|
* |kbd_meta|
* |man_ls|
* |logo_png|
* |logo_jpg|


----

.. list-table:: embedded replaces

  * - ``|release|``
    - |release|
  * - ``|version|``
    - |version|
  * - ``|today|``
    - |today|

----

.. list-table:: images in table

  * - PNG image
    - |logo_png|
  * - JPEG image
    - |logo_jpg|

フィールド表記
===================

:Date: |today|
:Version: |release|
:Authors: - author1
          - author2
          - author3
:インデント入り: この文章は、途中で
                インデントされてます。
                どう表示されるかな？


.. rubric:: Footnotes

.. [#] 脚注1
.. [#] 脚注2
.. [#] 脚注3
.. [4] 脚注4
.. [5] 脚注5
.. [#footnote-label1] 脚注文書です。
   脚注文書です。
   脚注文書です。
   脚注文書です。
   脚注文書です。

