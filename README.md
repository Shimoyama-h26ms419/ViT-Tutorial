# ViT-Tutorial

## 0. TL;DR
ViTの基本的な動かし方を説明するためのリポジトリです。

学部時代に行った [**卒業研究**](https://github.com/Shimoyama-h22s4059/GR2025) がごちゃついたので整理しました。

## 1. Overview

### 研究テーマ
> 「Vision Transformer によるアミノ酸配列のグラフ表示画像のGPCRクラス分類」

### 目的
- 既存のCNNに代わり、Vision Transformerを使うことにより分類の性能向上を目指す

## 2. Background
- 近年、タンパク質のファミリー分類を行う研究が盛んに行われている
- CNNでは勾配消失問題により長距離のアミノ酸間の特徴を捉えづらい、などの問題が発生する
- Vision Transformerにより、この問題を解決できないかと考えた

## 3. Structure
- [📂 `ViT-Tutorial`](/)（このリポジトリ）
  - [📂 `data`](/data)（データセットなどを保管する）
  - [📂 `images`](/data)（作成した画像データを保管する）
  - [📂 `jupyter`](/jupyter)（Jupyter Notebookを保管する）
  - [📂 `labels`](/jupyter)（ラベルデータを保管する）
  - [📂 `models`](/models)（作成したモデルを保管する）
  - [📄 `app.py`](/app.py)（Flaskの起動ファイル）
  - [📄 `requirements.txt`](/requirements.txt)（pipの依存関係の一覧）

## 4. Setup
まずは環境構築をしましょう。

### 4.0 環境
- Python：`3.14.4`
- PyTorch：`2.11.0+cu130`
- [`requirements.txt`](/requirements.txt) に必要ライブラリを記載

### 4.1 Pythonのインストール
1. [**Python公式ページ**](https://www.python.org/downloads/release/python-3144/) から **Python 3.14.4** をインストールします。
2. `PATH` を通してターミナルからPythonを起動できるようにします。

```
> python -V
Python 3.14.4
```

### 4.2 リポジトリのクローン
このリポジトリをクローンしましょう。
ディレクトリは分かりやすい場所ならばどこでも構いません。
```
> git clone https://github.com/Shimoyama-h26ms419/ViT-Tutorial.git
```

次に、作業ディレクトリに移動します。
```
> cd ./ViT-Tutorial
```

### 4.3 仮想環境の作成
仮想環境（venv）の作成を行います。
以下のコマンドで仮想環境を `.venv` ディレクトリに作成します。
```
> py -3.14 -m venv ./.venv
```

次に仮想環境をアクティブにします。
```
> ./.venv/Script/activate
```

コンソールのユーザー名の左に `(.venv)` と表示されれば OK です。
```
(.venv) PS C:\path\to\ViT-Tutorial>
```

仮想環境を非アクティブにしたいときは、以下のコマンドを実行します。
```
> deactivate
```

### 4.4 必要ライブラリのインストール
必要なライブラリなどを一括でインストールします。
以下のコマンドを順に実行してインストールします。

```
> pip install torch torchvision --index-url https://download.pytorch.org/whl/cu130
> pip install ipywidgets transformers[torch]
> pip install -r requirements.txt
```

インストールが終了したら、CUDAが対応してるかを確認しましょう。
`cuda` が出ればGPU対応、`cpu` が出ればGPUは非対応です。
```python
import torch

print("cuda" if torch.cuda.is_available() else "cpu")
```

## 5. Using Vision Transformer

### 5.0 MNIST Dataset
MNIST Datasetを用いてVision Transformerの画像分類の汎化性能を評価します。

Jupyter Notebook は [<img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Jupyter_logo.svg" width=16px height=16px> `/jupyter/vit-mnist.ipynb`](/jupyter/vit-mnist.ipynb) から利用できます。

### 5.1 BIAS-PROFS Dataset
[**BIAS-PROFS**](https://www.cs.kent.ac.uk/projects/biasprofs/files/gds_dataset.zip) から `gds_dataset.zip` をダウンロードします。

解凍して以下のような構造にします。

- [`📂 data`](/data)
  - `📂 gds_dataset`
    - `📄 ClassA_Adrenergic_Adrenergic.txt`
    - `...`
    - `📄 ClassE_cAMP_cAMP.txt`

Jupyter Notebook は以下から利用可能です
- データセットの加工（グラフ表示画像の作成・ラベルCSV作成）：[<img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Jupyter_logo.svg" width=16px height=16px> `/jupyter/processing-bias-profs.ipynb`](/jupyter/processing-bias-profs.ipynb)
- 機械学習：[<img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Jupyter_logo.svg" width=16px height=16px> `/jupyter/vit-bias-profs.ipynb`](/jupyter/vit-bias-profs.ipynb)


### 5.2 InterPro Dataset
> [!note]
> 現在工事中です

## 6. Dataset
使用したデータセットは以下の通りです。

| Dataset       | URL                                                         |
|:--------------|:------------------------------------------------------------|
| MNIST Dataset | https://huggingface.co/datasets/ylecun/mnist                |
| BIAS-PROFS    | https://www.cs.kent.ac.uk/projects/biasprofs/downloads.html |
| InterPro      | https://www.ebi.ac.uk/interpro/                             |

### 6.1 InterProの詳細

#### Class
[📄 `/data/interpro-class.md`](/data/interpro-class.md) を参照してください

#### Family
[📄 `/data/interpro-family.md`](/data/interpro-family.md) を参照してください

## 7. Notice
> [!caution]
> 工事中

## 8. Future Prospects
- [MaxViT](https://arxiv.org/abs/2204.01697) を使ってみる
- GPCR以外のデータセットでの検証
- [AAindex](https://www.genome.jp/aaindex/) の指標の組み合わせの検証

## 9. References
- Kawashima, Shuichi, and Minoru Kanehisa. "AAindex: amino acid index database." _Nucleic acids research_ 28.1 (2000): 374-374.
- Vaswani, Ashish, et al. "Attention is all you need." _Advances in neural information processing systems 30_ (2017).
- Dosovitskiy, Alexey, et al. "An image is worth 16x16 words: Transformers for image recognition at scale." _arXiv preprint arXiv:2010.11929_ (2020).
- 山口秀輝, and 齋藤裕. "タンパク質の言語モデル." _JSBi Bioinformatics Review_ 4.1 (2023): 52-67.
