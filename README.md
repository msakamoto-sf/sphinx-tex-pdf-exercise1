# sphinx-tex-pdf-exercise1

Sphinxを使ったTeXと日本語PDF生成の練習その1です。
`platex/dvipdfmx` と `rst2pdf` を使う2パターンを試してます。
https://github.com/msakamoto-sf/sphinx-rest-exercise1 でそのまま実験してみたかったのですが、エラーが多発して収拾が付かなくなったため、`sphinx-quickstart` からまっさらな状態で試してます。

# 実験環境

検証環境 : `CentOS7 (64bit)`

## Python, Sphinx, rst2pdf のインストール

Python と Sphinx 環境：

* https://github.com/msakamoto-sf/sphinx-rest-exercise1 で作成したpyenv, pyenv-virtualenv をそのまま使ってます。
* 具体的には、 https://github.com/msakamoto-sf/sphinx-rest-exercise1/blob/master/.python-version をそのままコピーして使ってます。

rst2pdf は上記pyenv(-virtualenv)環境のpipで最新版をインストールしています：

```
(2.7.12/envs/sphinxt1) [msakamoto@localhost sphinx-rest-exercise1]$ pip install rst2pdf
(...)
Successfully installed pdfrw-0.2 pillow-3.3.1 reportlab-3.3.0 rst2pdf-0.93.dev-r0

$ pyenv rehash
```

最終的なPython, Sphinx, rst2pdf のバージョン：

```
(2.7.12/envs/sphinxt1) [msakamoto@localhost sphinx-tex-pdf-exercise1]$ python --version
Python 2.7.12
(2.7.12/envs/sphinxt1) [msakamoto@localhost sphinx-tex-pdf-exercise1]$ pip list
alabaster (0.7.9)
Babel (2.3.4)
docutils (0.12)
imagesize (0.7.1)
Jinja2 (2.8)
MarkupSafe (0.23)
pdfrw (0.2)
Pillow (3.3.1)
pip (8.1.2)
Pygments (2.1.3)
pytz (2016.6.1)
reportlab (3.3.0)
rst2pdf (0.93.dev-r0)
setuptools (26.1.1)
six (1.10.0)
snowballstemmer (1.2.1)
Sphinx (1.4.6)
sphinx-rtd-theme (0.1.9)
wheel (0.29.0)
```


## pLaTeX, dvipdfmx のインストール

以下のインストール手順に従ってインストールしています。

 * 参考メモ/CentOS7に TeX Live 2016 をインストールして簡単な動作確認をする - Qiita
   * http://qiita.com/msakamoto_sf/items/78c322cb8656615ce134

# TeX, PDFの生成

以下、`squinx-quickstart` 直後の `index.rst` から、徐々に複雑な日本語PDFを生成していく。

## 1. `sphinx-quickstart` 直後の `index.rst`

`index.rst` ：

```
.. sphinx-tex-pdf-exercise1 documentation master file, created by
   sphinx-quickstart on Sun Sep 18 13:29:39 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to sphinx-tex-pdf-exercise1's documentation!
====================================================

Contents:

.. toctree::
   :maxdepth: 2



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
```

TeX経由のPDF生成：

```
$ make latexpdfja
```

rst2pdfによるPDF生成：

1. `conf.py` と `Makefile` の修正：
  * https://github.com/msakamoto-sf/sphinx-tex-pdf-exercise1/commit/0990b22aa12c48ad4de5f90aad379c2c3d0ce14b
  * 内容：
  * `conf.py` の `extensions` に `rst2pdf.pdfbuilder` を追加
  * `conf.py` に最低限度の設定を追加
  * `Makefile` に `pdf` ターゲットを追加
2. `ja` 用のスタイル設定ファイル `ja.json` を追加：
  * https://github.com/msakamoto-sf/sphinx-tex-pdf-exercise1/commit/7cdbbc184db9208b9556a0ff04b179c844281eb5
3. `make pdf` による生成

