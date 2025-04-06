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

// あとで、📄 `pyproject.toml` ファイルでこのビルドツールを指定します。  


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

