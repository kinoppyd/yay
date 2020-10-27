# Yay!

このテキストは、Web開発の経験があるけれど、RubyとRailsにはまだ慣れていない方々に向けて作成されたものです。
SmartHRでは、現在多くのプロダクトのバックエンドがRailsによって書かれています。すなわち、RailsのスキルはSmartHRのエンジニアに必須です！
しかし、Railsを深く理解するのはとても難しいです。なぜなら、Railsを理解するためにはまずRubyを理解する必要があるからです。
どの言語、どのWAFでも同じですが、そのWAFを使いこなすためには言語の特性を知り、WAFの動きを頭の中で納得することが重要です。

前半パートでは、まずRailsを理解するためのRuby講座があります。そして後半パートでは、[現場Rails](https://book.mynavi.jp/ec/products/detail/id=93905)を題材にしてRailsを理解していきます。
このテキストを終える頃には、あなたはSmartHRのRails戦士です！
Yay!

## 開発環境について

- Ruby 2.7 以上（2.6などでも動くはずですが、特別な理由がない限り最新のバージョンを利用しましょう）
  - Bundlerは2系のものを準備してください（Ruby 2.7であれば標準でBundler 2系がインストールされています）
- Rails 6.0 以上

## Rubyのインストール方法

新しいRubyが一番良いRubyなのでrbenvを使って新しいRubyを用意しておきましょう

### Rubyインストール準備

`rbenv`をインストールします

- https://github.com/rbenv/rbenv#installation
  - インストール方法に依らず、.bash_profileなどに設定を追加する必要があります（https://github.com/rbenv/rbenv#basic-github-checkout の `3.`の手順です）
  - `rbenv init`を実行すると、どのファイルに何を記載するか出力してくれるので、そこを参考にして`eval "$(rbenv init -)"`を記載しましょう
- brew以外の方法でrbenvをインストールした場合はruby-buildのインストールも行う必要があります
  - https://github.com/rbenv/ruby-build#installation
- ProTip
  - 手動でrbenvをインストールしている勢は`rbenv-update`も導入しておくと、`rbenv update`でインストールリストの更新ができて便利だよ
  - https://github.com/rkh/rbenv-update

### Rubyのインストール

インストールできるバージョンを確認しましょう。

```sh
% rbenv install -l
2.5.8
2.6.6
2.7.1
jruby-9.2.12.0
maglev-1.0.0
mruby-2.1.1
rbx-5.0
truffleruby-20.1.0

Only latest stable releases for each Ruby implementation are shown.
Use 'rbenv install --list-all' to show all local versions.
```

rbenvでは、いわゆる普段使う`Ruby`（区別するためにCRubyやMRIなどと呼ばれることもあるよ）以外にJRubyやmrubyなどもインストールできます。
ここでは普通のRubyを使うため、プリフィックスに何も記載されていないものが対象のRubyです。

今回は最新バージョンである2.7.1を利用します。

```sh
% rbenv install 2.7.1
```

ビルドが走るのでコーヒーでも入れてのんびり待ちます。
終わったらインストールしたRubyをデフォルトで使用するRubyに指定します。
（この瞬間だけ任意のバージョンを利用したい！というときは`global`の代わりに`shell`を使うと良いです）

```sh
% rbenv global 2.7.1
```

rbenv versionsを使うと現在のRubyのインストール・使用状況を確認できます。今回は2.7.1を指定したので、2.7.1に`*`がついていれば大成功です。
（作業ディレクトリに`.ruby-version`などがあるとそちらを優先するため、思った通りのバージョンにならない場合はそちらも確認しましょう）

```sh
% rbenv versions
  system
  2.5.7
  2.6.6
* 2.7.1 (set by /Users/***/.rbenv/version)
```

最後に、rubyコマンドでも正しいバージョンが利用されているか確認しましょう。

```sh
% ruby -v
ruby 2.7.1p83 (2020-03-31 revision a0c7c23c9c) [x86_64-darwin19]
```

## Railsのインストール方法

Railsを利用するためには、Railsだけでなくnodeなども必要になるためそれらのインストールも必要です。

### node/yarnのインストール

インストールしていない人向けです。

https://github.com/nodenv/nodenv#homebrew-on-macos

```sh
% brew install nodenv
```

nodenvがインストールできたら~/.zshrcなどに設定を追記します。

```
eval "$(nodenv init -)"
export PATH=$HOME/.nodenv/bin:$PATH
```

その後、ターミナルの再起動などを行い、以下のコマンドでnodeをインストールします。nodeに関してはバージョンの指定はありません。ここではRailsが利用する最低バージョンである10系を指定しますが、12系などでも差し支えはありません。

```sh
% nodenv install 10.21.0
% nodenv global 10.21.0
% node -v
v10.21.0
```

続いてyarnのインストールを行います。こちらもバージョンに関して厳密は指定はないので、普通にyarnが動く状態になっていれば良いです。

https://classic.yarnpkg.com/ja/docs/install#mac-stable

```
% brew install yarn --ignore-dependencies
```

### ImageMagickのインストール

ActiveStorageなどを利用する場合に必要です。
必要になるときにインストールするでも構いません。

```sh
% brew install imagemagick
```

### Railsのインストール

次のコマンドでrailsをインストールしておきます。

```sh
% gem i rails --no-doc
Fetching concurrent-ruby-1.1.6.gem
    :
Successfully installed rails-6.0.3.2
40 gems installed
%  rails -v
Rails 6.0.3.2
```

## 「現場で使える Ruby on Rails 5速習実践ガイド」向け環境構築

書籍URL : https://book.mynavi.jp/ec/products/detail/id=93905

微妙にバージョンが低いため、別途準備します

### Rubyのインストール

Ruby 2.5.1を利用しているので、2.5.1を準備します。
また、Ruby 2.5系ではBundlerが用意されていないため、Bundlerのインストールも行います。

```sh
% rbenv install 2.5.1
% rbenv shell 2.5.1
% gem install bundler -v "~> 1.0" --no-doc # bundler 1系をインストールする
```

### Railsのインストール

現場Railsで利用するRailsのバージョンに合わせてるため、以下のようにバージョンを指定してRailsをインストールします（`_version_`とすることで、任意のバージョンを切り替えることができます）。

```sh
% rbenv shell 2.5.1
% gem i rails -v 5.2.1 --no-doc
% rails _5.2.1_ -v
Rails 5.2.1
# rails newするときも `rails _5.2.1_ new sample` などとします
```

### データベースの準備

PostgreSQLが必要なのでインストールしておきます（起動などはしなくてOK）。PostgreSQL自体は次項のDockerを用いますが、gemライブラリのインストールで必要になるため、PostgreSQL自体をインストールだけ実施しておく必要があります。

```
% brew install postgresql
% postgres -V
postgres (PostgreSQL) 12.2
```

### Dockerの準備

以下を参考にDockerをインストールしてください
https://hub.docker.com/editions/community/docker-ce-desktop-mac/

最終的に以下のコマンドが利用可能になればOKです

- docker
- docker-compose


# LICENSE

このリポジトリは、[MITライセンス](https://opensource.org/licenses/MIT)で公開されています。
Yay! is published under the [MIT-License](https://opensource.org/licenses/MIT).
