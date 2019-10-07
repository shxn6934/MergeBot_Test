# iOSDC2019

## 前夜祭
1. スクリーン配信 by FromAtomさん
- pixiv
- リジェクトお守り
- ライブ配信が流行なのでサービス化
- スクリーン配信　スマホでライブ配信ができる
- ReplayKit
	- スクリーンの収録やライブ配信ができるライブラリ
	- iOS9では、録画ができるが配信ができない
	- 11から本格的にできる
- Qiitaの記事は5件のみ
- 実機でのみのデバックが必須
- iOS9
	- 録画機能
- iOS10
	- Extention
	- Broadcast Upload Extentionを実装しているアプリ経由で配信
- iOS11
	- RPScreenRecoder
	- Broadcast Upload Extentionを経由しなくても配信できるようになった
	- ホームセンターでも配信か
- Broadcast Upload Extention
	- iOS10、11に対応
	- メモリは50MBまで
	- 越えるとKill
- SetupUI Extention
	- RPBroadcastActivityViewController
	- CMSampleBuffer
-SampleHandler.swift
- CMSampleBuffer
	- Sora iOS SDKがCMSampleBufferをVP8エンコードする際に越える

- サイズを超えないようにするには、、、
	- FPS・画質・メモリ消費
- 音声
	- マイク音声とアプリ音声
	- 何もしないとマイク音声は取得できないので、何かを書いてあげる必要がある。
- Extentionでデバック
	- printが表示されない、BreakPointで止まらない
	- Schmeで止める
- ReplayKitとH.264エンコードとの相性が悪い

2. Advanced Segue by tokorom さん
- Basic Segue
	- Segueとは
		- UIStoryBoardSegue
		- StoryBoardのみ △
		- 画面遷移のみ △
	- 種類
		- Standard Segue
			- 画面遷移（ViewControllerからViewControllerへ）
		- Embed Segue
			- ViewControllerから孫のViewControllerへ
		- UnWind Segue
			- 戻る（特定のViewControllerへ）
		- Custom Segue
			- なんでもあり
	- Segueを使うPros
		- StoryBoardで完結できる
		- 一元管理できる
		- Apple Wayを外れない
	- Segueの相性
		- Static TableViewとの相性
	- prepareForSegue
		- 一つのメソッドで完結
		- iOS13からviewDidApperが呼ばれない
	- Segueを使うCons
		- ViewControllerのinitializerを自分で呼べない
		- prepareForSegueが複雑になる
	- SegueAction(iOS13)
		- initializerをSegue Actionで設定しておくことで、非オプショナルの定数で渡すことができる。
		- これにより、prepareForSegueが簡単に
	- UnwindSegue
		- ノンコードでできる
		- 変更に強い
		- 共通画面からのUnwind
	- Custom Segue
		- segueをコードで設定
		
## day1
1. 縦書きエディタを6プラットフォームで開発してみて by 六々
- pixivコミックのiOS実装とAPI実装
- テキストエディタ開発
	- TATEditorという縦書きエディタ
	- iOS/Android
	- macOS/Windows/Ubuntu
	- UWP
- TATEditor
	- ルビが触れる
	- PDF出力
- なぜ開発？
	- 2009年に小説が好きで、小説を書いていたが、Unicodeでかける縦書きテキストができなかった。
- 縦書き
	- 小説、脚本・シナリオ、新聞など
	- アウトプットされる状態に近い見た目
	- ファイル形式
		- PDF
		- SVG
		- HTML
	- 書字方向
		- 横書き：右から左
		- 縦書き：上から下
	- 改行方向
		- 横書き：上から下
		- 縦書き：右から左
- 6プラットフォーム
	- デスクトップ：ライブラリ wxWidgets
		- macOS
		- Windows
		- Ubuntu
	- モバイル：そのまま
		- iOS
		- Android
		- UWP
	- 開発言語は、C++
	- wxWidgetsはクロスプラットフォームライブラリ
	- デスクトップは、C++
	- モバイルは、各言語
		- ただ、コストが高い
	- C++共通のライブラリを使用
	- GUI部分は、C++とモバイルは各言語
	- swiftからC++のライブラリを呼ぶためには、Objecrive-Cのライブラリを使用
	- ライブラリでテキストを縦書きに表示する
	- 各プラットフォームでテキストを編集
	- GUIで各プラットフォームのUIを作成