```
(2.7.12/envs/sphinxt1) [msakamoto@localhost sphinx-tex-pdf-exercise1]$ make pdf
sphinx-build -b pdf -d build/doctrees   source build/pdf
Running Sphinx v1.4.6
making output directory...
loading translations [ja]... done
loading pickled environment... done
building [mo]: targets for 0 po files that are out of date
building [pdf]: targets for 1 source files that are out of date
updating environment: 0 added, 0 changed, 0 removed
looking for now-outdated files... none found
processing MyProject... index
resolving references...
done
writing MyProject... done
build succeeded.

Build finished. The PDF files are in _build/pdf.
```

## 2. sphinx-rest-exercise1 からのrestの移行

https://github.com/msakamoto-sf/sphinx-rest-exercise1 から幾つかrestファイルを移行してみた。

コミット自体はまとめて次になる : https://github.com/msakamoto-sf/sphinx-tex-pdf-exercise1/commit/725e821bc6e2d8eb7fb0325692cd995de3c16530

以下、そのまま移行できなくて、カスタマイズや修正が必要だったり、結局ギブアップした内容について簡単に紹介。

### リストのネスト

かなりリストのネストが深かったため、LaTeXで以下のエラーが発生した。

```
! LaTeX Error: Too deeply nested.
```

→

 * Maximum nesting level of lists in Latex - Stack Overflow
   * http://stackoverflow.com/questions/1935952/maximum-nesting-level-of-lists-in-latex

上記記事を参考に、`conf.py` の `latex_elements` の `preamble` に追記：

```
  'preamble': '''
  \\usepackage{enumitem}
  \\setlistdepth{9}

  \\setlist[itemize,1]{label=$\\bullet$}
  \\setlist[itemize,2]{label=$\\bullet$}
  \\setlist[itemize,3]{label=$\\bullet$}
  \\setlist[itemize,4]{label=$\\bullet$}
  \\setlist[itemize,5]{label=$\\bullet$}
  \\setlist[itemize,6]{label=$\\bullet$}
  \\setlist[itemize,7]{label=$\\bullet$}
  \\setlist[itemize,8]{label=$\\bullet$}
  \\setlist[itemize,9]{label=$\\bullet$}

  \\renewlist{itemize}{itemize}{9}
  ''',
```

### TODOリスト, 引用（ギブアップ）

TODOリストの機能を使ってみたが、 `KeyError: 'ids'` エラーが発生した。
また、引用についてもページ内や他のページにも分割してみたが、同様のエラーが発生した。

 * exception in rst2pdf when the sphinx.ext.todo is present and used · Issue #513 · rst2pdf/rst2pdf
   * https://github.com/rst2pdf/rst2pdf/issues/513

上記issueで紹介されてる修正を `rst2pdf/basenodehandler.py` に加えてみたが、改善されなかったため、ギブアップ。

### index.rst からの外部ファイル取り込み

`source/re-st_syntax/ex-indice.rst` を `index.rst` の `toctree` に加えたところ、`ValueError: too many values to unpack` エラーが発生した。

 * Generating Indices fails when used with Spinx 1.4.1 · Issue #568 · rst2pdf/rst2pdf
   * https://github.com/rst2pdf/rst2pdf/issues/568

上記issueで紹介されてる修正を `rst2pdf/pdfbuilder.py` に加えてみて、改善された。

### アスキーアートの表（ギブアップ）

```
凝った書き方
-------------------

+------------------------+------------+----------+----------+
| Header row, column 1   | Header 2   | Header 3 | Header 4 |
| (header rows optional) |            |          |          |
+========================+============+==========+==========+
| body row 1, column 1   | column 2   | column 3 | column 4 |
+------------------------+------------+----------+----------+
| body row 2             | Cells may span columns.          |
+------------------------+------------+---------------------+
| body row 3             | Cells may  | - Table cells       |
+------------------------+ span rows. | - contain           |
| body row 4             |            | - body elements.    |
+------------------------+------------+---------------------+
```

->以下のエラー発生。解決できず、ギブアップ。

