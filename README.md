# Codespace LaTeX for Japanese
- [Codespace LaTeX for Japanese](#codespace-latex-for-japanese)
  - [概要](#概要)
  - [なぜCodespacesを使うのか](#なぜcodespacesを使うのか)
  - [Codespaces経由の使い方](#codespaces経由の使い方)
    - [Troubleshooting](#troubleshooting)
  - [MS明朝，MSゴシックを使用したい場合](#ms明朝msゴシックを使用したい場合)
    - [1. フォントファイルの準備](#1-フォントファイルの準備)
    - [2. フォントのインストール](#2-フォントのインストール)
    - [3. フォントの使用](#3-フォントの使用)
  - [TODO](#todo)
  - [Credits](#credits)


## 概要
- これは日本語で文章を作成するためのCodaspace/devcontainer用LaTeXです。This is a LaTeX template for Codaspace that generates Japanese PDFs.

- [sanjib-sen](https://github.com/sanjib-sen)さんの[WebLaTeX](https://github.com/sanjib-sen/WebLaTex)より派生しています。Forked from [sanjib-sen/WebLaTeX](https://github.com/sanjib-sen/WebLaTex).

- 日本語のPDFを作成できるように，`latexmkrc`の設定や，[LaTeX-Workshop](https://github.com/James-Yu/LaTeX-Workshop)の設定をいれています。

## なぜCodespacesを使うのか
Codespaces は GitHub が提供するクラウド開発環境です。GitHub にリポジトリを作成するだけで、そのリポジトリを開発するための環境をすぐに利用できます。この環境は、GitHub が提供するクラウド上のコンピューターで、コードを編集したり、コンパイルしたり、デバッグしたりすることができます。Overleaf，CloudLaTeXのようなオンラインLaTeX環境を使うのと比べて，Codespacesを使うメリットは下記の通りです。
- 無料（時間制限あり）
- バージョン管理ができる
- 自由に環境をカスタマイズできる

## Codespaces経由の使い方
1. リポジトリの右上の`Use this template`で，
   
   `Create a new repository`または`Open in a codespace`を選択します。
2. 任意のリポジトリ名を入力し，**Create Fork / Create repository from template**をクリックします。
3. **<> Code** > **CodeSpaces** > **Create Codespace on Main**を選択し，インストールは始めます。
   
   初回起動は時間がかかりますが，2回目以降は早くなります。
4. latexindentを導入されています。texファイルをセーブする時点で自動でインデントが整えられます。好みの設定を入れたい場合は，`./latexindent.yaml`を編集してください。
5. デフォルトのビルドで`.latexmkrc`は自動的に読み込まれていますので，設定を変更したい場合は直接に`./.latexmkrc`を編集してください。PDFファイルは`./OUT`のディレクトリに出力されます。
   ### Troubleshooting
   - デフォルトのビルドが上手くいかない場合，下記のようにレシピの`Build with .latexmkrc`をクリックしてビルドしてください。
   　 ![latexmkrc](/images/latex.gif)
   -  ローカルのVisual Studio CodeでCodespaceを使うとき, ローカルのLaTeX Workshopとの設定が衝突してしまうことでレシピが実行されないことがあります。その場合は，VS Codeの`settings.json`に設定が衝突しないように設定してください。
6. texファイルの先頭にマジックコメントを入れることはできますが，デフォルトのレシピを無視して優先的に実行されるので，やっていることがわからない方にはおすすめしません。参照:[マジックコメント](https://texwiki.texjp.org/?Visual%20Studio%20Code%2FLaTeX#b7b858ba)。

## MS明朝，MSゴシックを使用したい場合
### 1. フォントファイルの準備
- フォントのttcファイルを`./map`に配置してください。

- マイクロソフトのフォントはライセンスの関係で，このリポジトリには含まれていません。
  - Windowsユーザーは，`C:\Windows\Fonts`からコピーしてください。
  - WordとかOffice系のアプリをお持ちのMACユーザーは，bashコマンドで
      ```bash
      $ open /Applications/Microsoft\ Word.app/Contents/Resources/Fonts
      ```
      Wordのフォントフォルダを開き，ttcファイルをコピーしてください。

### 2. フォントのインストール
ここからはCodespaceのターミナルを使用します。
- デフォルトディレクトリ`/workspaces/{レポジトリ名}#`になっていることを確認してください。
    
    - なっていない場合は，
       ```bash
       $ cd /workspaces/{レポジトリ名}
       ```
       で移動してください。
- 下記のコマンドで`./msfont.sh`を実行してください。
    ```bash
    $ sh msfont.sh
    ```
    これでdvipdfmxのデフォルトフォントはMS系フォントになります。
- 確認のために
    ```bash
    $ kanji-config-updmap-sys status
    ```
    で`CURRENT family for ja: ms`になっているか確認してください。


  ### 3. フォントの使用
  - ここまでできたら，デフォルトフォントはMS系フォントになります。
  - 他のフォント(例えばIPAex)を指定したい場合はmainとなるtexファイルにおいて適宜に
     ```LaTeX
     \usepackage[ipaex]{pxchfon}
     ```
      を追加してください。または，ターミナルで
      ```bash
      $ kanji-config-updmap-sys ipaex
      ```
      でデフォルトフォントを変更してください。

## TODO
- [ ] WSL2のdockerを用いてdevcontainerを立ち上がる方法を書くこと
## Credits
- [sanjib-sen](https://github.com/sanjib-sen)'s [WebLaTex](https://github.com/sanjib-sen/WebLaTex)
- @James-Yu's [LaTeX-Workshop](https://github.com/James-Yu/LaTeX-Workshop) 
- [texlive/texlive:latest](https://gitlab.com/islandoftex/images/texlive)
- 優曇華院's [MS明朝でLaTeXする話](https://omedstu.jimdofree.com/2019/05/29/ms%E6%98%8E%E6%9C%9D%E3%81%A7latex%E3%81%99%E3%82%8B%E8%A9%B1-mac%E7%B7%A8/)