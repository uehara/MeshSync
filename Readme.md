![demo](https://user-images.githubusercontent.com/1488611/39971828-98afa1d8-573d-11e8-9a6f-86263bee8949.gif)
# MeshSync
[English](https://translate.google.com/translate?sl=ja&tl=en&u=https://github.com/unity3d-jp/MeshSync)

DCC ツール上のモデルの編集をリアルタイムに Unity に反映させるツールです。ゲーム上でどう見えるかをその場で確認しながらモデリングすることを可能にします。  
Unity と DCC ツール両方のプラグインとして機能し、現在 [Maya](https://www.autodesk.eu/products/maya/overview), [Blender](https://blenderartists.org/), [メタセコイア](http://www.metaseq.net/), [xismo](http://mqdl.jpn.org/) をサポートしています。


## 使い方

**プラグイン本体は [releases](https://github.com/unity3d-jp/MeshSync/releases) からダウンロードしてください。**

<img align="right" src="https://user-images.githubusercontent.com/1488611/39971860-7f6d1330-573e-11e8-9a1e-9d95709cbd50.png" height=400>

### Maya
- Maya 2016.5, 2017, 2018 + Windows, Mac, Linux (CentOS 7) で動作を確認しています。
- インストールするには、プラグインを Maya の module path が通っているディレクトリにコピーします。
  - Windows: %MAYA_APP_DIR% が設定されている場合はそこに、ない場合は %USERPROFILE%\Documents\maya (←を Explorer のアドレスバーへコピペで直行) に modules ディレクトリをそのままコピー。
  - Mac: /Users/Shared/Autodesk/modules/maya に UnityMeshSync ディレクトリと .mod ファイルをコピー。
  - Linux: ~/maya に modules ディレクトリをそのままコピー。
- Maya を起動し、Windows -> Settings/Preferences -> Plug-in Manager を開き、MeshSyncClient の Loaded にチェックを入れてプラグインを有効化します。
- UnityMeshSync シェルフが追加されているので、それの歯車アイコンで設定メニューを開きます。
- "Auto Sync" がチェックされている間は編集が自動的に Unity 側に反映されます。Auyo Sync が無効でも "Manual Sync" ボタンを押すことで手動で反映できます。
- Animations の Sync を押すと、開始フレームから終了フレームまで時間を進めつつアニメーションをベイクして Unity に送ります

&nbsp;  

- 歯車アイコン以外のボタンはそれぞれ手動同期、アニメーション同期相当のボタンになっています
- ポリゴンメッシュ、カメラ、ライトの同期に対応しています
- ポリゴンメッシュはスキニング/ボーンと BlendShape もそのまま Unity へ持ってこれるようになっています
- 負のスケールは対応していません
- NURBS などポリゴン以外の形状データは対応していません

<img align="right" src="https://user-images.githubusercontent.com/1488611/39971861-81043192-573e-11e8-9945-2bb248d869bd.png" height=400>

### Blender
- Blender 2.79 系 + Windows, Mac, Linux (CentOS 7) で動作を確認しています。
- インストールするには、File -> User Preferences -> Add-ons を開き、画面下部の "Install Add-on from file" を押し、プラグインの zip アーカイブを指定します。
- "Import-Export: Unity Mesh Sync" が追加されるので、チェックを入れて有効化します。
- MeshSync パネルが追加されるので、そちらから設定や手動の同期を行います。
- "Auto Sync" がチェックされている間は編集が自動的に Unity 側に反映されます。Auyo Sync が無効でも "Manual Sync" ボタンを押すことで手動で反映できます。
- Animations の Sync を押すと、開始フレームから終了フレームまで時間を進めつつアニメーションをベイクして Unity に送ります。

&nbsp;  

- ポリゴンメッシュ、カメラ、ライトの同期に対応しています。
- ポリゴンメッシュはスキニング/ボーンと BlendShape もそのまま Unity へ持ってこれるようになっています。
- 制限はあるものの Mirror デフォーマも対応しています。
- 負のスケールは対応していません。
- NURBS などポリゴン以外の形状データは対応していません。
- Armature, BlendShape, Mirror 以外のデフォーマは対応していません。

### メタセコイア
- Windows 版 3 系と 4 系 (32bit & 64bit)、Mac 版 (4 系のみ) に対応しています。3 系はたぶん全てのバージョンに対応していますが、4 系は 4.6.4 以上である必要があります。(このバージョン以上でないとボーンの出力がサポートできないため)
- インストールするには、Help -> About Plug-ins を開き、ダイアログ左下の "Install" からプラグインファイルを指定します。ちなみにプラグインのタイプは Station です。
- インストール後 パネル -> Unity Mesh Sync が追加されるのでこれを開き、"Auto Sync" をチェックします。
- "Auto Sync" がチェックされている間は編集が自動的に Unity 側に反映されます。Auyo Sync が無効でも "Manual Sync" ボタンを押すことで手動で反映できます。
- "Import Unity Scene" を押すと現在 Unity で開かれているシーンをインポートすることができます。インポートしたシーンの編集もリアルタイムに反映可能です。

&nbsp;  

- ミラーリング、スムーシングは Unity にも反映されます。
  - ただし、ミラーリングの "左右を接続した鏡面" は非サポートです。
- メタセコイアで非表示のオブジェクトは Unity でも非表示になります。非表示のオブジェクトはメッシュの内容は送られないので、シーン内にオブジェクトが増えて同期が重くなってきた場合適切に非表示にすることで同期も速くなるはずです。
- マテリアルは Unity には反映されませんが、マテリアル ID に応じて適切にサブメッシュに分割されます。
- サブディビジョンやメタボールはフリーズするまで Unity には反映されません。
- メタセコイア 4 系でサポートされた法線の編集は "Sync Normals" にチェックを入れることで反映できます。
- メタセコイア 4 系でサポートされたボーンは "Sync Bones" にチェックを入れることで反映できます。 "Sync Poses" にチェックを入れると "スキニング" で設定したポーズも反映します。

### xismo
- xismo はプラグインの仕組みを提供していないため (2018/05 現在)、使い方が特殊であったり、 xismo のバージョンアップで動作しなくなる可能性が高いことにご注意ください。現行版は xismo 191～199 で動作を確認済しています。
- [UnityMeshSync_xismo_Windows.zip](https://github.com/unity3d-jp/MeshSync/releases) を解凍し、出てくる 2 つのファイル (MeshSyncClientXismo.exe, MeshSyncClientXismoHook.dll) を xismo がインストールされているディレクトリ (xismo.exe と同じディレクトリ) に置きます。
- MeshSyncClientXismo.exe を起動します。これにより MeshSync が付与された状態で xismo が起動します。
- ウィンドウ -> Unity Mesh Sync メニューが追加されており、これで各種設定などを行います。
- "Auto Sync" をチェックすると編集が自動的に Unity 側に反映されるようになります。

&nbsp;  

- xismo のビューポートに表示されているモデルをそのまま送っているため、モデルは大体同期できるはずです。
- モデル以外 (オブジェクト/マテリアルの名前、ボーンなど) は未対応です。これらは xismo 側がプラグイン API を用意しない限り対応が困難であり、現状対応予定はありません。


### Unity
- Unity 2017.1 系以上 + Windows (64 bit), Mac, Linux (CentOS 7) で動作を確認しています
- [MeshSync.unitypackage](https://github.com/unity3d-jp/MeshSync/releases) をプロジェクトにインポートします。
- メニュー GameObject -> MeshSync -> Create Server でサーバーオブジェクトを作成します。
- このサーバーオブジェクトが同期処理を担当します。これがシーン内になければ同期できません。

<img align="right" src="https://user-images.githubusercontent.com/1488611/39972178-45cf48d6-5744-11e8-8722-11fd412c7abd.png">

- マテリアルリスト
  - MesySyncServer はマテリアルのリストを保持しています。このリストにマテリアルを設定すると、対応するオブジェクトに適切にアサインされます。


- アセット化
  - DCC ツール側の編集によって生成された Mesh 郡は、そのままではそのシーン内にしか存在できないオブジェクトです。他のシーンやプロジェクトへ持ち出せるようにするにはアセットファイルとして保存する必要があります。
  MeshSyncServer の "Export Mesh" ボタンを押すとそのアセット化が行われます。("Asset Export Path" で指定されたディレクトリにファイルが生成されます)  


- ライトマップ UV
  - Unity でライトマップを使う場合、UV は通常のとは別の専用のものが用いられます。通常はモデルインポート時に自動的に生成されますが、本プラグインで DCC ツールから受信したモデルにはそれがありません。
  MesySyncServer の "Generate Lightmap UV" ボタンを押すとそのライトマップ用 UV を生成します。この処理は結構時間がかかるのでご注意ください。


- ランタイム対応
  - 本プラグインはその性質上エディタでのみの使用を想定していますが、一応ランタイムでも動作するようにしてあります。**意図せず最終ビルドに残さないようご注意ください**。



## Tips や注意事項など
- 同期は TCP/IP を介して行われるため、Unity と DCC ツールが別のマシンで動いていても同期させることができます。その場合、クライアントである DCC ツール側は設定項目の Server / Port に Unity 側のマシンを指定してください。


- Unity 上に MeshSyncServer オブジェクトがあるときにサーバーのアドレス:ポートをブラウザで開くと、サーバー側の Unity の GameView をブラウザで見ることができます。 (デフォルトでは [127.0.0.1:8080](http://127.0.0.1:8080))  
  このブラウザの画面のメッセージフォームからメッセージを送ると、Unity の Console にそのメッセージが出るようになっています。Unity 側作業者と DCC 側作業者が別の場合役に立つこともあるかもしれません。


- ポーズ/アニメーションのみを編集中の場合、"Sync Meshes" を切っておくことをおすすめします。メッシュデータを送らなくなるので動作が軽快になるでしょう。
  - プラグイン側でボーンのみの編集の場合メッシュは送らないようにすべきなのですが、判定がやや難しく、現状そうなっていません。


- Unity の頂点あたりの最大影響ボーン数が 4 であることに注意が必要です。
  これが原因でボーンが多いと DCC 側と Unity 側で結果が一致しなくなることがあります。


##  関連  
- [NormalPainter](https://github.com/unity3d-jp/NormalPainter): Unity 上で法線を編集できるようにするツール
- [BlendShapeBuilder](https://github.com/unity3d-jp/BlendShapeBuilder): Unity 上で BlendShape を構築できるようにするツール

## ライセンス
[MIT](LICENSE.txt), ただし Blender プラグインは [GPL3](Plugin/MeshSyncClientBlender/LICENSE.txt) (Blender のソースの一部を使っているため)
