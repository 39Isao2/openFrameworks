# ポインタとアドレス
ポインタとは、変数のアドレスを記憶する変数のことです。<br>
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
- ポインタ変数はアドレスを保存する変数
- ポインタ変数の宣言は型の後ろに* をつける int* pNum
- 変数のアドレスを知るには &をつける &num
- ポインタ変数から値を取るには変数名の前に*をつける *pNum　間接参照演算子


## クラスでポインタを使って高速化




```
クラス名* 変数で宣言
&で渡して、*で受け取る
*がきたら->でget！

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
SineCircle::SineCircle(ofVec2f* pPos){
    // *がきたので->でゲット！
    pos.x = pPos->x;
    pos.y = pPos->y;
}
------------------------------------
SineCircle* sc
*で作った変数は
sc->update();
sr->draw();
みたいに->で使う。
```
