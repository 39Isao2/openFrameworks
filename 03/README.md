# 動的配列
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

## サンプルコード : クリックする度に円が飛び散る
ofApp.h
```
#pragma once

#include "ofMain.h"

class ofApp : public ofBaseApp{

    public:
        void setup();
        void update();
        void draw();
        void mousePressed(int x, int y, int button);
        void mouseDragged(int x, int y, int button);
    
    
    //座標とスピードの動的配列
    vector <glm::vec2> pos;
    vector <glm::vec2> speed;
    
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
    
    for(int i=0; i<pos.size(); i++){
        pos[i] += speed[i];
    }

}
//--------------------------------------------------------------
void ofApp::draw(){
    
    for(int i=0; i<pos.size(); i++){
        ofSetColor(255);
        ofDrawCircle(pos[i].x, pos[i].y, 2);
    }
    
}
//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button){
    //クリックした座標を保存する変数
    glm::vec2 clickPos;
    clickPos.x = x;
    clickPos.y = y;

    //動的配列posにクリック座標を保存
    pos.push_back(clickPos);

    // cout<< clickPos <<endl; //クリック座標をプリント

    //ランダムなスピードを生成
    glm::vec2 randomSpeed;
    randomSpeed.x = ofRandom(-5,5);
    randomSpeed.y = ofRandom(-5,5);

    //動的配列speedにランダムな速度を保存
    speed.push_back(randomSpeed);
    
}

//--------------------------------------------------------------
void ofApp::mouseDragged(int x, int y, int button){

    // こっちに移動するとパーティクルが出現し続ける
}

```



### ofCurveVertexで線を引くver

<img src="https://github.com/55Kaerukun/openFrameworks/blob/main/03/img/vertaxLine.png" width="500px">


```
void ofApp::draw(){
    
    ofNoFill();
    ofSetLineWidth(5);
    ofBeginShape();
    for(int i=0; i<pos.size(); i++){
        ofSetColor(255,120);
        //ofDrawCircle(pos[i].x, pos[i].y, 2);
        ofCurveVertex(pos[i].x, pos[i].y);
    }
    ofEndShape(); 
}


// 画面をクリア
void ofApp::keyPressed(int key){
    if(key == 'c'){
        pos.clear();
        speed.clear();
    }
}


```
