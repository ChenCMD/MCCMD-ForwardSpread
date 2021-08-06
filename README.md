# ForwardSpread
前方に座標拡散を行うことのできるライブラリ

## 対応バージョン
1.16.X, 1.17.X

## インストール
下記からダウンロードしたものを解凍せずにdatapacksに入れてね
* [1.16.X](https://github.com/ChenCMD/MCCMD-ForwardSpread/releases/latest/download/ForwardSpreader1.16.zip)
* [1.17.X](https://github.com/ChenCMD/MCCMD-ForwardSpread/releases/latest/download/ForwardSpreader1.17.zip)

## 使い方
`storage forward_spreader:`の`Distance`と`Spread`に値を入れて`function forward_spreader:api/<circle|square>`を呼び出してね  
呼び出すとfunctionを実行したEntityが実行地点から`Distance`m離れた場所で最大直径`Spread`m移動した場所にTPするよ

## サンプル
```mcfunction
# 実行者の向いている方向から10m離れた地点で1.5m拡散するParticleを召喚する

# 返り値のEntity
    summon marker ~ ~ ~ {Tags:["SpreadMarker"]}
# 拡散の設定 // この場合最大10mで直径1.5m拡散する
    # どれくらい視点から離すか
        data modify storage forward_spreader: Distance set value 10f
    # どれくらい拡散させるか
        data modify storage forward_spreader: Spread set value 1.5f
# 処理の実行
    execute at @s as @e[type=marker,tag=SpreadMarker,limit=1] run function forward_spreader:api/circle
# 実行者
    execute facing entity @e[type=marker,tag=SpreadMarker,limit=1] feet anchored eyes positioned ^ ^ ^10 run particle end_rod
# リセット
    kill @e[type=marker,tag=SpreadMarker,limit=1]
```
> [forward_spreader:example](https://github.com/ChenCMD/MCCMD-ForwardSpread/blob/master/data/forward_spreader/functions/example.mcfunction)

## 注意事項
* チャンク(0,0)をforceloadしてるよ
* UUID `0-0-0-0-a` 使ってるよ 衝突する場合は書き換えてね
* 負荷面は気を使ってるけど重かったらごめんね
* これ使って何か起きても責任は取らないよ
* Spreadの絶対値が4.634f以上にすると内部処理でオーバーフローして想定した挙動にならないからDistanceを大きくするなりして対応してね

## Q & A
### Q. 何に使えるのこれ
例えば、銃の弾拡散とか...所謂精度って概念を作るのに使えるよ

### Q. Rotationに乱数値加算すれば良くない？
この方法だと上や下向いた時にジンバルロックって言う正常に拡散しない現象が起きるはずだよ

### Q. 何してるのこれ
実行方向のsin/cos取って回転行列に突っ込んで元の座標に加算してるよ

### Q. 改造とか再配布ってして大丈夫？
このデータパックライブラリは[Creative Commons Zero v1.0 Universal](https://github.com/ChenCMD/MCCMD-ForwardSpread/edit/master/LICENSE)の元に提供されているよ  
改造や再配布、商用/私的利用等は一切の制限なく許可されているよ  
ただし、改造や再配布の有無に関わらずバグ等が合っても製作者は責任を取らないよ

### Q. バグあったんだけど
[issue](https://github.com/ChenCMD/MCCMD-ForwardSpread/issues/new)立ててくれれば対応するよ

### Q. コード内の#declareとかってなに？
[IMP-Doc](https://github.com/ChenCMD/datapack-helper-plus-JP/wiki/IMP-Doc)ってやつだよ  
VSCodeにData-pack Helper Plusって拡張機能を入れてるとそこで定義した物が補完されるようになるからおすすめだよ