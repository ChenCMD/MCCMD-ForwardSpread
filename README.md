# ForwardSpread

## なにこれ
前方に座標拡散を行えるよ

## 何してるのこれ
プレイヤーのsin/cos取って回転行列に突っ込んでるだけ

## どう使うのこれ
    #forwardspread:returnにfunction追加するとその座標から実行できるよ
    
    scoreboard players set $distance ForwardSpread n //どれくらい視点から離すか n = 0.1m
    scoreboard players set $spread ForwardSpread n //どれくらい拡散させるか n = 直径0.1m
    function forwardspread:api/square_run || api/circle_run //実行

## ここ気を付けてね
- デフォルトで`#forwardspread:return`に`forwardspread:api/return_test`が入ってるよ  
これはね、その座標にparticleを出すだけの確認用
- UUID 0-0-0-0-a 使ってるよ 衝突する場合は書き換えてね
- 負荷面は気を使ってるけど重かったらごめんね
- これ使って何か起きても責任は取らないよ
- $spreadを47以上にセットして円形拡散を使うと内部処理でオーバーフローして大きくならないよ
