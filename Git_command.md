## git command一覧

- pushするブランチ名をローカルのブランチ名でないものにする.local branch名をlocal1としてremote1という名前でbranchにpushしたい
  `git push origin local1:remote1`
  
- git fetchはリモートのサーバーから情報を取得するのみ
- `git fetch`+ `git merge` = `git pull`

サーバーのブランチを削除したい場合
`git push origin --delete [ブランチ名]`

### git mergeとgit rebaseの違い
rebase参考サイト[https://qiita.com/hkuno/items/ef639b75efc156cf37d7]<br>
以下の状態があるとする
<img width="813" alt="スクリーンショット 2024-08-22 20 58 49" src="https://github.com/user-attachments/assets/3778db4b-13ab-4416-a39e-ca5b8803aedb">
**`git checkout master -> git merge master/experiment`を実行したとき**<br>
masterからexperimentを結合したものがcommitされてmasterが進む
<img width="814" alt="スクリーンショット 2024-08-22 21 00 52" src="https://github.com/user-attachments/assets/ad36bbae-707d-410a-8d4f-b68d7d84b4d1">

**`git checkout experiment -> git rebase master`を実行したとき**<br>
1. experimentのブランチとmasterのブランチの共通の先祖に移動 (今回はC2)
2. rebase先のところ(masert)まで移動してそこからexperimentの差分を適用
3. 一直線の履歴が出来上がる
<img width="811" alt="スクリーンショット 2024-08-22 21 08 52" src="https://github.com/user-attachments/assets/c4192e82-76b3-49aa-9de0-fdfc24d39b71">
-> `git checkout master -> git merge experiment`でfast-forwardマージが可能

### git rebase上級編
**`git rebase --onto [接続先] [切り取りの基準にしたい点] [切り取り終了点]`**<br>
意味：[切り取り終了点]に移動して[切り取りの基準にしたい点]と[切り取り終了点]の共通の祖先からのパッチを取得して、[接続先]上でそれを適用しろ
こんな状態になっているとする !serverの作業はまだしたい.. clientのみをmasterにrebaseしたい...
<img width="806" alt="スクリーンショット 2024-08-22 21 20 07" src="https://github.com/user-attachments/assets/1c858107-32ca-4a49-a8f9-4acc474c9ea6">
1. [切り取り終了点]に移動する(HEADが指す先はC9になる)
2. [切り取りの基準にしたい点]と[切り取り終了点]が分岐する前の共通状態を特定し、そこから[切り取り終了点]までの差分を取得する (今回はC3が先祖なのでそこから[切り取り終了点]までの差分C8,C9が退避される)
3. HEADを[接続先]へ移動する`git reset --hard [接続先]`
4. そこから退避した差分を順にcommitしていく(今回だとC8,C9がcommitされる　※masterもC5で分岐しており完全同じではないためC8'C9')
これで以下のように１本の履歴になった
<img width="790" alt="スクリーンショット 2024-08-22 21 48 57" src="https://github.com/user-attachments/assets/4d380c79-5bdb-404c-bc01-8ef2dc9d5850">
ここで`master`より`client`が先に行っている事に注意. fast-forwardすること(ポインタを先端に移動するmerge方法)を忘れずに<br>
`git checkout master` -> `git merge client`でマージ

残りのserverがmergeできるようになったら<br>
`git rebase master server` -> `git checkout master` -> `git merge server`で完全な１直線
(`git rebase master server`は`git rebase --onto master master server`の略)
