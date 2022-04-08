---
layout: post
title:  "draft_github pagesにjekyllを使用する (windows10)"
date:   2022-03-29 19:42:28 +0900
categories: jekyll update
---
# 環境
Windows10Pro  
ruby: 3.1.1p18  
jekyll:   


jeykllのインストール
https://jekyllrb-ja.github.io/docs/installation/windows/

Rubyインストーラーを使用してインストールする。
DEVKITを含めたものを指定。

https://rubyinstaller.org/downloads/
WITH DEVKITから、最新 (Ruby+Devkit 3.1.1-1)
インストールはデフォルトで構いません。
add ruby executables to you path.                          → 環境変数にrubyのパスを追加する。
Associate ,rb and, rbw files with this ruby installation.  → 拡張子rb,rbwをrubyのインストールに関連付けする。

コンポーネントはMSYS2は有効にします。ドキュメントは任意です。いれておいてよいと思います。

MSYS2を起動するため、そのままFinishします。
Run ‘ridk install’ to install MSYS2 and development toolchain.
セットアップには外部への通信を行います。
プロキシが必要な環境の場合は、チェックつけずにfinishして、cmd.extにてコマンドプロンプトを起動してください。

起動後、プロキシを設定します。
> set HTTP_PROXY=(プロキシサーバ):(ポート)
> set HTTPS_PROXY=(プロキシサーバ):(ポート)
設定後、インストーラーを起動します。
> ridk install

   1 - MSYS2 base installation
   2 - MSYS2 system update (optional)
   3 - MSYS2 and MINGW development toolchain

Which components shall be installed? If unsure press ENTER [1,3]

1,2,3を入力してEnterを押下します。


> pacman -Rdd catgets libcatgets --noconfirm
エラー: 対象が見つかりませんでした: catgets
エラー: 対象が見つかりませんでした: libcatgets
Rddオプションは他のパッケージから依存されているパッケージを、依存しているパッケージを削除しないで削除するものです。対象がないのは削除済であると同じなので、このエラーは問題ありません。

 何も行うことがありません
Install MSYS2 and MINGW development toolchain succeeded

>ruby -v
ruby 3.1.1p18 (2022-02-18 revision 53f5fc4236) [x64-mingw-ucrt]

>gem install bundler jekyll



https://github.com/login
にログインし、Create a new repositoryでpublicリポジトリを作成。

リポジトリ名は、以下の説明にのっとり、<ユーザ名 or 組織名>.github.ioのリポジトリをpublicで作成します。
https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites

Add a README file  .... README.mbを作成
Add .gitignore     ... 除外ルール設定
Choose a license   ... MIT License

Windowsの任意の場所にgit cloneします。(TortoiseGit)

cmd.exeでコマンドプロンプトを起動。
クローンしたリポジトリまで、移動します。

jekyll new . 
ディレクトリ内は空以外の場合はエラーが発生します。(ディレクトリ内に READMEやLISENCEファイルが存在)
その場合、同名ファイルの上書きが問題なければ--forceを付与します。
          Conflict: <PATH>/<REPOSITORY> exists and is not empty.
                    Ensure <PATH>/<REPOSITORY> is empty or else try again with `--force` to proceed and overwrite any files.
jekyll new . --force


動作確認用のサーバを起動します。
bundle exec jekyll serve
:in `require': cannot load such file -- webrick (LoadError)
webrickが存在しないようなので、gemfileに追加して、bundle installを実行します。
bundle add webrick
bundle exec jekyll serve

 Auto-regeneration: enabled for 'E:/200_Workspace/github/gorilakkuma.github.io'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

Server addressにアクセスします。
画面がでてこればOKです。終了する場合は、ctrl-cでstopしてください。

ディレクトリ内に_postsが存在します。
その中にmarkdownファイルが存在します。それをコピーペーストして、YYYY-MM-DD-(title).markdownにリネームします。
リネーム後、ブラウザーを再表示してください。
新規に作成したmarkdownファイルが表示されると思います。


ブログ全体の設定(titleやメールアドレス等)
_config.ymlを編集します。
非表示したいものは、コメントアウトします (先頭に#を付与)

http://jekyllrb-ja.github.io/docs/configuration/
http://jekyllrb-ja.github.io/docs/variables/

接頭辞としてsite. と付与されてます。
_config.ymlには接頭辞が記載ない状態で記載します。

各マークダウンには
{{ site.title }} と接頭辞を付与し{{ }} で囲むことで、その値を表示することが出来ます。




exclude:          表示したくないファイル
  - README.md
include:          表示したいファイル
  - Gemfile
  
# Exclude from processing.
# The following items will not be processed, by default.
# Any item listed under the `exclude:` key here will be automatically added to
# the internal "default list".
#
# Excluded items can be processed by explicitly listing the directories or
# their entries' file path in the `include:` list.
#
# exclude:
#   - .sass-cache/
#   - .jekyll-cache/
#   - gemfiles/
#   - Gemfile
#   - Gemfile.lock
#   - node_modules/
#   - vendor/bundle/
#   - vendor/cache/
#   - vendor/gems/
#   - vendor/ruby/
excludeにあるファイル、ディレクトリはデフォルトで設定されていますので、不要です。
これらのファイルにブラウザーからアクセスを許可する場合は、include:で指定します。



{{ site.title }}




https://ja.markdown.net.br/basic-syntax/#headings

公開前のmarkdownを管理する。
ルートフォルダに_draftsを作成します。

bundle exec jekyll serve --drafts
にて作成中のmarkdownを出力することが出来ます。




[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
