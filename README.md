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


