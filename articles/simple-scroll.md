---
title: "（VUE)ライブラリーを使わずスクロールアニメーション"
emoji: "🤓"
type: "tech"
topics: ['VUEJS','アニメーション','css']
published: false
---
初心者として、ライブラリー使いがちだと思いませんか？私もでした。
ライブラリーは使いやすく、とても便利ですが、バージョンアップした時に必要ない更新作業を発生して大変な目に合いました。
その経験から学んだのが１００％必要でない限りピュアーJSで書くのがBESTです！

今回はライブラリー使わずにCSS Transitionプロパティと9行のJavascriptコードでこのようなスクロールアニメーションを実装！



トランジションあまり分からないから下記の記事おすすめです。
https://webst8.com/blog/css-transition/　

### 最終的にこうなります！


## VUE環境を整える 

スタートファイルをクローンしましょう。
```
git clone git@github.com:ogorei/simple-scroll-starter.git

```
ダウンロードできたらエディターを開いて必要なパッケージをインストールする。
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
イベントが発火されるまでにrevealを非表示にしたいので、opacityを０にして、
active（発火）したらアニメーションと一緒に表示させます。

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

2. アニメーションがsection要素が表示されるタイミングで発火させたいので、
そのため、各要素の位置を確認しなければなりません。
今回getBoundingClientRect()とwindow.innerHeight　を使います。

Element.getBoundingClientRect() メソッドは、要素の寸法と、そのビューポートに対する相対位置に関する情報を返します。
(MDNにより)

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
・windowHeightはビューポートの高さを測る
・elTopはreveal要素からの距離またスクロールの距離を測る
・elVisibleを使って、どのタイミング（距離）でsection要素を表示されるべきか決めます。（この場合150px）


最後に下記の関数でCSSクラスをダイナミックに追加されていきます。

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

created()のタイミングでイベントをロードされるように設定しましょう

```
window.addEventListener("scroll", reveal);
reveal();

```
