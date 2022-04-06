---
title: "AppCenterを使ってREACT NATIVEアプリをリリースしてみた話"
emoji: "🔰"
type: "tech"
topics: ['ios','reactnative','appcenter','app']
published: false
---

AppCenter.msを使って良かったこと：

時間短縮
自動アップデート
dependenciesを自動でインストールしてくれる
MacOS使っていなくても、iOSのアプリをリリースできる

###設定

1. appcenterのアカウントを作成する。
（Githubでログインすることをおすすめ）
2. Add new appをクリックしてアップロードしたいアプリを登録する。
（ReactNativeでもiOS/Androidを別々で登録する必要ある）
picture here 
3. メニューからbuildタブに入って、githubにあがっているアプリのレポを選択します。
　　branchを間違えないよう注意！
　　build on pushを選択するとレポ更新される際に自動アップデートできます。

手動アップデートまたテスト実装の場合下までスクロールしてください。
run unit tests と　sign buildsを選択します。

1. ターミナルを開いてiosフォルダーを開きます。
```
open ios/xxxx.xcodeproj
```
