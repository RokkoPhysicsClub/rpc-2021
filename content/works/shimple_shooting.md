---
title: "ミニゲーム"
date: 2021-09-16T20:30:31+09:00
description: "普通のシューティングゲーム。"
image: "./img/simple_shooting/stage40.png"
draft: false
weight: 5
---
<div align="right">83rd kusa51 & 0x4C</div>

## 初めに

このゲームは、簡単に言うと、普通の(?)シューティングゲームです。普通のシューティングゲームですがレベル機能があったりします。

## 概要

製作過程
- 製作期間：約一年間
- 製作人数：2人
- コード：汚い

このゲームには色々なシステムがあります。

その一つとして、このゲームには各キーに特殊なスキルが割り当てられています。

!["スキル"](./../../img/simple_shooting/shooting_gaiyou.png)

## スキルについて

このゲームには次のようなスキルがあります

!["スキル"](./../../img/simple_shooting/skill.png)

ちなみにaキーとsキーはレベルを上げることで解放されます。

## 攻撃方法

右クリックで通常攻撃、左クリック(長押し)でチャージショットです。

!["charge"](./../../img/simple_shooting/charge.png)

## 移動方法

基本マウスカーソルで移動します。上下に動く際には矢印キーを使用します(w、e、s、dキーとかではないです！)

## 敵の種類

## 雑魚キャラ

現在16体存在しています
中には属性付与をするキャラ(毒、炎、雷など)もいます。

## ボス

5体います。うち二体はペアで登場します。
<br>ちなみにですがその二体ボスがいるステージはレベリングしやすいです(ほぼ無意味な豆知識)



## 0x4Cからの話
## 技術的な話
実は最近まではこのゲームのコードは殴られてもいいほど本当に汚いコードでした。<br>
概要としては、
- 敵の管理には可変長配列であるArrayListを使用
- ConcurrentModificationExceptionを避けるために次のフレームで処理する敵をバッファのArrayListに使用
- しっかり全ての敵はクラスを継承している
- リフレクションはインスタンスの生成のみで済むようにバッファを設けている
- アイテム追加、レシピの追加はテキストファイルで容易に管理可能<br>

分かりやすく言うと、簡単に 後から要素を追加できるよって事です。<br>
ちなみに、リフレクションという手段は動作の安全性を確保するのが難しくなるのであまり好まれていません。

↓リフレクション関係のコード。怒られる自信はある。
```java
ArrayList<Constructor>EnemyClass;//バッファ

for(int i=0;i<enemyname.size();i++){
　try{
    EnemyClass.add(Class.forName("Simple_shooting$Enemy"+str(i+1))
    .getDeclaredConstructor(Simple_shooting.class));
  }catch(ReflectiveOperationException e){}
}//バッファへのコンストラクタの追加

(EnemyFrame)EnemyClass.get(spown.spown()-1).newInstance(this)//インスタンス生成。何回も実行されるのはこの部分。
```
↓敵の処理
```java
for(Enemymanagement enemy: enemies){
  enemy.get().display();
}//敵の描画

for(Enemymanagement enemy: enemies){
  enemy.get().update();
  if(!enemy.get().isDead){
    extEnemies.add(enemy);
  }
}//敵の更新とバッファへの追加
```
大体こんな感じです。
## これからについて
これからの方針としては、敵やステージの追加、さらに拡張しやすくするなどのことが挙げられます。<br>
↓開発段階のステージ<br>
!["開発途中のバージョンの敵(stage40)"](./../../img/simple_shooting/stage40.png)<br>
まあ、結構時間がかかるのはどうしても避けられないので、来年に乞うご期待!
## 開発者からのコメント
このシューティングゲームの開発期間は1年に及んだので、僕としては結構思い入れが深い作品になっています。なので、開発が終わるということは多分無いと思います。そんなわけで、この企画も毎年続いていくと思うので、ほどほどに期待しておいて下さい。

## 最後に

とまあざっと説明ははこのくらいです。
<br>見ている側はつまんなさそうだと思いますが、ぜひ一回遊んでください。