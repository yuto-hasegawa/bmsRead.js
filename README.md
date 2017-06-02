# bmsRead.js
## bmsRead.jsとは
bmsRead.jsは、ファイルまたはフォルダからのドラッグアンドドロップによりBMSファイルの読み込みを可能にするjQeuryプラグインです。  
## 使い方
本プラグインを使うための最小構成は以下の通りです。
### HTML
```
<!-- jQueryを読み込み -->
<script
  src="https://code.jquery.com/jquery-3.2.1.min.js"
  integrity="sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4="
  crossorigin="anonymous"></script>

<!-- bmsRead.jsを読み込み -->
<script src="./bmsRead.js"></script>

<!-- ファイルをドロップする領域 -->
<div class="sample"></div>
```

### Javascript
```
$('.sample').bmsRead();
```

## 結果
### オブジェクトの構成
bmsReadを行い、読み込みがすべて終わると onRead メソッドが呼び出され、第一引数にBMSデータオブジェクトが渡されます。BMSデータオブジェクトは以下のような構成をとっています。

    {
        files:{
            フォルダ名:[
                {
                    各BMSファイルの詳細情報
                },
                {
                    各BMSファイルの詳細情報
                },
                {
                    各BMSファイルの詳細情報
                },
                ...
            ],
            フォルダ名:[
                {
                    各BMSファイルの詳細情報
                },
                {
                    各BMSファイルの詳細情報
                },
                {
                    各BMSファイルの詳細情報
                },
                ...
            ],
            ...
        }

onRead メソッドの内容は初期化時に書き換えることができます。

### BMS詳細情報のパラメーター
上記構成の「各BMSファイルの詳細情報」にあたる部分には以下の情報が格納されています。

| Parameter | Description |
|:-----------|:------------|
| artist     | ファイル内の #ARTIST|
| bmshash | BMSファイルのMD5ハッシュ |
| bmshash_old    | （※使用しないでください）<br>このパラメーターは BMS Search (http://bmssearch.net/)において発生していた誤ったハッシュの変換に基づいたファイルハッシュです。データベース上の互換性を保つために残されている情報であり、正しい値ではありません。|
| bmson       | ファイルがbmsonファイルであった場合は 1, それ以外は 0        |
| chart_name         | bmson における chart_name          |
| difficulty       | ファイル内の #DIFFICULTY       |
| filename    | 読み込んだファイルのファイル名     |
| filesize | 読み込んだファイルのファイルサイズ(KB) |
| genre | ファイル内の #GENRE |
| lanes | 後で書く|
| maxbpm | BPMの最大値 |
| minbpm | BPMの最小値 |
| mode_hint | bmson における mode_hint |
| player | ファイル内の #PLAYER |
| playlevel | ファイル内の #PLAYLEVEL |
| title | ファイル内の #TITLE |
| totalnotes | 総ノート数 |

## 設定
bmsRead の初期化時に以下のようにして設定を行うことができます。
```
$('.bmsbox').bmsRead({
    'folderWait':'ここにファイルかフォルダをドラッグアンドドロップしてね',
    'onDrop': function() {
        this.children('.bmsRead_message').text('投下！');
    }
});
```

設定できる項目は以下の通りです。
| Parameter | Type | Default | Description |
|:-----------|:------------|:------------|:------------|
| folderWait | string | 'Drag and Drop Files or Folders Here.' | フォルダドロップ対応ブラウザにおける初期表示です。|
| fileWait | string | 'Drag and Drop Files Here.' | ファイルドロップのみ対応のブラウザにおける初期表示です。|
| noWait | string | 'Your Browser doesn\'t support bmsRead.js' | ファイルドロップ非対応ブラウザにおける初期表示です。|
| onDrop | function | 略 | ファイルがエリアにドロップされたときに呼び出されます。|
| onRead | function | 略 | BMSファイルの読み込みが終わると呼び出されます。BMSの詳細情報オブジェクトは第一引数に渡されます。|
| onProceed | function | 略 | ファイル数のカウントが行われたとき、もしくは進捗が生まれたときに呼び出されます。第一引数に全ファイル数、第二引数に処理済みのファイル数が渡されます。|

## ライセンス
The MIT License (MIT)  

Copyright (c) 2017 q/stol

このプラグインは、各種ライセンスに基づき以下のプラグインを改変して組み込んでいます。


encoding.js by polygon planet  
licensed under the MIT license.  
https://github.com/polygonplanet/encoding.js  


md5.js by Masanao Izumo  
written "You can redistribute it and/or modify it without any warranty."


yjd.js by 2014 yujakudo  
written "尚、今回作成した記事中で参照しているファイル（yjdmd5.js, testcase.js, md5test.html）の再利用や改変は、ご自由に行って下さい。"
on http://www.yujakudo.com/blogs/develop/hash-on-js/md5-on-javascript/


ここにお礼申し上げます。