```
! Undefined control sequence.
\@tempc #1->\expandafter \def \@itemlabel
                                          {#1}\def \enit@ref {\expandafter \...
l.1065 \unskip}\relax \unskip}\relax }
                                      \\
```

### GIF, TIFF画像の埋め込み（ギブアップ）

GIF, TIFF画像を埋め込もうとしたのだが、GIF画像の埋め込みの段階で以下のエラーが発生。

```
! LaTeX Error: Cannot determine size of graphic in rgb.gif (no BoundingBox).
```

→ 以下のWikiにあるが、dvipdfmx が対応しなかったので、ギブアップ。（もしかしたら他のツールチェインで回避策もあるかもですが・・・）

 * dvipdfmx/画像のとりこみ - TeX Wiki
   * https://texwiki.texjp.org/?dvipdfmx%2F%E7%94%BB%E5%83%8F%E3%81%AE%E3%81%A8%E3%82%8A%E3%81%93%E3%81%BF

### PNG, JPEG画像の埋め込み

PNG, JPEG画像の埋め込みでも、色々エラーが出たので以下の記事を参考。

 * Sphinx で blockdiag や seqdiag の図をいれた PDF 生成 | BmathLog
   * http://bmath.org/wordpress/?p=2000

→ `conf.py` の `latex_elements` に以下を追加して対応できた。

```
latex_elements = {
#...
     'transition': '',
     'extraclassoptions': ',openany,oneside',
     'classoptions': ',dvipdfmx',
     'babel': '\\usepackage[japanese]{babel}',
}
```

### Javaソースのinclude(code版)（ギブアップ）

```
.. include:: /include_demos/demo.java
  :code: Java
```

→ 以下のエラーが発生。

```
! Missing \endcsname inserted.
<to be read again>
                   \unhbox
l.1716 \DUrole{keyword,declaration}{public}
                                            \DUrole{keyword,declaration}{cla...
```

解決できず、ギブアップ。

以下の書き方は問題ないのに・・・：

```
Javaソースのliteralinclude:

.. literalinclude:: /include_demos/demo.java
  :language: java
  :linenos:
```

# 参考資料

 * SphinxでPDFファイル作成 — Python製ドキュメンテーションビルダー、Sphinxの日本ユーザ会
   * http://sphinx-users.jp/cookbook/pdf/
   * まずはここから。

## rst2pdf 参考資料

 * rst2pdf/rst2pdf: Use a text editor. Make a PDF.
   * https://github.com/rst2pdf/rst2pdf
 * The Rst2pdf Handbook | Rst2pdf
   * http://rst2pdf.ralsina.me/handbook.html
   * Sphinx での使い方は、 http://rst2pdf.ralsina.me/handbook.html#sphinx から解説されてます。
 * rst2pdf拡張を使ったPDFファイル作成 — Python製ドキュメンテーションビルダー、Sphinxの日本ユーザ会
   * http://sphinx-users.jp/cookbook/pdf/rst2pdf.html
   * 2016年9月時点の最新バージョンでも、ほぼほぼこの通りで作れてます。
 * rst2pdf で reStructuredText から PDF を生成する : 紹介マニア
   * http://sakito.jp/python/rst2pdf.html
 * SphinxのPDF出力をrst2pdfで試す@Windows64bit | Futurismo
   * http://futurismo.biz/archives/946

## LaTeX経由 参考資料

 * LaTeX経由でのPDF作成 — Python製ドキュメンテーションビルダー、Sphinxの日本ユーザ会
   * http://sphinx-users.jp/cookbook/pdf/latex.html
   * 2016-09時点の最新 Sphinx 1.4系なら、必要なパッチは当たってるようです。
 * sphinxで日本語PDFを作成する方法 - Qiita
   * http://qiita.com/graceful_life/items/3287fb8b82e2fec1aa49
   * 少し古いバージョンの情報のようですが、画像埋め込みなど参考になります。
 * Re: SphinxのLaTeXのフォーマットをいじる - Hack like a rolling stone
   * http://tk0miya.hatenablog.com/entry/2014/07/17/003104
   * Sphinxといいますか、ほぼ LaTeX 技の話になってます。preamble設定で好きなLaTeXを埋め込めます。
 * Sphinx と LaTeX を使うときの 小技
   * https://gist.github.com/uchida/4545280
   * 細かいノウハウ。
 * sphinxのPDF出力ではまった - yuitowest's blog
   * http://yuitowest.hatenablog.com/entry/20111114/1321262351
   * AAで作成した表でトラブルになった例
 * Maximum nesting level of lists in Latex - Stack Overflow
   * http://stackoverflow.com/questions/1935952/maximum-nesting-level-of-lists-in-latex
   * リストアイテムのネスト段数の拡張について。

