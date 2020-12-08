# 図形の描画
openFrameworksの基本図形です。<br>
Processing経験者の方は、関数名の頭にoFとつけると覚えやすいです。

<img src="https://github.com/55Kaerukun/openFrameworks/blob/main/FigureAndColor/images/sckech.png" width="400px">

## 基本図形

```
// 線
ofDrawLine(50,50,100,100);

// 四角形
ofDrawRectangle(100, 100, 100, 50);

// 正円
ofDrawCircle(100, 100, 250);

// 楕円
ofDrawEllipse(100, 100, 50, 100);

// 三角形
ofDrawTriangle(100, 100, 150, 150, 50, 150);


// 頂点
ofVertex(100,100);
//3Dの場合
ofVertex(100,100,100); 


// パスで図形を描画 (ひし形の例)
ofBeginShape();
    // ここに(x,y)のポイントを追加
    ofVertex(150, 30);
    ofVertex(210, 150);
    ofVertex(150, 270);
    ofVertex(90, 150);
ofEndShape(); //パスを閉じる


```

### 基本図形のオプション
```
// 線幅の設定  
ofSetLineWidth(4);
 
// 円の角の数(円を滑らかにする)
ofSetCircleResolution(64);

// 四角形をの起点を中心に 
ofSetRectMode(OF_RECTMODE_CENTER);

// 四角形の起点を左上に 
ofSetRectMode(OF_RECTMODE_CORNER);
 
```

#  描画色について
描画色、背景色、ブレンドモードの紹介です。



```
// R G B 指定
ofSetColor(255, 255, 255);
    
// 16進数指定(HEX)
ofSetHexColor(0xff0000);
    
// 塗り潰し
ofFill();
    
// 塗りつぶさない
ofNoFill();


// HSBモード (0~255で指定する)
ofColor c;
c.setHsb(ofRandom(255),255,255);

// 使いにくいので....
 
// setHSBA関数 (ofSetColorみたいに使えます。)
void ofApp::setHSBA(int hue, int saturation, int brightness, int alpha){
    int setHue = (int)ofMap(hue, 0 , 360, 0, 255);
    int setSaturation = (int)ofMap(saturation, 0 , 100, 0, 255);
    int setBrightness = (int)ofMap(brightness, 0 , 100, 0, 255);
    int setAlpha = (int)ofMap(alpha, 0, 100, 0, 255);
    ofColor c;
    c.setHsb(setHue, setSaturation, setBrightness, setAlpha);
    return ofSetColor(c);
}

```

## ブレンドモード
```
ofEnableBlendMode(OF_BLENDMODE_ALPHA);

//    アルファ使用 OF_BLENDMODE_ALPHA
//    加算 OF_BLENDMODE_ADD
//    乗算 OF_BLENDMODE_MULTIPLY
//    減算 OF_BLENDMODE_SUBTRACT
//    スクリーン OF_BLENDMODE_SCREEN

```

## 背景色について
描画色、背景色、ブレンドモードの紹介です。
```

// R G B 指定
//ofBackground(255, 255, 255);
    
// 16進数指定(HEX)
//ofBackgroundHex(0xff0000);
    
// 背景グラデーション (draw内に記述する)

void ofApp::draw(){
    ofColor colorOne;
    ofColor colorTwo;
    colorOne.set (255, 0, 0);
    colorTwo.set (0, 0, 255);

    ofBackgroundGradient(colorOne, colorTwo, OF_GRADIENT_CIRCULAR);
}
・グラデーションの種類

円形グラデーション OF_GRADIENT_CIRCULAR
線形グラデーション OF_GRADIENT_LINEAR
BARグラデーション OF_GRADIENT_BAR
    
    
ofBackgroundGradient(リファレンスの説明)
http://openframeworks.jp/documentation/graphics/ofGraphics.html#!show_ofBackgroundGradient
    
```


### color型変数
```
// color型 変数
ofColor c;

// サンプルコード
void ofApp::draw(){
    // 変数の定義
    ofColor redColor; 
    // 色のセット
    redColor.set(255, 0, 0); 
    // 描画色のセット
    ofSetColor(redColor); 
    // 描画
    ofDrawCircle(500,500,100); 
}
```


## 上の画像のサンプルコード
ofApp.cppのファイル
```
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup(){
    
    //円の角の数(円を滑らかにする)
    ofSetCircleResolution(64);
    
    // フレームレート60に
    ofSetFrameRate(60);
    
    // 背景白
    ofBackground(255, 255, 255);

}

//--------------------------------------------------------------
void ofApp::update(){

}
//--------------------------------------------------------------
void ofApp::draw(){
    
    // 線
    ofSetLineWidth(3);
    ofSetColor(0,0,0);
    ofDrawLine(200, 50,300, 150);
    
    // 四角形
    ofSetColor(0,255,0);
    ofDrawRectangle(200, 200, 100, 100);

    // 正円
    ofSetColor(255,0,0);
    ofDrawCircle(100, 100, 50);

    // 三角形
    ofSetColor(0,0,255);
    ofDrawTriangle(100, 200, 150, 250, 50, 250);
}
```
