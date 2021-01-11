# 3Dグラフィックスプログラミング

コンピュータグラフィックの3D表現は3次元の仮想空間を作り、
その中をカメラを通して2Dとして見ている。 
左右(x座標)と上下(y座標)に加えて(z座標)奥行きが加わる。



<img src="https://raw.githubusercontent.com/55Kaerukun/JavaScript/master/images/threeJS.png" width="600px">

## 3Dの基本図形 of3dPrimitive 

#### 立方体 

[ofBoxPrimitive](http://openframeworks.jp/documentation/3d/ofBoxPrimitive.html) 



```
//ofApp.h

ofBoxPrimitive box; //立方体のインスタンス

```

```
//ofApp.cpp
void ofApp::setup(){
    ofBackground(0);
    ofSetFrameRate(60);
}

void ofApp::draw(){
    //カメラを使わないと左上起点になるので中心座標をずらす
    ofTranslate(ofGetWidth()/2, ofGetHeight()/2,0);

    // boxPrimitiveの描画
    ofSetColor(255, 0, 0); //カラー
    box.set(200); //サイズ
    box.setPosition(0,0,0); //座標
    box.draw(); //描画
}

```

&nbsp;


#### 球体 `ofSpherePrimitive` 
[ofSpherePrimitive](http://openframeworks.jp/documentation/3d/ofSpherePrimitive.html) 

![](img/SphereGeometry.png)

&nbsp;


#### 平面 `ofPlanePrimitive` 

 [ofPlanePrimitive](http://openframeworks.jp/documentation/3d/ofPlanePrimitive.html) 
 
 ![](img/PlaneGeometry.png)

&nbsp;


Primitiveのメソッド

*  `set()` サイズ
*  `setPosition()` 座標
*  `draw()` 描画
*  `drawWireframe()` ワイヤーフレーム表示
*  `setResolution()`　分割数 

&nbsp;
&nbsp;



## 3Dオブジェクトを描画してみる
実際に3Dオブジェクトを描画してみましょう

![](images/3dprimitive.png)

ofApp.h

```

ofBoxPrimitive box;
ofSpherePrimitive sphere;

```

ofApp.cpp
```

// 座標を中心に
ofTranslate(ofGetWidth()/2, ofGetHeight()/2);

// 立方体
box.set(100); //幅、高さ、奥行き 100px
box.setPosition(0,0,0); // 位置指定
box.draw();

// 球体を描画
sphere.set(100,8); //半径100px、分割数8
sphere.setPosition(200, 0, 0);
//sphere.draw();
sphere.drawWireframe();

```




## カメラ
<img src="images/easycam.png" width="600px">

[ofEasyCam](http://openframeworks.jp/documentation/3d/ofEasyCam.html)

3D用の簡易カメラ。3Dでよく使われる中央起点に自動的に変わり、  
マウス操作で位置を変えることができる。（ofTranslateは無効に）

```

// カメラ開始
cam.begin();

// カメラ終了
cam.end();

// カメラの視野角 fov (Field of View) 視野角 60~90度が多い
cam.setFov(80.0f);

// カメラとの距離
cam.setDistance()

// カメラの位置
cam.setPosition()

// カメラが見る対象物を設定
cam.setTarget()

// 深度テスト DEPTH TEST
手前にあるものが奥にあるものを覆い隠すという現実世界の表現を 
シミュレートするために必要。 
無効のすると、新しく描画したオブジェクトがどんどん上書きされる。

ofEnableDepthTest()


```


```
//ofApp.h
ofEasyCam cam; // カメラ
ofBoxPrimitive box; // 立方体 
ofSpherePrimitive sphere; // 球体

```

```
//ofApp.cpp

void ofApp::setup(){
    ofSetFrameRate(60);
    ofBackground(0);
    ofEnableDepthTest(); //深度テストを有効に
    
    // カメラ設定
    cam.setFov(80.0f);
    cam.setPosition(0,0, +500);
}


void ofApp::draw(){

    cam.begin();
    
        // 立方体
        box.set(100); //幅、高さ、奥行き 100px
        box.setPosition(0,0,0); // 位置指定
        box.draw();
        
        // 球体を描画
        sphere.set(100,8); //半径100px、分割数8
        sphere.setPosition(200, 0, 0);
        //sphere.draw();
        sphere.drawWireframe();

    cam.end();
}
```


&nbsp;
&nbsp;

## ライト ofLight

ライトを追加して陰影をつけます。

<img src="images/light.png" width="600px">

[ofLight](http://openframeworks.jp/documentation/gl/ofLight.html)


![](https://openframeworks.cc/documentation/gl/Lights_PointSpot.jpg)

![](https://openframeworks.cc/documentation/gl/Lights_AmbientDirectional.jpg)



```
//ofApp.h

    ofEasyCam cam; // カメラ
    ofBoxPrimitive box; // 立方体
    ofSpherePrimitive sphere; // 球体
    ofLight light; // ライト
    

```

```
//ofApp.cpp

void ofApp::setup(){

    ofSetFrameRate(60);
    ofBackground(0);
    ofEnableDepthTest(); //深度テストを有効に
    
    // カメラ設定
    cam.setFov(80.0f);
    cam.setPosition(0,0, +500);
    
    // スポットライト設置
    light.setSpotlight();
    light.setPosition(0, 300, 500); //ライトの位置
    light.enable();
   
}


void ofApp::draw(){
    
    ofEnableDepthTest();
    
    cam.begin();
    
        // 立方体
        box.set(100); //幅、高さ、奥行き 100px
        box.setPosition(0,0,0); // 位置指定
        box.draw();
        
        // 球体を描画
        sphere.set(100,8); //半径100px、分割数8
        sphere.setPosition(200, 0, 0);
        //sphere.draw();
        sphere.drawWireframe();

    cam.end();
    
}



```

&nbsp;
&nbsp;


## マテリアル ofMaterial

[ofMaterial](http://openframeworks.jp/documentation/gl/ofMaterial.html)

マテリアルは物体の反射の色を表す

#### Ambient 環境光

`setAmbientColor()`

光源からの環境光が物体に当たって拡散されたときの色


#### Diffuse 拡散光

`setDiffuseColor()`

光源から放射された光が、物体に当たって拡散（乱反射）されるときの色


#### Specular 反射光

`setSpecularColor()`

光源から放射された光が、物体の表面で反射したときの色｡ 


#### Emissive 放射光

`setEmissiveColor()`

物体が自ら放射している光の色

&nbsp;


```
//ofApp.h

    ofBoxPrimitive box; //立方体
    ofEasyCam cam; //カメラ
    ofMaterial material;
    ofLight light; //ライト

```



```
//ofApp.cpp

void ofApp::setup(){
	ofBackground(0);
    ofSetFrameRate(60);
    
    // カメラ設定
    cam.setFov(80.0f);
    cam.setPosition(0,300,500);
    
    ofEnableDepthTest();
    light.enable();
    light.setPosition(0,100,0);
    
    material.setAmbientColor(ofColor(0,0,255)); //ベースの色
    material.setDiffuseColor(ofColor(0,255,0)); //光が当たる色
    material.setShininess(120); //鏡面反射程度
    material.setSpecularColor(ofColor(255,0,0));//鏡面反射の色
}

void ofApp::draw(){

    cam.begin();
	
    // boxPrimitiveの描画
    ofSetColor(255, 0, 0); //カラー
    box.set(200); //サイズ
    box.setPosition(100,0,0); //座標
    material.begin(); //マテリアル描画開始
    box.draw(); //描画
    material.end(); //マテリアル描画終了
	
    cam.end();
}
```

&nbsp;

## ヘルパー


#### XYZ軸
`ofDrawAxis(1000);`

#### XYZ回転
`ofDrawRotationAxes(200,1,60);`


#### グリッド（カスタム）

```
//ofApp.h
void gridHelper(int size, int step);
```

```
//ofApp.cpp
void ofApp::gridHelper(int size, int step){
    ofSetColor(0,20);
    for (int i=0; i<size; i+=step) {
        ofDrawLine(i-size/2, 0, size/2, i-size/2, 0, -size/2);
        ofDrawLine(-size/2, 0, i-size/2, size/2, 0, i-size/2);
    }
}
```