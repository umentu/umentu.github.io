+++
aliases =["posts", "articles", "blog", "showcase", "docs"]
author = "umentu"
title = "Rustlingsを始める方法"
date = "2022-09-21"
description = "asdfからRust環境を構築してrustlingsを始める方法を紹介"
tags =["tech", "rust"]
+++

Rustの公式の学習ツールとして「[Rustlings](https://github.com/rust-lang/rustlings)」というものを一月前ほどに知り、非常に楽しくて
何週かしていた。ぜひプログラミング学習的な意図としても活用してみてほしいと考え、紹介する。

MacかWSLのUbuntu環境での方法を紹介する。


## 1. asdfをインストール

[asdf](https://asdf-vm.com/)とは、プログラミング言語やソフトウェアのバージョン管理をしてくれるソフトウェア。
asdfを入れれば(M1/2とかでない限り)おおよその環境を構築できる。
ただしasdfに限らずな点として、PythonにおけるSQLite3など、システム領域にインストールする必要がある場合は別途インストールが必要。

### Ubuntuでgccが入っていない場合はインストール

```bash
sudo apt install gcc
```

### zsh(Macの場合デフォルト)の場合

```sh
git clone https://github.com/asdf-vm/asdf.git ~/.asdf 
. $HOME/.asdf/asdf.sh >> $HOME/.zshrc
exec $SHELL -l
```

### bash(Ubuntuのデフォルト)の場合

```sh
git clone https://github.com/asdf-vm/asdf.git ~/.asdf 
. $HOME/.asdf/asdf.sh >> $HOME/.bash_profile
exec $SHELL -l
```

### 確認

```sh
asdf --version
# v0.10.2
```

## 2. Rust をインストール

```sh
asdf plugin add rust
asdf install rust latest
asdf global rust latest
```

### 確認

```sh
rustc --version

# rust 1.63.0
```

## rustlingsをインストール

### rustup をインストール

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### rustlings をインストール

```sh
curl -L https://raw.githubusercontent.com/rust-lang/rustlings/main/install.sh | bash
```

### rustlingsのexerciseをローカルにclone

**VS Codeでやることを想定**
```sh
cd $WORKSPACE # $WORKSPACEは任意のディレクトリ
git clone https://github.com/rust-lang/rustlings
cd rustlings
code .
```

## rustlingsの使い方

VS Codeのターミナルで実行

#### 起動
```sh
rustlings watch
```

起動するとエラーファイルとエラー箇所が表示されるので、それらを修正していく。
修正して保存したらエラーが解消されたかを自動でチェックしてくれる。
間違っていた場合は再度修正、完了したら

```sh
// I AM NOT DONE
```
を削除すると次のファイルのエラーが表示される。これをひたすら繰り返す。


#### ヒント

わからないときは
```sh
rustlings hint intro1
```

のように実行すると、ヒントが表示される。

ただしターミナルは`rustlings watch` が起動しているので、VS Codeの画面を分割して

Mac: `Cmd + Shift + p`
Ubuntu: `Ctrl + Shift + p`

でコマンドパレットを開き、`Create New Terminal in Editor Area`で新たなターミナルを開くと使いやすい。


{{< figure src="lets_rustlings01.png" alt="画像1" >}}


## 感想

世の中、こういうツールがでまわっているんだから、オンラインスクールなんて言う情報商材にお金をかけなくてもプログラミング言語は勉強できるのに。



