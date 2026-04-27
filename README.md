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

以下のコマンドで仮想環境を非アクティブにします。
```
> deactivate
```

### 4.4 必要ライブラリのインストール
必要なライブラリなどを一括でインストールします。
以下のコマンドによりインストールします。

```
> pip install -r requirements.txt
```

PyTorchは以下のコマンドにより別途インストールする必要があります。
```
> pip install torch torchvision --index-url https://download.pytorch.org/whl/cu130
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
> [!note]
> 現在工事中です


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

| Class |                                                             Accession No.                                                             | Name                                       |
|:-----:|:-------------------------------------------------------------------------------------------------------------------------------------:|:-------------------------------------------|
|   A   |                                 [IPR000276](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000276/)                                 | G protein-coupled receptor, rhodopsin-like |
|   B   |                                 [IPR000832](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000832/)                                 | GPCR, family 2, secretin-like              |
|   C   |                                 [IPR000337](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000337/)                                 | GPCR, family 3                             |
|   D   |                                                                   -                                                                   | -                                          |
|   E   |                                                                   -                                                                   | -                                          |
|   F   |                                 [IPR000539](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000539/)                                 | Frizzled/Smoothened, 7TM                   |

#### Family

| Class |                             Accession No.                             | Name                                                                               |
|:-----:|:---------------------------------------------------------------------:|:-----------------------------------------------------------------------------------|
|   A   | [IPR000018](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000018/) | P2Y purinoceptor 4                                                                 |
|   A   | [IPR000025](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000025/) | Melatonin receptor family                                                          |
|   A   | [IPR000142](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000142/) | P2Y purinoceptor 1                                                                 |
|   A   | [IPR000204](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000204/) | Orexin receptor family                                                             |
|   A   | [IPR000356](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000356/) | P2Y2 purinoceptor                                                                  |
|   A   | [IPR000371](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000371/) | P2Y3 purinoceptor                                                                  |
|   A   | [IPR000405](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000405/) | Galanin receptor family                                                            |
|   A   | [IPR000499](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000499/) | Endothelin receptor family                                                         |
|   A   | [IPR000503](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000503/) | Histamine H2 receptor                                                              |
|   A   | [IPR000586](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000586/) | Somatostatin receptor family                                                       |
|   A   | [IPR000611](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000611/) | Neuropeptide Y receptor family                                                     |
|   A   | [IPR000670](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000670/) | Urotensin II receptor                                                              |
|   A   | [IPR000723](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000723/) | G protein-coupled receptor 3/6/12 orphan                                           |
|   A   | [IPR000725](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000725/) | Olfactory receptor                                                                 |
|   A   | [IPR000820](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000820/) | Proto-oncogene Mas                                                                 |
|   A   | [IPR000826](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000826/) | Formyl peptide receptor-related                                                    |
|   A   | [IPR000921](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000921/) | Histamine H1 receptor                                                              |
|   A   | [IPR000929](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000929/) | Dopamine receptor family                                                           |
|   A   | [IPR000995](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000995/) | Muscarinic acetylcholine receptor family                                           |
|   A   | [IPR001069](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001069/) | 5-Hydroxytryptamine 7 receptor                                                     |
|   A   | [IPR001350](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001350/) | G10D orphan receptor                                                               |
|   A   | [IPR001402](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001402/) | Prolactin-releasing peptide receptor                                               |
|   A   | [IPR001418](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001418/) | Opioid receptor                                                                    |
|   A   | [IPR001520](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001520/) | 5-Hydroxytryptamine 4 receptor                                                     |
|   A   | [IPR001556](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001556/) | Bombesin receptor-like                                                             |
|   A   | [IPR001634](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001634/) | Adenosine receptor                                                                 |
|   A   | [IPR001658](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001658/) | Gonadotrophin-releasing hormone receptor family                                    |
|   A   | [IPR001671](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001671/) | Melanocortin/ACTH receptor                                                         |
|   A   | [IPR001681](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001681/) | Neurokinin receptor                                                                |
|   A   | [IPR001760](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001760/) | Opsin                                                                              |
|   A   | [IPR001793](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001793/) | Retinal pigment epithelium GPCR                                                    |
|   A   | [IPR001817](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001817/) | Vasopressin receptor                                                               |
|   A   | [IPR001973](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001973/) | P2Y6 purinoceptor                                                                  |
|   A   | [IPR002002](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002002/) | Octopamine receptor                                                                |
|   A   | [IPR002120](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002120/) | Thyrotropin-releasing hormone receptor                                             |
|   A   | [IPR002131](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002131/) | Glycoprotein hormone receptor family                                               |
|   A   | [IPR002230](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002230/) | Cannabinoid receptor family                                                        |
|   A   | [IPR002231](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002231/) | 5-hydroxytryptamine receptor family                                                |
|   A   | [IPR002232](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002232/) | 5-Hydroxytryptamine 6 receptor                                                     |
|   A   | [IPR002233](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002233/) | Adrenoceptor family                                                                |
|   A   | [IPR002275](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002275/) | Chemerin-like receptor 2                                                           |
|   A   | [IPR002276](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002276/) | G protein-coupled receptor 4 orphan                                                |
|   A   | [IPR002282](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002282/) | Platelet-activating factor receptor                                                |
|   A   | [IPR002962](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002962/) | Peropsin                                                                           |
|   A   | [IPR003904](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003904/) | Apelin receptor                                                                    |
|   A   | [IPR003905](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003905/) | Growth hormone secretagogue receptor/motilin receptor                              |
|   A   | [IPR003909](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003909/) | G protein-coupled receptor 37 orphan                                               |
|   A   | [IPR003912](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003912/) | Protease-activated receptor                                                        |
|   A   | [IPR003980](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003980/) | Histamine H3 receptor                                                              |
|   A   | [IPR003981](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003981/) | Leukotriene B4 receptor                                                            |
|   A   | [IPR003984](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003984/) | Neurotensin receptor                                                               |
|   A   | [IPR004061](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR004061/) | Sphingosine 1-phosphate receptor                                                   |
|   A   | [IPR004065](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR004065/) | Lysophosphatidic acid receptor                                                     |
|   A   | [IPR004071](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR004071/) | Cysteinyl leukotriene receptor                                                     |
|   A   | [IPR005388](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR005388/) | G2A lysophosphatidylcholine receptor                                               |
|   A   | [IPR005389](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR005389/) | OGR1 sphingosylphosphorylcholine receptor                                          |
|   A   | [IPR005390](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR005390/) | Neuromedin U receptor                                                              |
|   A   | [IPR005394](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR005394/) | P2Y12 purinoceptor                                                                 |
|   A   | [IPR005395](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR005395/) | Neuropeptide FF receptor family                                                    |
|   A   | [IPR005464](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR005464/) | Psychosine receptor                                                                |
|   A   | [IPR005466](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR005466/) | P2Y14 purinoceptor                                                                 |
|   A   | [IPR008102](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008102/) | Histamine H4 receptor                                                              |
|   A   | [IPR008103](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008103/) | KiSS-1 peptide receptor                                                            |
|   A   | [IPR008109](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008109/) | P2Y13 purinoceptor                                                                 |
|   A   | [IPR008112](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008112/) | Relaxin receptor                                                                   |
|   A   | [IPR008361](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008361/) | Melanin-concentrating hormone receptor                                             |
|   A   | [IPR008365](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008365/) | Prostanoid receptor                                                                |
|   A   | [IPR009126](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR009126/) | Cholecystokinin receptor                                                           |
|   A   | [IPR009132](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR009132/) | Trace amine associated receptor family                                             |
|   A   | [IPR009150](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR009150/) | Neuropeptide B/W receptor family                                                   |
|   A   | [IPR013312](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR013312/) | G protein-coupled receptor 40-related receptor                                     |
|   A   | [IPR022347](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR022347/) | G protein-coupled receptor 153/162                                                 |
|   A   | [IPR026234](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR026234/) | Mas-related G protein-coupled receptor family                                      |
|   A   | [IPR027677](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR027677/) | P2Y purinoceptor 11                                                                |
|   A   | [IPR028335](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR028335/) | G protein-coupled receptor 18 orphan                                               |
|   A   | [IPR028336](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR028336/) | Glucose-dependent insulinotropic receptor                                          |
|   A   | [IPR037486](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR037486/) | G-protein-coupled receptor GPR139                                                  |
|   A   | [IPR039952](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR039952/) | G-protein coupled receptor Aex-2                                                   |
|   A   | [IPR042804](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR042804/) | Probable G-protein coupled receptor 82                                             |
|   A   | [IPR047143](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR047143/) | G-protein coupled estrogen receptor 1-like                                         |
|   A   | [IPR047160](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR047160/) | G-protein coupled receptor 183-like                                                |
|   A   | [IPR048077](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR048077/) | G-protein-coupled receptor 171                                                     |
|   A   | [IPR049579](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR049579/) | G protein-coupled receptors 26/78-like                                             |
|   A   | [IPR050119](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR050119/) | C-C chemokine receptor type 1-9-like                                               |
|   B   | [IPR001740](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001740/) | GPCR family 2, EMR1-like receptor                                                  |
|   B   | [IPR001749](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001749/) | GPCR, family 2, gastric inhibitory polypeptide receptor                            |
|   B   | [IPR002001](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002001/) | GPCR, family 2, diuretic hormone receptor                                          |
|   B   | [IPR002144](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002144/) | GPCR, family 2, secretin receptor                                                  |
|   B   | [IPR002170](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002170/) | GPCR, family 2, parathyroid hormone receptor                                       |
|   B   | [IPR002285](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR002285/) | GPCR, family 2, pituitary adenylate cyclase activating polypeptide type 1 receptor |
|   B   | [IPR003051](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003051/) | GPCR, family 2, corticotropin releasing factor receptor                            |
|   B   | [IPR003056](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003056/) | GPCR, family 2, ADGRE2/ADGRE5                                                      |
|   B   | [IPR003287](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003287/) | GPCR, family 2, calcitonin receptor family                                         |
|   B   | [IPR003290](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003290/) | GPCR, family 2, glucagon-like peptide-1/glucagon receptor                          |
|   B   | [IPR003910](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003910/) | GPCR, family 2, orphan receptor, GPR1/GPR3/GPR5                                    |
|   B   | [IPR003924](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR003924/) | GPCR, family 2, latrophilin                                                        |
|   B   | [IPR008077](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008077/) | GPCR, family 2, brain-specific angiogenesis inhibitor                              |
|   B   | [IPR008078](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR008078/) | GPCR family 2, Ig-hepta-like receptor                                              |
|   C   | [IPR000162](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000162/) | GPCR, family 3, metabotropic glutamate receptor                                    |
|   C   | [IPR004073](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR004073/) | GPCR, family 3, vomeronasal receptor, type 2                                       |
|   D   | [IPR000366](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000366/) | GPCR fungal pheromone mating factor, STE2                                          |
|   D   | [IPR000481](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR000481/) | GPCR fungal pheromone B alpha receptor                                             |
|   D   | [IPR001546](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR001546/) | GPCR fungal pheromone A receptor                                                   |
|   E   | [IPR022340](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR022340/) | G protein-coupled receptor GCR1 putative                                           |
|   F   | [IPR026543](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR026543/) | Frizzled-6, 7TM                                                                    |
|   F   | [IPR026551](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR026551/) | Frizzled-4, 7TM                                                                    |
|   F   | [IPR035683](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR035683/) | Smoothened, 7TM                                                                    |
|   F   | [IPR047105](https://www.ebi.ac.uk/interpro/entry/InterPro/IPR047105/) | Frizzled-4/Mom-5, 7TM                                                              |


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
