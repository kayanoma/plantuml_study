# plantUMLの勉強ログ

<!-- ## メモ
imagesブランチに画像ファイルを作成、それを参照して画像を埋め込む
md中にソースの埋め込みはしない
![リンク参考](https://github.com/kaitas/PlantUML-Study/blob/images/kawaiiPlantUML.png?raw=true "サンプル画像のレンダリング結果") -->

## 拡張機能について
以下のソースコードが@startumlから始まっている場合は[こちら](https://chrome.google.com/webstore/detail/pegmatite/jegkfbnfbfnohncpcfcimepibmhlkldo)のchrome拡張機能を利用するとumlの画像が表示されるようになります。
拡張機能により画像表示されているソースコードは該当画像をダブルクリックすることで元のソースを見ることができます
### このページでは拡張機能をオフにしてください
```plantuml
@startuml
(Hello World!!)
@enduml
```


## エラーや非表示
uml中で'、。,()'は使えなさそう
クラス図中で特にパーレン'()'が含まれているとメソッド扱いになる
```plantuml
@startuml
class Hello_World!!{
  Hello
  (World)!!
}
@enduml
```
![](https://github.com/kayanoma/plantuml_study/blob/images/images/helloworld.png?raw=true "メソッド化に注意")

## 注意
- 画像はモノによってはかなり重くなる、previewが使い物にならなくなるので注意（縦横のサイズが重要か？, webページだと重かったのでTwitterのアイコンから引っ張ってきた）
- 作成した画像中のテキストはコピペできるがそのままではリンクにならない
そもそも最終的には画像になるのでリンクにしても編集中しか使えない

## レイアウトについて
大雑把なものは```top to bottom direction``` ```left to right direction```で指定。
細かい調整は方向指定矢印＋hiddenで行う。
位置調整のため中継オブジェクトを生成して矢印で場所指定をしてみたが試したものは上手くいかなかった。
left to right中にdown矢印を使っても真下に来ない（南南東方向）
top to bottomだと逆に東南東方向に配置


## テクニック 
document作成時に新しく学んだ内容を以下に記述（生成画像だけでなくソースの方を見て欲しいのでソースも記述）


```plantuml
@startuml

'一行コメント

/'
複数行コメント
'/

'allow_mixingを使うとクラス図とユースケース図の共存が可能
allow_mixing

'methodを非表示
hide members
show fields

rectangle 紹介{
  /'classの内部にあるものはプロパティとメソッドに自動で分けられ、
  class_name
  property（画像など'()'がついてないものはこちら）
  method()
  上のように分割される
  '/
  class 転声こえうらない女性キャラ <<vtuber>>{
    <img:https://vr.gree.net/lab/vc/img/10.768c4c29.png{scale=0.3}>
    プロフィール
    愛称　カワボちゃん
  }

  'class を非表示代わりに<<ステレオタイプ>>が表示されてしまう
  hide <<vtuber>> circle
  show <<vtuber>> fields

  '以下でステレオタイプも消せる
  hide <<vtuber>> stereotype
  /'allow_mixingで使えるようになったがusecaseを使って宣言する必要がある
  (sing)はだめ
  '/
  usecase sing <<before>>
  転声こえうらない女性キャラ -- sing
  usecase speak <<ing>>
  転声こえうらない女性キャラ -- speak
  '方向指定矢印＋hidden属性で多少は場所を調整できる
  sing -down[hidden]- speak
  usecase dance <<after>>
  転声こえうらない女性キャラ -- dance

  /'ノート（コメント的な）が使える
  対象
  note 場所: 内容
  '/
  class 転声こえうらない女性キャラ
  note right: クラス
  class 転声こえうらない女性キャラ
  '[[URL テキスト]]でリンクになる　うまくいかない場合は前後に全角スペースを入れると解決する場合がある
  note left: [[https://vr.gree.net/lab/vc/ 転声こえうらない]]はこちら
  usecase sing
  note right : usecase
  usecase speak
  note right : [[http://www.yosbits.com/wordpress/?page_id=4857 umlで使える色一覧]]

}

/'色の変換が行える
色によって時間の区別や強調等が行える
'/
skinparam usecase {
	BackgroundColor<<before>> powderblue
	BorderColor slateblue

	BackgroundColor<< ing >> darkseagreen
	BorderColor<< ing >> DarkSlateGray

  BackgroundColor<< after >> darksalmon
	BorderColor<< after >> maroon
}
hide <<before>> stereotype
hide <<ing>> stereotype
hide <<after>> stereotype

@enduml
```
![](https://github.com/kayanoma/plantuml_study/blob/images/images/kawabo.png?raw=true "まとめ")