## `sphinx-quickstart` オプション

最初に `sphinx-quickstart` でプロジェクトを生成した時のオプション：

```
(2.7.12/envs/sphinxt1) [msakamoto@localhost sphinx-tex-pdf-exercise1]$ sphinx-quickstart
Welcome to the Sphinx 1.4.6 quickstart utility.

Please enter values for the following settings (just press Enter to
accept a default value, if one is given in brackets).

Enter the root path for documentation.
> Root path for the documentation [.]:

You have two options for placing the build directory for Sphinx output.
Either, you use a directory "_build" within the root path, or you separate
"source" and "build" directories within the root path.
> Separate source and build directories (y/n) [n]: y

Inside the root directory, two more directories will be created; "_templates"
for custom HTML templates and "_static" for custom stylesheets and other static
files. You can enter another prefix (such as ".") to replace the underscore.
> Name prefix for templates and static dir [_]:

The project name will occur in several places in the built documentation.
> Project name: sphinx-tex-pdf-exercise1
> Author name(s): msakamoto-sf

Sphinx has the notion of a "version" and a "release" for the
software. Each version can have multiple releases. For example, for
Python the version is something like 2.5 or 3.0, while the release is
something like 2.5.1 or 3.0a1.  If you don't need this dual structure,
just set both to the same value.
> Project version: 1.0
> Project release [1.0]: 0.1

If the documents are to be written in a language other than English,
you can select a language here by its language code. Sphinx will then
translate text that it generates into that language.

For a list of supported codes, see
http://sphinx-doc.org/config.html#confval-language.
> Project language [en]: ja

The file name suffix for source files. Commonly, this is either ".txt"
or ".rst".  Only files with this suffix are considered documents.
> Source file suffix [.rst]:

One document is special in that it is considered the top node of the
"contents tree", that is, it is the root of the hierarchical structure
of the documents. Normally, this is "index", but if your "index"
document is a custom template, you can also set this to another filename.
> Name of your master document (without suffix) [index]:

Sphinx can also add configuration for epub output:
> Do you want to use the epub builder (y/n) [n]:

Please indicate if you want to use one of the following Sphinx extensions:
> autodoc: automatically insert docstrings from modules (y/n) [n]:
> doctest: automatically test code snippets in doctest blocks (y/n) [n]:
> intersphinx: link between Sphinx documentation of different projects (y/n) [n]:
> todo: write "todo" entries that can be shown or hidden on build (y/n) [n]: y
> coverage: checks for documentation coverage (y/n) [n]:
> imgmath: include math, rendered as PNG or SVG images (y/n) [n]:
> mathjax: include math, rendered in the browser by MathJax (y/n) [n]:
> ifconfig: conditional inclusion of content based on config values (y/n) [n]:
> viewcode: include links to the source code of documented Python objects (y/n) [n]:
> githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n]:

A Makefile and a Windows command file can be generated for you so that you
only have to run e.g. `make html' instead of invoking sphinx-build
directly.
> Create Makefile? (y/n) [y]:
> Create Windows command file? (y/n) [y]:

Creating file ./source/conf.py.
Creating file ./source/index.rst.
Creating file ./Makefile.
Creating file ./make.bat.

Finished: An initial directory structure has been created.

You should now populate your master file ./source/index.rst and create other documentation
source files. Use the Makefile to build the docs, like so:
   make builder
where "builder" is one of the supported builders, e.g. html, latex or linkcheck.
```

