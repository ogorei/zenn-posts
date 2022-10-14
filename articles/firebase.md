---
title: "Firebase v9でチャット作ってみました！"
emoji: "🤓"
type: "Tech"
topics: ['チャット機能','firebase','リアクト']
published: False
---
### 1 プロジェクト作成する


```
npx create-react-app chat-room && cd chat-room

```
### Firebaseライブラリーを導入する

ホームディレクトリーにいることを確認して下記のレポをクローンします。

```
npm i firebase react-router-dom

```
firebase.tsというファイルを作成します.
このファイルの中にFirebaseの設定を書いていきます。

````
mkdir src/services && touch src/services/firebase.js
```