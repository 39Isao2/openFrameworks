# 図形の描画
openFrameworksの基本図形です。<br>
Processing経験者の方は、関数名の頭にoFとつけると覚えやすいです。

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
線幅の設定  
ofSetLineWidth(4);
 
円の角の数(円を滑らかにする)
ofSetCircleResolution(64);

// 四角形をの起点を中心に 
ofSetRectMode(OF_RECTMODE_CENTER);

// 四角形の起点を左上に 
ofSetRectMode(OF_RECTMODE_CORNER);
 
```
