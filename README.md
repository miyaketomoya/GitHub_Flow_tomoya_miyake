# GitHubでチーム開発をするときのルールを書き出しただけのやつ
参考：GITHUB実践入門　[https://github.com/github-book]

## ワークフローの全体
1. mainブランチは常にデプロイできる状態とする(最終版のみを保存)
2. 新しい作業をするときは、mainブランチから記述的な名前のブランチを作成する
3. 作成したローカルリポジトリのブランチに変更をコミットする
4. 同名のブランチをGitHubのリポジトリに作成し、定期的に pushする
5. 助けて欲しい時やフィードバックが欲しい時は、Pull Requestを作成し、Pull Requestでやりとりする。
6. 他の開発者がレビューし、作業終了を確認したらmainブランチにマージする
7. mainブランチへマージしたら、直ちにデプロイする(まだあんま関係ない)

### 1. mainブランチは常にデプロイできる状態にする
mainブランチには絶対に不完全なコードを入れてはいけない

### 2. 新しい作業をするときは、mainブランチから記述的な名前のブランチを作成する
ブランチの作り方は、そのブランチの特性をそのまま正確に表したような名前<br>
例えば、ドキュメントをロードする機能を実装する時`load-document`など？

### 3. 作成したローカルリポジトリのブランチに変更をコミットする
commitはこまめに
⭐branchで作業してそこでcommitする分には最後pull requestを行うまでmainには影響がないため、どんどんcommitする。pull requestで統合するときにどんな変化が行われてきたかが見えるようにする

```
commit1: 近くのコードのインデントが崩れていたので適切に修正
commit2: 変数の単語の間違いを見つけたので正しい単語に修正
commit3: 今回の作業として追加するべきメソッドを追加
```
これぐらいの粒度でいいらしい

### 4. 同名のブランチをGitHubのリポジトリに作成し、定期的に pushする
```
git push origin branch名
```
これでローカルに作っていたブランチをGitHub上にupできる
⭐️mainにpushさえしなければbranchで作業する分には自分だけのものなので気軽にやっていい。開発途中でもpushすることで他の人がコードを見ることができる

### 5. 助けて欲しい時やフィードバックが欲しい時は、Pull Requestを作成し、Pull Requestでやりとりする
マージしなくてもpull requestを作成してそのページで議論を行うことが可能<br>
pull requestは開発者が承認しなければされない。

### 6. 他の開発者がレビューし、作業終了を確認したらmainブランチにマージする
pull requestを送ったら、基本的にそのコードは第３者に見てもらってレビューを受ける<br>
何か問題があったり、アドバイスがある場合はそのpull requestのページにコメントする(5.の話)<br>
`LGTM(looks good to me)`ってコメントすると、mergeして問題ないです！という文化があるらしい


# 作業をする時の通常の流れ
(デプロイとかはなく、一旦本のdevelopブランチがmainとする) <br>

コマンドで出てくる`origin`はリポジトリのリンクの別名 
```
git push origin feature/add-A -> originというリポジトリにローカルのfeature/add-A ブランチをpushする（登録する）ということ
```
### 何か新しい機能を実装したい時
⭐まずmainがGitHubのリポジトリと同じ最新版になっているかを確認(ないと思ってもとりあえずやって損なし)
```
git checkout main   #mainのbranchに移動
git pull origin main #リポジトリからpull(git remoteで対象のリポジトリにつながっているかを確認)
```
mainが最新版になっているか確認が取れたら `feature/(作りたい機能の説明)`のブランチを作って移動　例えばadd-Aという機能を追加したかったら
```
git checkout -b feature/add-A　# feature/add-Aというbranchを作って移動するコマンド
```
**作業を行う**<br>
- この時、こまめにcommitを行う(mainにcommitしなければ絶対影響ない)
```
git add 追加したいファイル
git commit -m "add-Aを実装するための部品Bを実装"
```

**機能が完成したら**<br>
pushしてpull requestを送る
```
git push origin feature/add-A # リポジトリにfeature/add-Aを登録
```
githubの該当ページに行って更新すると「create pull request」あるはずなのでそれをポチ<br>
作ったページに詳しい内容を書く<br>
他の人にコードをレビューしてもらったり議論して許可が出たらmergeしてもらう<br>
⭐この作業が完了したらそのbranchは終了!! 基本的には使わない

**ローカルの状態を最新にして次の作業を待つ**<br>
現在、`main`と`feature/add-A`のbranchが存在する

ローカル feature/add-A != main
- feature/add-A -> ここで作業していたので最新の状態
- main -> feature/add-Aで作業を行っていたため、feature/add-Aの更新はされてない状態

リモート(GitHubのリポジトリ)　feature/add-A = main
- feature/add-A -> git push origin feature/add-Aしてローカルの状態が反映されているので最新の状態
- main -> feature/add-Aのpull requestを承認しているので最新の状態

現在、ローカルのmainだけ最新ではない状態<br>
これを最新にするためにmainに戻って最新の状態を更新
```
git checkout main # mainのbranchに移動
git pull origin main # mainにorigin(何もいじらなければGitHubのリポジトリのmainへのリンクを指しているはず)の情報を持ってくる
```
これでローカルのmainが最新で保たれている。ここから何か作業があれば、またfeature/add-Bなど新しいbranchを作る

**作業中に他の人によってGithubのmainが更新された時**<br>
このような状態になっているはずであり、この時、作業しているブランチを最新にする必要がある<br>
ローカル
- main -> feature/add-Aを作った時の状態
- feature/add-A -> いくつかコードをcommit(push)している状態

リモート(Githubのリポジトリ)
- main -> 他の人が更新した最新の状態
- feature/add-A -> (pushしたことあったら存在)最後にpushした時の状態

手順
1. mainにcheckoutして`git pull origin main` (githubのmainを引っ張ってくる. これで最新)
2. 作業ブランチに移動 `git checkout feature/add-A`
3. mainの状態を feature/add-Aに引っ張ってくる(mearge) 'git mearge main'

⭐️基本的に同じコードをいじってるとかでなければmeargeしたら、今までの作業に影響なく更新を持ってくることができるはずなので、ビビらない
⭐️同じコードをいじっていた時 conflictが発生 -> ガイドをもとに修正(また調べます)

この操作でmainは最新、feature/add-Aは最新の状態から変更を加えているみたいになっている<br>
ローカル
- main -> githubのリポジトリの最新状態(feature/add-Aで新しく作っているコードは反映されていない)
- feature/add-A -> 最新情報更新した上で、今まで作ってきたコードがある状態

リモート(Githubのリポジトリ)
- main -> 他の人が更新した最新の状態
- feature/add-A -> meargeした後の状態をpushしてたら、最新情報とそこまでのfeature/add-Aのコードがある状態





 