- テキストエディタ
	- swiftだと、UITextView
	- テキストエディタを再実装する
	- 人間やOS、アプリなどの様々な要因に影響を受ける
	- **表示と編集**
- 表示
	- 文字コードとフォントと画像
	- platform-independent
	- 表示 = 文字が書かれた画像が出る
	- UILabelやString.draw
	- テキストから画像にし、出力
	- テキストから画像にするには、画像がRGBAの配列なので全OSで表示できる。
	- UIImageをextentionする
	- 文字コード(Unicode)、フォント(OpenType)、グリフ
	- 縦書き用のグリフ、グリフの仕様などに応じて切り替える
- 編集
	- OSとIMEとUI
	- platform-specific
	- 文字列の選択、選択範囲を文字列で置換
	- 人間が打ったキーコードをIMEがテキストに変化
	- IMEとTextViewの関係
	- IMEとTextViewのやり取りは、IME APIを使用する
		- テキストの取得と変更
		- 選択範囲の取得
		- View上の位置情報
		- 未確定文字列
- デスクトップとモバイルで全然違う

2. クリーンコードアドベンチャー by shiz さん
- VISITS TEC 株式会社
- クリーンコード
	- Uncle Bob曰く、読みやすいコード
	- 書く時間 << 読む時間
	- それぞれに正解がある -> クリーンコード道場
- わかりやすい
- 安全である
- 変更に強い
- Kickstarter
	- 構造の統一
	- SingletonでのDI管理
	- 画面遷移の管理
- ジェネリック
	- 具体的なデータ型に直接依存しない
- protocol
	- Static
		コンパイル時
	- Dynamic
		- 実行時
- "Start With a Protocol"
- 個々の具体的な問題を解決 -> ジェネリックな解決策を抽出
- ジェネリックにしていくためには、protocolの使い方を理解しなければならない
- 価値体系

3. 画像処理における、	UIImageとCGImageとCIImageの効果的な使い分け by 栗山さん
- sansan iOS
- 名刺管理サービス
- Qiita Jobs
- リアルタイム画像処理
	- 画面上の名刺自動検出
	- バーションアップで検出率向上
- リアルタイム画像処理とは、
	- カメラからリアルタイムに渡ってくる画像を処理する
	- カメラから画像を取得 -> 前処理 -> 処理 -> 結果
- iOSにおける画像処理
	- カメラからの画像を取得
		- AVFoundation AVcaptureVideoDataOuyput
		- 画像は、CMSampleBuffer
		- これをCIImageまたはUIImageに変換
		- CMSampleBuffer -> CVImageBuffer -> CIImage
	- 画像認識への入力のための前処理
		- 処理はUIImage
		- 入力画像を縮小する必要あり
		- CIImage -> CGImage -> UIImage
	- 画像処理
		- ライブラリ：CIFilter
	- 表示
		- UIImageViewやMTKview
		- 認識は、UIBezierPathやCAShapeLayer
- リサイズ
	- UIImageへ変換
	- サイズを縮小
	- 基本はCIImageを使い回す.必要なところでUIImageへ
- CIImage(Core Image)
	- Core Imageに含まれる画像クラス
	- Coew Imageは、静止画の画像処理を行う
	- 特徴
		- 一度作成すると、情報の変更不可
		- 別スレッドから参照可能
		- 遅延実行
	- リサイズ方式は、3つ
- UIImage
	- PNGとJPEG
	-リサイズでnon-optional
- 処理速度：CIImage >> UIImage
- GPU(CIImage)を有効活用する
- 適切な処理速度方式を選ぶ

4. FatViewControllerを安全に書き換える方法が見つからなかったので、どういう痛みを許容するか by ダンボー田中さん
- BOOTH
- 自動テスト
	- テストを書いてからリファクタリングをする
	- 自動テストがある状態
		- コードを書き換えたら、壊れる可能性あり
		- 壊れないかの確認のテスト
		- 自動テストがあるため、安心して書き換えられる
	- デッドロック問題
		- 自動テストを入れるために設計を書き換える.
	- UITest
	- BDD
	- 一時的に手動テスト
	- テストに選定方法はコストや生存期間を鑑みる必要がある
	- シチュエーションによって方法を変える
