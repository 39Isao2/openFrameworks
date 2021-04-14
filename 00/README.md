# openFrameworksとは

公式サイト
http://openframeworks.cc/

Zachary Lieberman, Theo Watson, Arturo Castroを中心に開発されたフレームワーク。 <br>
Processingより後発でその影響を受けているが、<br>C++で開発するためより高速な処理ができる。<br><br>
スローガンは、**詩を書くようにコードを書け** （ポエティックコーディング）と<br>
**「DIY」（Do It Yourself）ではなく、「DIYO」（Do It With Others）みんなで作ろう。**<br><br>

グラフィックの描画の為のOpenGL、オーディオの入出力にはRtAudio、フォントの表示FreeTypeなど、様々なライブラリが
もともと用意されていて、表現に集中できるようになっている。また多くのアドオン(拡張機能)もある。<br><br>

**「糊（のり glue）」として例えられる。**

開発言語 : C++ 
開発環境 : Xcode visual studio

<img src="images/of.png" width="600px">

# 作品例

Canness Lions International Festival of Creativity 
真鍋大度、Perfume 

<img src="images/pufume.png" width="500px">

Faces 
Arturo Castro, Kyle McDonald

<img src="images/faces.jpg" width="500px">

その他

CREATIVE APPLICATIONS NETWORK – openFrameworks Tag 
https://www.creativeapplications.net/tag/openframeworks/

## セットアップ方法
１、こちらからダウンロード <br><br>
https://openframeworks.cc/ja/download/
<br><br>
<img src="images/daunload.png" width="600px">
<br><br>
２、ファイルをダウンロード後、解凍し、projectGeneratorをアプリケーションフォルダに移動します。<br><br>
<img src="images/setup_first.png" width="600px">
<br><br>
３、projectGeneratorを起動すると、このような画面が出ると思います。<br><br>
<img src="images/error.png" width="300px"><br><br>
４、虫眼鏡アイコンをクリックして、ルートパス(of_v0.11.2_osx_release フォルダ)の場所を指定し、<br>createボタンをクリックします。<br><br>
<img src="images/ptath_ok.png" width="300px"><br><br>
## プロジェクト設定方法
1、projectGeneratorを起動。
<br><br>
2、 「プロジェクト名」、「Addon(拡張機能)」、を設定したらパスをcreateボタンをクリックするとXcodeが立ち上がります。<br><br>
<img src="images/create.png" width="400px"><br><br>
※project path という欄は構造が崩れないように、基本的には「ルートパス/myApp」に指定してあげてください。
<br><br>

