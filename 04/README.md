# クラスとインスタンス
classとは設計図。インスタンスは実態。<br>
全部of.App内で配列などで管理するとコードが見にくくなるのでオブジェクトごとに分けて管理します。<br>




```
オブジェクト指向プログラミング
cとc++の違いはオブジェクト指向
objectがメッセージを送りあう

オブジェクト
プロパティ、メソッド
カプセル化 時計の時間合わせとかはpublic 中身機械構造はprivate
```

## クラスファイルの作成
ファイル → new → file → c++ <br>
Particle.h (クラス名の先頭は大文字が流儀)


# シンプルなクラスの例
Particle.hpp
```
#pragma once

#include "ofMain.h"


class Particle{
    
public:
    
    // プロパティ
    glm::vec2 pos; // 位置
    ofColor col; // 色
    float radius; // 半径
    
    // コンストラクタ
    Particle();
    
    // メソッド
    void setup();
    void draw();
    
};

```


Particle.cpp
```

#include "Particle.hpp"

Particle::Particle(){
    
}


void Particle::setup(){
    // 位置
    pos.x = ofRandom(300, 600);
    pos.y = ofRandom(300, 600);
    
    // 半径
    radius = ofRandom(10,50);
    
    // 色
    col = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

void Particle::draw(){
    ofSetColor(col);
    ofDrawCircle(pos.x, pos.y, radius);
}


```


ofApp.h
```
#pragma once

#include "ofMain.h"
#include "Particle.hpp"

class ofApp : public ofBaseApp{

    public:
        void setup();
        void update();
        void draw();
    
        // Particleクラス2つインスタンス化
        Particle p1;
        Particle p2;
};

```

ofApp.cpp
```
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup(){
    
    p1.setup();
    p2.setup();
    
}

//--------------------------------------------------------------
void ofApp::update(){

}

//--------------------------------------------------------------
void ofApp::draw(){
    
    
    p1.draw();
    p2.draw();

}


```




### 動的配列のクラス版 (少し難しいかも)
Particle.hpp
```
#pragma once

#include "ofMain.h"

class Particle{
    
public:
    
    // プロパティ
    glm::vec2 pos; // ポジション
    glm::vec2 speed; // スピード
    ofColor col; // 色
    
    // コンストラクタ
    Particle();
    
    // メソッド
    void update();
    void draw();
    void setPos(int x, int y);
    void setSpeed(float x, float y);
    void setColor(ofColor randomColor);
    
};
```

Particle.cpp
```
#include "Particle.hpp"

// コンストラクタ
Particle::Particle(){
    
}

void Particle::update(){
    pos += speed;
}

void Particle::draw(){
    ofSetColor(col);
    ofDrawCircle(pos.x, pos.y, 10);
}

void Particle::setPos(int x, int y){
    pos = glm::vec2(x, y);
}

void Particle::setSpeed(float x, float y){
    speed = glm::vec2(x,y);
}

void Particle::setColor(ofColor randomColor){
    col = randomColor;
}

```

ofApp.h
```
#pragma once

#include "ofMain.h"
#include "Particle.hpp"

class ofApp : public ofBaseApp{

    public:
        void setup();
        void update();
        void draw();
        void mousePressed(int x, int y, int button);
        void mouseDragged(int x, int y, int button);
        void keyPressed(int key);
    
    
    vector <Particle> particles;
    
};

```

ofApp.cpp

```
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup(){
    
    //円の角の数(円を滑らかにする)
    ofSetCircleResolution(64);
    
    // フレームレート60に
    ofSetFrameRate(60);
    
    // 背景黒
    ofBackground(0);
    
    // アルファ使用可能に
    ofEnableAlphaBlending();
}

//--------------------------------------------------------------
void ofApp::update(){
    
    for(int i=0; i<particles.size(); i++){
        particles[i].update();
    }

}
//--------------------------------------------------------------
void ofApp::draw(){
    
    for(int i=0; i<particles.size(); i++){
        particles[i].draw();
    }
    
}
//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button){
    
    
    // インスタンス生成
    Particle p;
    
    
    // クリック座標位置
    p.setPos(x, y);
    
    // ランダムなスピード
    glm::vec2 randomSpeed;
    randomSpeed.x = ofRandom(-5,5);
    randomSpeed.y = ofRandom(-5,5);
    p.setSpeed(randomSpeed.y, randomSpeed.y);
    
    // ランダムな色設定
    ofColor randColor;
    randColor.set(ofRandom(255), ofRandom(255), ofRandom(255));
    p.setColor(randColor);

    // 今までの情報を含んだインスタンスpを動的配列に追加
    particles.push_back(p);

    
}

//--------------------------------------------------------------
void ofApp::mouseDragged(int x, int y, int button){
    

}

void ofApp::keyPressed(int key){
    if(key == 'c'){
        particles.clear();
    }
}

```
