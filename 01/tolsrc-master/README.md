# tolsrc
[![CircleCI](https://circleci.com/gh/HariboteOS/tolsrc.svg?style=svg)](https://circleci.com/gh/HariboteOS/tolsrc)

Source set of tools for developing Haribote OS .

## How to compile

### 注意点

- gccでコンパイルしないとうまく動きません。
 - つまりMacOSXでコンパイルする際は、標準のclangではなく、適切なgccを指定する必要があります。
 - 以下はHomebrewでgcc6.2.0を導入している場合の例です。
 - `make GCC=/usr/local/Cellar/gcc/6.2.0/bin/gcc-6`

### 手順

- リポジトリ直下で
 - `make`するとバイナリが生成されます。
 - `make install`すると、そのバイナリを`ok`ディレクトリ以下に配置します。
  - これを`z_tools`に改名して適切な場所に配置してください。

## ベースとなったソースコード
- このブランチは、Akkie氏によって移植された2007-02-21版のソースをベースに、最新のMac向けの修正を加えています。
- ベースとなったソースコードのパッケージは、以下のサイトから取得できます。
 - http://shrimp.marokun.net/osakkie/wiki/tolsetOSX/

## Changes
### haritol
- 標準ライブラリのみ使用
- マルチプラットフォームでの開発に対応するため、追加されました。
- OSごとに引数の形式が異なるコマンド(del/rm copy/cat)の肩代わりをします

### fdimg2iso
- 標準ライブラリのみ使用
- fdのダンプイメージを、ブータブルなisoイメージに変換します。
 - ブータブルCDの作成が簡単に行えます。

## Known issues

### `sys/cdefs.h: No such file or directory`とのエラーが出る
- Ubuntuの場合は、以下のコマンドを実行して、必要なパッケージをインストールしてください。(Thanks @sk2sat!)
 - `apt-get install libc6-dev-i386`

### Xcode 10 以降でコンパイルできない

macOS でコンパイルする場合 Xcode 10 以降は `i386` アーキテクチャは [サポートされなくなる](https://developer.apple.com/documentation/xcode_release_notes/xcode_10_release_notes#3035631) ためコンパイルができなくなります。

以下の手順で Xcode 9.4 以前をダウンロードし、内部にある `MacOSX.sdk` を利用してコンパイルしてください。

- [https://developer.apple.com/download/more/](https://developer.apple.com/download/more/) から `Xcode_9.4.1.xip` をダウンロードして解凍
- `gcc` の `--sysroot` にダウンロードした SDK を設定してコンパイルする
  - (解凍した `Xcode.app` を `/Applications/Xcode_9.4.1.app` に移動させた場合)
  ```bash
  make GCC="/usr/local/Cellar/gcc/6.2.0/bin/gcc-6 --sysroot=/Applications/Xcode_9.4.1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.13.sdk/"
  ```
