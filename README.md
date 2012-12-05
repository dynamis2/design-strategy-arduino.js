
## Arduino.js でブラウザからハードウェアを操作する

## Arduino をゲットする

[Arduino UNO](http://arduino.cc/en/Main/ArduinoBoardUno) をリファレンスとして扱います。他のモデルでも動作するかも知れませんが、動作しないかも知れません。他のモデルでは動作する場合でもピン配列などが異なるので、いろいろと読み替えてもらう必要があります。

### Arduino IDE  をインストールする

Arduino IDE の[ダウンロードページ](http://arduino.cc/en/Main/Software) から自分の OS にあったバージョンをダウンロードし、インストールしてください。

### Arduino に Command Server を書き込む

arduino.js を使うためには Arduino 内部にプログラムを書き込む必要があります。sketch/CommandServer/CommandServer.ino を Arduino SDK で開き、Arduino にアップロードして(マイコンボードに書き込むボタンを押して)ください。 

### Firefox に arduino.js for webpages をインストール

addon/arduino-js.xpi を Firefox にドロップしてインストールしてください。

### blink.html を自分の環境に合わせて編集する

webpage/blink.html には次のように LED を点滅させる JavaScript が書かれています。
```
var blink = function(value) {
    var arduino = document.arduino;
    arduino.analogWrite(13, value);
    if (value == 255) {
$("#blink-label").addClass("blinking");
    } else {
$("#blink-label").removeClass("blinking");
    }
    setTimeout(blink, 1000, value == 0 ? 255 : 0);
}

$(document).ready(function() {
    var arduino = document.arduino;
    arduino.open("/dev/cu.usbmodemfa131");
    arduino.pinMode(13, true);
    //start blinking
    blink(0);
});
```

このコードについては [arduino.js のページ](http://www.mecha-mozilla.org/projects/arduino.js/) の説明も参照してください。

* arduino.open("/dev/cu.usbmodemfa131"); と書かれている部分では PC に接続している Arduino のシリアルポートを指定する必要があります。Arduino IDE の「ツール → シリアルポート」を参照して書き換えてください。

* [pinMode()](http://arduino.cc/en/Reference/PinMode) や [analogWrite()](http://arduino.cc/en/Reference/AnalogWrite) では LED を接続する端子の番号を指定します。接続したいピンに合わせて書き換えてください。

### Arduino に LED を接続する

指定したピンに LED を接続してください。

### Firefox で blink.html を開く

blink.html を開くと LED が点滅します。しなかったら手順を見直したり周りに聞いたりして頑張って解決しましょう。

### もっとあそぶ

[arduino.js のページ](http://www.mecha-mozilla.org/projects/arduino.js/) や [Arduino の Language Reference](http://arduino.cc/en/Reference/HomePage) を参考にしながら色々試してください。


## References:
* Arduino 
	* http://arduino.cc/
* arduino.js の紹介と API
	* http://www.mecha-mozilla.org/projects/arduino.js/
* Arduino のプログラム書き込み手順
	* [Getting Started with Arduino](http://arduino.cc/en/Guide/HomePage)
		* http://arduino.cc/en/Guide/Windows
		* Mac: http://arduino.cc/en/Guide/MacOSX
* Arduino Language Reference
	* arduino.js から操作する場合は [arduino.js ページ](http://www.mecha-mozilla.org/projects/arduino.js/) に書かれた API を参照
	* http://arduino.cc/en/Reference/HomePage