- テスト戦略
	- 何をテストするのか？
		- サービスにとって最も重要なユーザー価値は？
			 - 責任者との意識との共有
	- ポストポーテム
	
5. LT
- XCTestのつまづき
	- テストコード、アプリ自体のバグ	かわからない
- LLDB
	- 次世代型のデバック
	- po,p,v
	- po,p 式を評価
- CoreML + AR
	- 平面検出 -> 識別 -> 測定結果
	- Core MLでサーバーレスに！！

##day2
1. テストケースで Ambiguous Layout を発見する
- メルカリのiOS Architecture
- autolayoutのデバックがめんどくさい、表示が遅くなる
- hasAmbigunosLayout
- XCTAssertAutoLayout
	- x64 trampolines
- AutoLayoutをテストするには、C言語をHookする必要があり。

2. モバイル決済アプリの作り方 
- 社会的背景
	- キャッシュレスビジョン
	- 協議会や事業が立ち上がり、キャッシュレス事業が加速
- Cash-In
	- 銀行口座やコンビニATM、フリマからチャージ
- Cash-Out
	- ApplePay
	- コード決済
	- ネット決済
- 資金決済法
- 犯罪収益移転防止法により、本人確認(KYC)が必要
- 郵便によるKYC
- 銀行口座接続によるKYC
- **eKYC**
	- カメラを使用したオンラインでのKYC
- Apple Pay
	- セキュアなクレジットベースの決済方法
	- カード登録フローで生のカード番号を別の番号に変化している
		- 決済する際に銀行にわたるまでは、生の番語を使用しない
	- Apple Pay In-App Provisioning
- コード決済
	- CPM(利用者提示型)とMPM(店舗表示型)
	- コード決済の仕組みは、各社独自実装であるため非公開
	- CPM
		- 何Payを使って、誰が入っているのかという情報
	- MPM
		- お店のどこに置いているかの情報
- メルカリは、機能ごとにFrameworkを分割
- Sandboxを用いた開発
- モバイル決済は、実機が不可欠
	- DIを使用してシミュレーターでビルドできるようにする。

3. iPhoneのカメラで写真撮影から現像までの技術を紐解く
- エウレカ
- カメラの技術
- カメラを撮る = 適切に光を操る
- カメラ・オブスクラム
	- 光の量が少ないため、暗い -> レンズ
		-  色収差
		- 単色収差
		- 凸レンズを凹レンズ
- Imageing Lens System = iPhoneのカメラ
- 集めた光をデータに
	- イメージセンサー
	- 光電効果により、光を電荷に変換 = データか
	- サイズと画素
- サイズ
	- サイズが大きいと 1pxに対するフォトダイオードが大きくなる -> 多く配置可能
	- 小さいとコンパクトに
- 画素
	- フォトダイオード1つ1つが電荷に変化
	- 電荷の大きさ = 1pz毎の光の量
	- ただ、画素数が大きと高画質になるわけではない
- 光を操るための値
- シャッタースピード
	- 早いと動体がブレないが、暗い
	- 遅いと動体がぶれる
- F値
	- 小さいと光の量が多い
	- 大きいと光が少ない
	- 絞りと被写界深度
- ISO感度
	- 高いと暗くても明るい写真が撮れる　ただ、ノイズが目立つ
- 関係性
	- バケツと蛇口に例えられる
	- バケツ(ISO感度)、蛇口の大きさ(F値)、開ける時間(SS)
- AVCaptureDevice
- AVCaptureDeviceInput
- AVCaptureSession
- AVCaptureOutput
- AVFoundationと仕組みは変わらない

4. すべての人のためのアクセシビリティ対応
- アクセシビリティ
	- 情報やサービスへのアクセスのしやすさ
	- 障害者だけでなく全ての人対応
	- ユーザビリティは、使いやすさを重点
- ある程度は、自動
- アクセシビリティの恩恵を理解していないから、優先順位が低い
- ズーム機能
- Assistive Touch
- 色反転
- タップ領域
	- 44 x 44 pt 以上
	- 要素を密集させない
- 文字の画像かは避ける
- スタイルの一貫性
- 強い光の点滅も避ける
- Accessibility Inspector
- やるべきこと
	- Text Style
	- adjustsFontForContentSiECategory
	- 文字だけでなく画像も対応させる
- 見え方
	- ColorTester