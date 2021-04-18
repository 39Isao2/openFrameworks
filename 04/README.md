# オブジェクト指向プログラミング(object oriented programming)
現実世界の物に例えて、オブジェクト間でメッセージを送り合う設計で、<br>
プログラミングしていく考え方。oFではこちらを推奨。<br>
例えばこちらの例だと、「飼い主」「犬」「背景」などにソースを分けて管理する。

<img src="images/oop2.png" width="600px">

## 実際のオブジェクト指向のコード

多すぎる配列はコードが見にくいし書くのが面倒。<br>
x座標，y座標，速度...など一つのオブジェクトが持つデータの種類が増えてきたときが出番です<br>
コードの中で配列が全く出ない，<br>または１つか２つしか出ないコードにはOOPのメリットはそこまで光りません。。<br>

```
イメージの例: 

１、いままでの配列を使った書き方

座標が100個
色が100個
サイズが100個

for(100回){
	座標[i]
	色[i]
	サイズ[i]
	円を書く
}


２、クラス使った書き方
(座標、色、サイズ)のデータを持っている円が100個
for(100回){
	円を書く
}

```

# Processingで書いてみる

<img src="images/oop.png" width="700px">

## 配列ver
```
int NUM = 100;

float[] x = new float[NUM];
float[] y = new float[NUM];
float[] vy = new float[NUM];         
float[] size = new float[NUM];       
color[] col = new color[NUM];       

void setup(){
  size(1000, 600);
  noStroke();                   
  for(int i=0; i<NUM; i++){
    x[i] = random(width);
    y[i] = random(height);
    vy[i] = random(1,3);        
    size[i] = random(5, 40);    
    col[i] = color(random(255),random(255),random(255));
  }
}

void draw(){
  background(255);
  for(int i=0; i<NUM; i++){
    fill(col[i]);                                                  
    ellipse(x[i], y[i], size[i], size[i]);
    y[i] -= vy[i];               
  }
}

```

## classを使ったオブジェクト指向ver

```

class Circle{
  float x;
  float y;
  float vy;
  float size;
  color col;

  Circle(){
    x = random(width);       
    y = random(height);
    vy = random(1, 3);
    size = random(5, 40);
    col = color(random(255),random(255),random(255));
  }
  
  void display(){
    fill(col);
    ellipse(x, y, size, size);
    y -= vy;
  }
}

```

```


int NUM = 100;
Circle[] c = new Circle[NUM];

void setup(){
  noStroke();
  size(1000,600);
  for(int i=0; i<NUM; i++){
    c[i] = new Circle();
  }
}

void draw(){
  background(255);
  for(int i=0; i<NUM; i++){
    c[i].display();
  }
}


```




# openFrameworksでクラスとインスタンスを使ってみる
classは設計図。インスタンスはそれに基づいて生成した実態。<br>
先程のオブジェクト指向をopenFrameworks版で書いてみる<br>

## クラスファイルの作成
ファイル → new → file → c++ → クラス名を記述(今回はParticle) → 格納先はsrcフォルダを指定<br>
Particle.hpp (クラス名の先頭は大文字が流儀)


# シンプルなクラスの例

<img src="images/class2.png" width="500px">

Particle.hpp
```
#pragma once

#include "ofMain.h"


class Particle{
    
public:

    // コンストラクタ (インスタンス化した時に実行されるメソッド)
    Particle();
    
    // メソッド
    void setup();
    void draw();
    
    // プロパティ
    glm::vec2 pos; // 位置
    ofColor col; // 色
    float radius; // 半径
    
};


```


Particle.cpp
```
#pragma once
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
    
        // Particleクラスのインスタンス宣言   (正確にはポインタ変数で)
        Particle* p1;
        Particle* p2;
};
```

ofApp.cpp
```
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup(){
    
    // インスタンスの生成
    p1 = new Particle();
    p2 = new Particle();
    
    p1->setup();
    p2->setup();
    
}

//--------------------------------------------------------------
void ofApp::update(){

}

//--------------------------------------------------------------
void ofApp::draw(){
    
    p1->draw();
    p2->draw();

}

```


### 泡の様に上に上るソース

<br>
これのoFバージョンです<br><br>
<img src="images/oop.png" width="700px">

Particle.hpp
```
#pragma once

#include "ofMain.h"


class Particle{
    
public:

    Particle();
    void update();
    void draw();
    

    glm::vec2 pos;
    float velocity;
    float size;
    ofColor col;
    
};

```

Particle.cpp
```
#pragma once
#include "Particle.hpp"


Particle::Particle(){
    pos.x = ofRandom(0,ofGetWidth());
    pos.y = ofRandom(0,ofGetWidth());
    velocity = ofRandom(1, 3);
    size = ofRandom(5, 40);
    col = ofColor(ofRandom(255),ofRandom(255),ofRandom(255));
}

void Particle::update(){
    
    pos.y -= velocity;
    
    if(pos.y < 0){
        pos.y  = ofGetHeight();
    }

}

void Particle::draw(){
    
    ofSetColor(col);
    ofDrawCircle(pos.x, pos.y, size, size);
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
    
        static const int NUM = 100;
    
        // Particleクラスをインスタンス化
        Particle p[NUM];
    
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
    
}

//--------------------------------------------------------------
void ofApp::update(){
    
    for(int i=0; i<NUM; i++){
        p[i].update();
    }

}

//--------------------------------------------------------------
void ofApp::draw(){
    
    for(int i=0; i<NUM; i++){
        p[i].draw();
    }

}


```




### 引数渡すver

Particle.hpp
```
void setup(float r);
```
Particle.cpp
```
void Particle::setup(float r){
    // 位置
    pos.x = ofRandom(300, 600);
    pos.y = ofRandom(300, 600);
    
    // 半径
    radius = r;
    
    // 色
    col = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

```

ofApp.cpp
```
p1.setup(300);
p1.setup(200);

```
