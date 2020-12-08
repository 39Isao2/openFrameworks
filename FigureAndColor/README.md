# 図形の描画
openFrameworksの基本図形です。<br>
Processing経験者の方は、頭にoFとつけると覚えやすいです。

## 基本図形

```

線
ofDrawLine(50,50,100,100);


四角形
ofDrawRectangle(100, 100, 100, 50);

四角形を中心起点 ofSetRectMode(OF_RECTMODE_CENTER);
四角形を左上起点 ofSetRectMode(OF_RECTMODE_CORNER);
 

正円
ofDrawCircle(100, 100, 250);

楕円
ofDrawEllipse(100, 100, 50, 100);

三角形
ofDrawTriangle(100, 100, 150, 150, 50, 150);


パスで図形を描画

ofBeginShape();
    //ここに(x,y)のポイントを追加
    ofVertex(50, 120); 
    ofVertex(100, 90); 
    ofVertex(110, 60); 
    ofVertex(80, 20); 
    ofVertex(210, 60); 
    ofVertex(160, 80); 
    ofVertex(200, 90); 
    ofVertex(140, 100); 
    ofVertex(130, 120); 
ofEndShape(); //パスを閉じる

頂点
ofVertex(100,100);

曲線
ofCurveVertex(100,100);

```

### 基本図形のオプション
```
線幅の設定  
ofSetLineWidth(4);
 
円の角の数(円を滑らかにする)
ofSetCircleResolution(64);
 
```
