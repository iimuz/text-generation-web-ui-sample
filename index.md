---
title: oobabooga/text-generation-webuiの利用スクリプト
date: 2023-10-28
lastmod: 2023-11-04
---

## 概要

[oobabooga/text-generation-webui](https://github.com/oobabooga/text-generation-webui)を利用するためのスクリプトや実行方法に関するメモとなります。

anaconda ではなく pip で環境構築を試していますが、正常にモデルが動作するところまで試せていません。

## フォルダ構成

このフォルダに text-generation-webui を git clone して環境構築することを想定してスクリプトを記載します。

- til-20231028
  - .gitignore
  - index.md
  - text-generation-webui/: クローンしたリポジトリのフォルダ。ただし、.gitignore で設定されているため何もコミットされない。

## 実行方法

WebUI を起動するためには、環境構築が完了して以降は下記のように実行するとサーバーが立ち上がる。

```sh
cd ./text-generation-webui
.venv/scripts/activate
python server.py
```

## 環境構築方法

(Windows 環境の場合)

start_windows.bat を利用すると conda が必要となる。
conda を利用しないで環境構築を行う場合は下記のようになる。

```sh
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
cd ./text-generation-webui
git switch -c v1.7 tags/v1.7
python -m venv .venv
.venv/scripts/activate
pip install -r requirements.txt --extra-index-url https://download.pytorch.org/whl/cu118
python server.py
```

ただ、上記でインストールには成功したが、[cyberagent/open-calm-7b](https://huggingface.co/cyberagent/open-calm-7b)が動作しなかった。

```sh
Tokenizer class GPTNeoXTokenizer does not exist or is not currently imported.
```

## Tips

### Windows 環境における scoop を利用したバージョン設定

scoop を利用してバージョン管理する場合は下記のようにして利用するバージョンを設定する。

```sh
scoop reset python310
scoop reset cuda11.6
```

### モデルファイルのダウンロード

Hugging Face からダウンロードする場合は、WebUI の Model のところに、"Download model or LoRA"とある部分にブランチ名を入力することでダウンロードできる。
ダウンロードしたファイルは、`models`の配下にダウンロードされる。
例えば、`cyberagent/open-calm-7b`でダウンロードできる。
