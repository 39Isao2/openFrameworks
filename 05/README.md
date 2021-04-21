# ポインタとアドレス
ポインタとは、変数のアドレスを取り扱う変数のことです。<br>
アドレスとはメモリ上に与えられた番号のことです。<br>

## コードを書いて確かめる
変数を宣言すると、その変数にアドレスすなわちメモリ上の番号が与えられます。<br>
<br>
<img src="images/pointa.png">
<br>
<br>

参考:
http://www.isc.meiji.ac.jp/~re00079/EX2.2009/2009_24.html

```

 // フレームレート表示
 ofDrawBitmapString(ofToString(ofGetFrameRate()) + "fps", 20, 20);


 int num = 10; // int型変数

 // 普通にint型numを出力
 cout << num << endl;   // 結果10

 // 変数numのアドレスを出力 (頭に&をつける)
 cout << &num << endl;   // 結果0x7ffeefbff3c8

 // ポインタ変数の作成方法
 int* pNum = &num;
 cout << pNum << endl;   // 結果0x7ffeefbff3c8
 

```



- ポインタ変数はアドレスを保存する変数
- ポインタ変数の宣言は型の後ろに* をつける int* pNum
- 変数のアドレスを知るには &をつける &num
- ポインタ変数から値を取るには変数名の前に*をつける *pNum　間接参照演算子


## ポインタを使って高速化の書き方

ofApp.hpp

```
#pragma once

#include "ofMain.h"
#include "Particle.hpp"

class ofApp : public ofBaseApp{

    public:
        void setup();
        void update();
        void draw();
    
        static const int NUM = 1000;
    
        // Particleクラスのインスタンスを宣言
        Particle* p[NUM];
    
};
```

ofApp.cpp
```
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup(){
    
    ofSetFrameRate(60);
    
    ofBackground(0);
    
    ofSetCircleResolution(64);
    
    
    for(int i=0; i<NUM; i++){
        
        // 色
        ofColor col = ofColor(ofRandom(256),ofRandom(256),ofRandom(256));
        
        // サイズ
        float diameter = ofRandom(1, 4);
        
        // インスタンスの生成
        p[i] = new Particle(&diameter, &col);
    }
    
}

//--------------------------------------------------------------
void ofApp::update(){
    
    for(int i=0; i<NUM; i++){
        p[i]->update();
    }

}

//--------------------------------------------------------------
void ofApp::draw(){
    
    for(int i=0; i<NUM; i++){
        p[i]->draw();
    }

}

```

Particle.hpp

```
#pragma once

#include "ofMain.h"


class Particle{
    
public:

    Particle(float* s, ofColor* c);
    void setup();
    void update();
    void draw();
    

    glm::vec2 pos;
    float velocity;
    float diameter;
    ofColor col;
    
};
```

Particle.cpp

```
#pragma once
#include "Particle.hpp"


Particle::Particle(float* s, ofColor* c){
    pos.x = ofRandom(0,ofGetWidth());
    pos.y = ofRandom(0,ofGetWidth());
    velocity = ofRandom(1, 3);
    diameter = *s;
    col = *c;
}


void Particle::setup(){

}


void Particle::update(){
    
    pos.y -= velocity;
    
    if(pos.y < 0){
        pos.y  = ofGetHeight();
    }

}

void Particle::draw(){
    
    ofSetColor(col);
    ofDrawCircle(pos.x, pos.y, diameter);
}

```


メモ
```
ofAppで
クラス名* 変数で宣言
&で渡して、*で受け取る

ofApp.hとcpp
------------------------------------
// 変数pos作る
ofVec2f pos;
// コンストラクタに&で渡す
SineCircle* sc = new SineCircle(&pos);
------------------------------------
SineCircle.cpp
------------------------------------
// &できたので*で受け取る
SineCircle::SineCircle(ofVec2f* pPos, int s){
    // *がきたので->でゲット！
    pos.x = pPos->x;
    pos.y = pPos->y;
    size = s;
}
------------------------------------
SineCircle* sc
*で作ったインスタンス（ポインタ変数）は
sc->update();
sr->draw();
みたいに->で使う。
```
