# Webサイト向け実装マニュアル

このマニュアルには、AdStirの広告タグをWebサイトに掲載する際のカスタマイズ方法が記載されています。

## インライン広告の掲載

インライン広告(通常のバナー広告)を掲載するには、掲載したい箇所に、管理画面から取得したタグを挿入します。

```html
...
<div id="ad_area_1">
  <!-- AdStirタグはここから -->
  <script type="text/javascript">
    var adstir_vars = {
      ver: "4.0",
      app_id : "MEDIA-XXXX",
      ad_spot: 1,
    };
  </script>
  <script type="text/javascript" src="http://js.ad-stir.com/js/adstir.js?20130527"></script>
  <!-- ここまで -->
</div>
...
```

上記のコードでは、&lt;div id="ad_area_1">〜&lt;/div>の箇所に、広告が掲載されます。

## オーバーレイ広告の掲載

オーバーレイ広告を掲載するには、ページ内の任意の箇所に、管理画面から取得したタグを挿入します。\
推奨の掲載箇所は、ページの最下部、&lt;/body>の直前です。

```html
...
<!-- AdStirタグはここから -->
<script type="text/javascript">
  var adstir_vars = {
    ver: "4.0",
    app_id : "MEDIA-XXXX",
    ad_spot: 1,
    floating: true,
  };
</script>
<script type="text/javascript" src="http://js.ad-stir.com/js/adstir.js?20130527"></script>
<!-- ここまで -->
</body>
</html>
```

上記のコードでは、&lt;div id="ad_area_1">〜&lt;/div>の箇所に、広告が掲載されます。

## Tips

### レスポンシブデザインへの対応

AdStirでは、スマートフォン向けとPC向けの広告タグは共通の形式を使用していますが、\
スマートフォン向けWebサイトとして登録された場合には、スマートフォン向けの案件を配信するように設定します。\
(ただし、RTB広告においては、DSPがPCからのアクセスと判断した場合には、自動的にPC向けの広告が掲載されることがあります)

そのため、スマートフォン向けサイトとPC向けサイトで別々のタグを出し分けて頂くことを推奨しておりますが、\
レスポンシブデザインを採用している場合など、出し分けが難しいケースがあります。

その場合、下記のいくつかのパターンから対応を選択します。

#### 同じ箇所でPCとスマートフォンの広告タグを切り替える
```html
<script type="text/javascript">
  var adstir_vars = {
    ver: "4.0",
    // 管理画面から取得したPC用のIDに置き換えてください
    app_id: "MEDIA-YYYY",
    ad_spot: 1,
    floating: true,
  };
  if (navigator.userAgent.match(/(iphone|ipod|android)/i)){
    // 管理画面から取得したスマートフォン用のIDに置き換えてください
    adstir_vars.app_id = "MEDIA-XXXX";
    adstir_vars.ad_spot = 1;
  }
</script>
<script type="text/javascript" src="http://js.ad-stir.com/js/adstir.js?20130527"></script>
```

#### スマートフォンのみで広告が呼び出されるようにする
```html
<script type="text/javascript">
  if (navigator.userAgent.match(/(iphone|ipod|android)/i)){
    window.adstir_vars = {
      ver: "4.0",
      // 管理画面から取得したIDに置き換えてください
      app_id: "MEDIA-XXXX",
      ad_spot: 1,
      floating: true,
    };
    document.write('<scr'+'ipt src="http://js.ad-stir.com/js/adstir.js?20130527"><\/scr'+'ipt>')
  }
</script>
```
