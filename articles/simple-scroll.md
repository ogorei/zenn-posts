---
title: "（VUE)ライブラリーを使わずスクロールアニメーション"
emoji: "🌟"
type: "tech"
topics: ['VUEJS','アニメーション','css']
published: false
---
初心者、ライブラリーを使いがちだと思いませんか？私もそうでした。
 ライブラリーは使いやすくとても便利ですが、バージョンアップした時に必要ない更新作業が発生して大変な目に合いました。
その経験から学んだのが１００％必要でない限りピュアーJSで書くのがBESTだということです！

今回はライブラリーを使わずにCSS Transitionプロパティと9行のJavascriptコードでこのようなスクロールアニメーションを実装します！



トランジションはあまり分からないので下記の記事おすすめです。
https://webst8.com/blog/css-transition/

### 最終的にこうなります！

![](https://https://ogorei.tumblr.com/post/679030342918799360/simple-scroll)


## VUE環境を整える

スタートファイルをクローンしましょう。
```
git clone git@github.com:ogorei/simple-scroll-starter.git

```
ダウンロードできたらエディターを開いて必要なパッケージをインストールします。
```
npm install

```
ローカルホストで表示されているか確認します。
```
npm run serve
```

### STEP 1
<Style>タグに移動して、CSSを書きましょう。

revealというクラスのCSSを書きます。
イベントが発生されるまでにrevealを非表示にしたいので、opacityを０にして、
active（発生）したらアニメーションと一緒に表示させます。

補足）
「transition」で変化の対象と変化の秒数と変化の仕方をまとめて指定します。

```
.reveal{
  position: relative;
  transform: translateY(150px);
  opacity: 0;
  transition: 2s all ease;
}
.reveal.active{
  transform: translateY(0);
  opacity: 1;
}
```

### STEP 2

methodを書きます。
1)revealというクラスが付いている要素を選択します。

```
methods:{
    reveal() {
      const reveals = document.querySelectorAll(".reveal");
    }
}
```

2. アニメーションがsection要素が表示されるタイミングで発生させたいので、
そのため各要素の位置を確認しなければなりません。
今回 getBoundingClientRect()とwindow.innerHeight を使います。

Element.getBoundingClientRect() メソッドは、要素の寸法とそのビューポートに対する相対位置に関する情報を返します。(MDNにより)

innerHeight は Window インターフェイスの読み取り専用プロパティで、ウィンドウの内部の高さをピクセル単位で返します。水平スクロールバーがあれば、その高さを含みます。

<img src="https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect/element-box-diagram.png">


```
for (let i = 0; i < reveals.length; i++) {
        const windowHeight = window.innerHeight;
        const elTop = reveals[i].getBoundingClientRect().top;
        const elVisible = 150;
        if (elTop < windowHeight - elVisible) {
          reveals[i].classList.add("active");
        } else {
          reveals[i].classList.remove("active");
        }
      }

```

補足）
・windowHeightはビューポートの高さを測定
・elTopはreveal要素からの距離またスクロールの距離を測定
・elVisibleを使って、どのタイミング（距離）でsection要素を表示されるべきか決定（この場合150px）


最後に下記の関数でCSSクラスを動的に追加していきます。

```
if (elTop < windowHeight - elVisible) {
  reveals[i].classList.add("active");
} else {
  reveals[i].classList.remove("active");
}

```

reveal関数はこうなります。

```
function reveal() {
  const reveals = document.querySelectorAll(".reveal");
  for (let i = 0; i < reveals.length; i++) {
    const windowHeight = window.innerHeight;
    const elTop = reveals[i].getBoundingClientRect().top;
    const elVisible = 150;
    if (elTop < windowHeight - elVisible) {
      reveals[i].classList.add("active");
    } else {
      reveals[i].classList.remove("active");
    }
  }
}

```

最後に、created()のタイミングでイベントをロードするように設定して完了です。

```
window.addEventListener("scroll", reveal);
reveal();

```


