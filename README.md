# PyPI explained

PyPI を説明。  


# 第１章：これは何か？

［自作したPythonパッケージをクラウドからimportできるようにする方法］を説明します。


## 第１節：公式の説明

公式の説明は以下のウェブページにあります。別窓で開いておいてください。本書では実践をしていきます。  

* 📖 [Packaging Python Projects](https://packaging.python.org/en/latest/tutorials/packaging-projects/)


# 第２章：build前準備

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


## 第５節：ローカルＰＣ　＞　自作プロジェクトの構成

### 第９項：　README.md について

トップ・ディレクトリーの 📄 `README.md` テキストは pypi.org のパッケージのページの README としても使われるので、それを想定して書くこと。  
画像は相対パスではなくURLを指定すること。  


### 第１０項：　ディレクトリー階層の例

👇　１例として、ディレクトリー階層は以下のようにする。  

```plaintext
📁 {REPOSITORY_NAME}/    # GitHub のリポジトリー名に対応。詳しくはソースコードの現物参照
├─ 📄 src/
│   └─ 📄 {PACKATE_NAME}/    # Python パッケージ名に対応。詳しくはソースコードの現物参照
│      ├─ 📄 __init__.py
│      └─ others...
└─ 📄 pyproject.toml
```


### 第１１項：ローカルＰＣ　＞　📄［`pyproject.toml`］ファイルを書きあげる

以下のリンクを参考に、📄［`pyproject.toml`］ファイルを書きあげてください。本書では省略します。  

* 詳しくは：
    * 📖 [pyproject.toml を書く](https://packaging.python.org/ja/latest/guides/writing-pyproject-toml/)
    * 📖 [【GitHub Actions】自作Pythonパッケージを自動ビルドしてPyPIとGitHubリリースまで一気にデプロイする](https://qiita.com/hanaosan/items/83194c4cd6c80fc3c377)


# 第３章：buildについて

## 第６節：　再確認

`build` を**実行する前**に:  

* 📄 `pyproject.toml` のバージョンを設定したか確認しておくこと
* デプロイしたいファイルで、GitHub にプッシュし忘れているファイルが残っていれば、プッシュしてください
* ファイルの保存のし忘れがあれば、ファイルの保存をしてください


## 第７節：　build実行

👇 pyproject.toml を書き上げたら、 `build` を実行する。  

```shell
py -m build
```

`build` を実行すると、 `dist` フォルダーが作成される。  

例：  

```plaintext
📁 dist/
├─ 📄 {PACKATE_NAME}-0.0.1-py2.py3-none-any.whl     # Python パッケージ名に対応。詳しくはソースコードの現物参照
└─ 📄 {PACKATE_NAME}-0.0.1.tar.gz
```

これが pypi にアップロードするファイルだ。  


# 第４章：アップロード


### 第１２項：書式チェック

👇　書式チェック。圧縮ファイルに対して行う  

```shell
twine check dist/*
```

* エラーがでたら、書式を確認する。
    * 📖 [Writing your pyproject.toml](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/)


### 第１３項：twine実行

twine を実行する前に、 📄 `pyproject.toml` のバージョンの数を設定（２回目以降なら上げる）しておくこと  

👇 twine を実行する  

```shell
py -m twine upload --repository testpypi dist/*

# 細かいログが見たいとき
#py -m twine upload --repository testpypi --verbose dist/*
```

APIトークンを尋ねられるので、 `pypi-` プレフィックスを付けたまま入力する  


## 第５章：アップロードされたものを確認しにいく

### 第１４項：［test.pypi.org］にログイン

👇 アップロードされたら、test.pypi.org を見に行く  

[test.pypi.org](https://test.pypi.org/) に Fire Fox でログインする（Google Chrome や Edge では二要素認証が通らないことがあった）  

https://test.pypi.org/account/login/

**test.pypi.org の［アカウント設定］の［API トークン］の欄から、［APIトークンの追加］ボタンをクリックする。**  
スコープは `アカウント全体` を選ぶ。発行されたAPIトークンは再発行されないので、どこかに記憶しておく  


## 第６節：参考記事

* デプロイのために
    * 📖 [【Python】PyPIに自作ライブラリを登録する](https://qiita.com/gsy0911/items/702f43100e5abdefd318)
        * 📖 [PyPIパッケージ定義ファイル作成方法 - __init__.py setup.py MANIFEST.in の書き方](https://qiita.com/shinichi-takii/items/6d1063e0aa3f79e599f0)
    * 📖 [【GitHub Actions】自作Pythonパッケージを自動ビルドしてPyPIとGitHubリリースまで一気にデプロイする](https://qiita.com/hanaosan/items/83194c4cd6c80fc3c377)
