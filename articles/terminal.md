---
title: "MacデフォルトのZSHをかっこよくしてみた！"
emoji: "🤓"
type: "Tech"
topics: ['ターミナル','おしゃれ']
published: True
---
Before／After


### 1 
ターミナルを開いて、Oh my zshをダウンロードします。
https://ohmyz.sh/　

```
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

```
### 2

ホームディレクトリーにいることを確認して下記のレポをクローンします。
```
cd ~ 

```

https://github.com/romkatv/powerlevel10k

```
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ~/powerlevel10k
```

### 3

.zshrc に入ってデフォルトテーマを切り替えます。

```
vi ~/.zshrc 

```
＃を使ってデフォルトテーマをコメントアウトして新しいテーマをその下に貼ります。


shashin here 

編集終わりましらた下記のコマンドで確定します。
```
$ source .zshrc

```