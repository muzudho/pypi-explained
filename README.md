# PyPI explained

PyPI を説明。  


# 第１章：これは何か？

［自作したPythonパッケージをクラウドからimportできるようにする方法］を説明します。


## 第１節：公式の説明

公式の説明は以下のウェブページにあります。別窓で開いておいてください。本書では実践をしていきます。  

* 📖 [Packaging Python Projects](https://packaging.python.org/en/latest/tutorials/packaging-projects/)


# 第２章：事前準備

## 第２節：［test.pypi.org］、［pypi.org］のアカウント準備

📖[test.pypi.org](https://test.pypi.org/) と 📖[pypi.org](https://pypi.org/) の２つのアカウントを作っておいてください。アカウントの作り方は本書では省略します。この２つのアカウントは別物です。 

* Microsoft Authentication などを使って、2FA（二要素認証）を行うようにします。


## 第３節：ローカルＰＣ　＞　Python環境設定

### 第１項：pip パッケージ更新

```shell
py -m pip install --upgrade pip
```


### 第２項：build パッケージのアップデート

build パッケージは、pypi にアップロードできる形式にファイル圧縮してくれるツールです。  

```shell
py -m pip install --upgrade build
```

// TODO あとで、📄 `pyproject.toml` ファイルでこのビルドツールを指定します。  


### 第３項：　twine パッケージ

`twine` は、圧縮されたファイルを pypi ウェブサイトへアップロードするツールです。  

```shell
py -m pip install --upgrade twine
```


### 第４項：　pkginfo パッケージ

```shell
pip install --upgrade pkginfo
```


### 第５項：　packaging パッケージの削除

古いから、アンインストールしてください。  

```shell
pip install -U packaging
```


## 第４節：ローカルＰＣ　＞　📄［pyproject.toml］ファイルの記述

### 第６項：どのビルドツールを使うか決める

本書では、ビルドツールに Hatchling を使います。  

* Hatchling について詳しく知りたい場合： 📖 [Hatchling > Build system](https://hatch.pypa.io/latest/config/build/#build-system)


### 第７項：自作パッケージで使用しているパッケージを調べる

👇  自作プロジェクトをパッケージ化するためにインストールしておく必要があるパッケージを一覧する方法はありませんが、以下のコマンドを使うと、環境にインストールしたパッケージが一覧できます。自作パッケージに関係のないパッケージ名も出てくるので、手動で選別してください。  

```shell
pip freeze > requirements.txt
```

* 詳しくは：📖 [How to install Python packages with pip and requirements.txt](https://note.nkmk.me/en/python-pip-install-requirements/)

// TODO 後述の　📄［`pyproject.toml`］ファイルの dependencies の項目に移した方がいいか？


### 第８項：既存の📄［pyproject.toml］ファイルをコピーして持ってくる

📄 `pyproject.toml` ファイルを一から書くのは大変なので、既存のものをコピーして、書き替えていくことにします。だいたい、プロジェクト・ルートに置いてあります。  

* 例： 📖 [pyxltree](https://github.com/muzudho/pyxltree)
* 例： 📖 [exshell](https://github.com/muzudho/exshell)


## 第５節：ローカルＰＣ　＞　📄［`pyproject.toml`］ファイルを書く

これから説明していきます。  

* 詳しくは：
    * 📖 [pyproject.toml を書く](https://packaging.python.org/ja/latest/guides/writing-pyproject-toml/)
    * 📖 [【GitHub Actions】自作Pythonパッケージを自動ビルドしてPyPIとGitHubリリースまで一気にデプロイする](https://qiita.com/hanaosan/items/83194c4cd6c80fc3c377)
