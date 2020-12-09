# 配列
値を順序付けてたくさんしまえるローカールームのような存在。<br>
一つの変数の中に、複数の値を入れること。<br>

<img src="https://github.com/55Kaerukun/Processing/raw/master/images/array.jpg" width="500px">


## 静的配列
最初から数が決まっている配列<br>
```
例:int型配列

// 一つのクラスに対して1つだけ存在し、しかも書き換えができない変数
static const int NUM = ５;

// 配列の作成 
int NumArr[NUM];

// 配列myArrにデータを保存
NumArr[0] = 10;
NumArr[1] = 20;
NumArr[2] = 30;
NumArr[3] = 15;
NumArr[4] = 5;


// 宣言を省略した記述方法
int NumArr[] = {10,20,30,15,5};
```


## サンプルコード : 大量のボールの跳ね返り処理

ofApp.h

```
#pragma once

#include "ofMain.h"

class ofApp : public ofBaseApp{

    public:
	void setup();
	void update();
	void draw();
    
    static const int NUM = 1000;
    
    // ポジション定義
    float posX[NUM];
    float posY[NUM];
    
    // スピード定義
    float speedX[NUM];
    float speedY[NUM];
    
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
    
    // 初期値セット
    for (int i=0; i<NUM; i++) {
        posX[i] = ofRandom(0,ofGetWidth()); // ofGetWidth 画面横幅取得
        posY[i] = ofRandom(0,ofGetHeight()); // ofGetHeight 画面縦幅取得
        speedX[i] = ofRandom(-10, 10);
        speedY[i] = ofRandom(-10, 10);
    }

}

//--------------------------------------------------------------
void ofApp::update(){
    
    // updateで位置の更新などの計算
    for (int i=0; i<NUM; i++) {
        posX[i] = posX[i] + speedX[i];
        posY[i] = posY[i] + speedY[i];
        
        if(posX[i] > ofGetWidth() || posX[i] < 0 ){
            speedX[i] = speedX[i] * -1;
        }
        
        if(posY[i] > ofGetHeight() || posY[i] < 0 ){
            speedY[i] = speedY[i] * -1;
        }
    }

}
//--------------------------------------------------------------
void ofApp::draw(){
    
    // 描画色指定
    ofSetColor(0,255,0,120);
    
    // 描画
    for (int i = 0; i<NUM; i++) {
        ofDrawCircle(posX[i], posY[i], 10);
    }
    
}

```


### ベクトルを使って簡潔にコードを書いてみよう！
ベクトルとは？ XとY、二つの座標を同時に格納するオブジェクト
```
ofVec2f pos; //ベクトル型変数の宣言
pos.x = 10.0;
pos.y = 20.0;

// もしくは
pos.set(10.0, 20.0);

(ofVec3fもあります。)
```

### 先ほどのコードのベクトル版

ofApp.h
```
#pragma once

#include "ofMain.h"

class ofApp : public ofBaseApp{

	public:
		void setup();
		void update();
		void draw();
    
    static const int NUM = 1000;
    
    // ポジション定義
    ofVec2f pos[NUM];
    
    //スピード定義
    ofVec2f speed[NUM];
    
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
    
    // 初期値セット
    for (int i=0; i<NUM; i++) {
        pos[i].x = ofRandom(0,ofGetWidth());
        pos[i].y = ofRandom(0,ofGetHeight());
        speed[i].x = ofRandom(-10, 10);
        speed[i].y = ofRandom(-10, 10);
    }

}

//--------------------------------------------------------------
void ofApp::update(){
    
    // updateで位置の更新などの計算
    for (int i=0; i<NUM; i++) {
        pos[i] += speed[i];
        
        if(pos[i].x > ofGetWidth() || pos[i].x < 0 ){
            speed[i].x = speed[i].x * -1;
        }
        
        if(pos[i].y > ofGetHeight() || pos[i].y < 0 ){
            speed[i].y = speed[i].y * -1;
        }
    }

}
//--------------------------------------------------------------
void ofApp::draw(){
    
    // 描画色指定
    ofSetColor(0,255,0,120);
    
    for (int i = 0; i<NUM; i++) {
        ofDrawCircle(pos[i].x, pos[i].y , 10);
    }
    
}

```






## 動的配列
最初から数を決めず、動的に要素数を増減できる配列
```
// 定義方法
vector <データ型> 配列の名前;

// 例
vector<int> vec{ 1, 2, 3 };
for (int i=0; i<vec.size(); i++) {
    cout << vec[i] << endl;
}

//動的配列の末尾に値を追加する
vec.push_back(追加する値);

//動的配列の末尾から値を削除する
vec.pop_back();

//動的配列の途中に値を追加する
vec.insert(イテレータ,値);

//動的配列の途中に値を削除する
vec.erase(vec.begin() + 2);

//動的配列の数を調べる
vec.size();

//参考リンク
Introduction to vectors
https://openframeworks.cc/ofBook/chapters/stl_vector.html
```



## 2次元配列

```

static const int ROW_NUM = 2;
static const int COL_NUM = 5;
    
int hueArray[ROW_NUM][COL_NUM] = {{10,20,30,40,50},{50,40,30,20,10}};

```
