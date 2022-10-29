---
title: "GitHub 連携から始める Zenn 入門"
emoji: "😸"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["GitHub", "Zenn"]
published: true
---

# はじめに

Zenn で投稿を始める前に、GitHub[^1] を利用してコンテンツを管理するよう **変更する** 手順については、次のような記事が公式に用意されているので、そちらを見れば分かりますし、

[^1]: [https://github.co.jp/](https://github.co.jp/)

https://zenn.dev/zenn/articles/connect-to-github

ローカルでの **記事の作成方法** などについても、次の記事の通りに進めていけば、基本的に問題ないかとは思うのですが、

https://zenn.dev/zenn/articles/install-zenn-cli

記事を作成する練習も兼ねて、自分なりに、改めて簡潔にまとめ直してみました。

表現の違いなどにより、人によっては分かりやすいと思ってもらえるかもしれませんし、何かしら、誰かの助けにでもなれば幸いです。

前提条件として、GitHub アカウントと、Zenn にログインするための Google アカウントは、すでに作成してあるものとし、

ちなみに、本記事における動作確認環境のベースは「 macOS Big Sur 」なので、その点についても、念のため、ご留意いただければと思います。

# GitHub と連携する手順

1. まず、GitHub にログインして、連携用に、例えば「 zenn-connects 」というような、空のリポジトリを作成しておきましょう。

2. 次に、Zenn にログインし、[Deploys](https://zenn.dev/dashboard/deploys) ページにアクセスして、そこにある「 リポジトリを連携する 」ボタンを押します。

![GitHubリポジトリからデプロイ1](https://storage.googleapis.com/zenn-user-upload/b29874a3492905f436dc4b1b.png)

3. GitHub の認証画面に進んだら「 Only select repositories 」を選択した上で、最初に作成しておいたリポジトリを選ぶと、次の画像のような状態になるはずなので、先へ進みます。

![Build software better, together](https://storage.googleapis.com/zenn-user-upload/95adc0a410d8959529f72dd5.png)

4. すると、先ほどの [Deploys](https://zenn.dev/dashboard/deploys) ページが、次の画像のように変わり、

![GitHubリポジトリからデプロイ2](https://storage.googleapis.com/zenn-user-upload/ae4a941d31e0b337fb3800ee.png)

例えば、デフォルトでは「 main 」ブランチに、ファイルを push すれば、投稿ができるようになっているはずです。

逆に、Zenn の Web ページからは、もう投稿ができなくなっているので、注意してください。

![記事の管理](https://storage.googleapis.com/zenn-user-upload/a688ef1ec00400aeae309389.png)

ただし、見ての通り、画像のアップロードはココからできて、記事に埋め込めるリンクが簡単に取得できるので、覚えておきましょう。

# ローカルで記事を作成する準備

GitHub と連携できたのは良いけれど、目の前にあるのは、空のリポジトリだけ。これでは、どうして良いか分かりませんよね。

そこで、是非とも導入すべきなのが「 Zenn CLI 」というツールで、次の公式の記事を読めば、大体、分かるかとは思うのですが、

https://zenn.dev/zenn/articles/install-zenn-cli

一応、ローカルでのセットアップから、基本的なコマンドの実行まで、自分で試してみた様子を紹介しておきます。

1. まず、インストールについては、ターミナルを起動し、以下のようにして実行しました。

```
% npm -v
7.19.1
% npm init --yes
Wrote to /Users/normalsalt/Documents/zenn-connects/package.json:

{
  "name": "zenn-connects",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/normalsalt/zenn-connects.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/normalsalt/zenn-connects/issues"
  },
  "homepage": "https://github.com/normalsalt/zenn-connects#readme"
}
% npm install zenn-cli

added 203 packages, and audited 204 packages in 12s

8 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm notice 
npm notice New minor version of npm available! 7.19.1 -> 7.20.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v7.20.0
npm notice Run npm install -g npm@7.20.0 to update!
npm notice
```

:::message
もし、`command not found: npm` と言われてしまったら、例えば、Mac なら `% brew install node` と実行するなどして、先に Node.js[^2] 環境を整えておく必要があります。
:::

[^2]: [https://nodejs.org/ja/](https://nodejs.org/ja/)

2. これで、次のようなコマンドを実行するだけで、記事を配置するために必要な `articles` ディレクトリなどが自動的に生成され、

```
% npx zenn init

  🎉  Done!
  早速コンテンツを作成しましょう

  👇  新しい記事を作成する
  $ zenn new:article

  👇  新しい本を作成する
  $ zenn new:book

  👇  投稿をプレビューする
  $ zenn preview
  
% ls
README.md          articles/          books/             node_modules/      package-lock.json  package.json
```

3. 以降は、簡単なコマンドから記事の作成が始められるので、慣れれば非常に便利そうです。

```
% npx zenn new:article --slug github-zenn-introduction
created: articles/github-zenn-introduction.md
```

マークダウン記法については、次のページに目を通しておきましょう。

https://zenn.dev/zenn/articles/markdown-guide

4. そして、ローカルで記事を作成していく上で気になるのが、プレビューの仕方ですが、

次のようなコマンドを実行すれば「 Zenn Editor 」という専用のページが、http://localhost:8000 のような URL で、ブラウザから見られるようになります。

```
% npx zenn preview
👀 Preview: http://localhost:8000
```

![GitHub 連携から始める Zenn 入門のプレビュー](https://storage.googleapis.com/zenn-user-upload/51a4f1c68f08b78443d55c4e.png)

ご確認いただけたでしょうか？

:::message
ちなみに、`% npx zenn preview --port 8888` というように、オプションを付けて起動することにより、ポート番号を変えることもできます。
:::

それでは、記事を作成して、どんどんリポジトリに push していきましょう！ その際、ブランチ名には注意してくださいね。

```
% git branch -M main
% git push -u origin main
```

:::message
[Deploys](https://zenn.dev/dashboard/deploys) ページから、デプロイ対象ブランチを変更することもできます。
:::

最後に、本記事を含むリポジトリへのリンクも張っておきますので、ご参考までに。

https://github.com/normalsalt/zenn-connects

# おわりに

Git でコンテンツを管理していく、主な利点としては、バージョン管理ができるのはもちろん、一応、プルリクエストを受け付けたりもできるようになるわけですが、

そうでなくとも、最低限、バックアップとして、とても **安心感** がありますよね。

今の時代、デジタルの世界では何があるか分かりませんし、サービス本体のサーバーにだけでなく、ローカルにも GitHub にも、バックアップを確保しておくということは、

物書きの中でも、特に意識の高い人にとっては、もはや基本になりつつあるかもしれません。

そこに **資産を貯めていく** というような意欲にも、つながってくるのではないでしょうか？

また、一度書き上げたら終わりというものでもなく、特にテック系の記事については、日夜アップデートを重ねていくことも大切で、

そうなってくると、やはり、バージョン管理は、ほとんど必須です。

技術の進歩も、ゆくゆくは、より良質な記事だけが生き残っていくという **自然淘汰** をネット上で実現してくれると信じて、お互い、精進してまいりましょう！
