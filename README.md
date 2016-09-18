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


