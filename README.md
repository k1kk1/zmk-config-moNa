# moNa 詳細説明

## 目次
  - [1. moNaについて](#1-monaについて)
    - [1-1. 性能紹介](#1-1-性能紹介)
    - [1-2. バージョン説明](#1-2-バージョン説明)
  - [2. 商品内容](#2-商品内容)
    - [2-1. 内容詳細](#2-1-内容詳細)
    - [2-2. その他おすすめ購入品](#2-2-その他おすすめの購入品)
  - [3. 動作確認](#3-動作確認)
  - [4. ファームウェア編集](#4-ファームウェアについて)
    - [-1. キーマップの編集](#4-1-キーマップの編集)
    - [4-2. ファームウェアの書き込み方法](#4-2ファームウェアの書き込み方法)

## 1. moNaについて

moNaはkumakeyさんが制作したroBaを参考にしてできた分割型キーボードです。

### 1-1. 性能紹介

* ロープロファイル
* 完全ワイヤレス
* 17mmキーピッチ
* ロータリーエンコーダつき
* 43キー
> [!NOTE]
> ロープロファイルエンコーダを採用しているためスイッチ機能はついていません

### 1-2. バージョン説明

#### moNa - 左手トラックボール版
#### moNa2 - 右手トラックボール版

## 2. 商品詳細


### 2-1. 商品内容

写真

* キーボード本体(左右)
> [!NOTE]
> すべて組み立て済みのため、工具等の準備は必要ありません。

### 2-2. 購入おすすめ品

> [!WARNING]
> この商品には含まれていません

1. マグネットコネクタ
> usb-cにマグネットコネクタを使うことで取り回しの良さが向上します
2. ポロンシート
> ケースとPCBとの間に敷くことで打鍵感の向上が予想されます

## 3. 動作確認
1. それぞれのマイコンのリセットボタンを1回押します。
2. PCでbluetoothデバイスとして「moNa」を選択します。

bluetooth接続が完了したらすべてのキーが認識するか、ロータリーエンコーダ、トラックボールが問題なく動作するか確認してください。
左右間のペアリングは電源を入れると自動的に行われます。
有線接続でも動作しますが、左右間は無線接続のみになります。
ロータリーエンコーダ側はPCに有線接続してもキーボードとして動作しません。

## 4. ファームウェアについて

### 4-1. キーマップの編集

冒頭で書いたようにzmk firmwareの編集にはgithubのアカウントが必要です。  
一からファームウェアを用意する際の手順は[公式ドキュメントの導入解説](https://zmk.dev/docs/user-setup)を見るとわかりやすいです。  
以下では、私が作成したリポジトリをフォークし、[KeymapEditor](https://nickcoutsos.github.io/keymap-editor/)を用いてGUIでキーマップを書き換える手順を紹介します。  

1. githubアカウントを作成し、ログインします。
2. [このリポジトリ](https://github.com/sayu-hub/zmk-config-moNa)にアクセス
3. 画面右上の「Fork」をクリック
![](img/fork.jpg)
4. そのまま「Create fork」をクリック
![](img/createfork.jpg)
5. フォークしたリポジトリの「Actions」タブに移動し、「I understand my workflows, go ahead and enable them」をクリックし、github Actionsを有効化
![](img/enableActions.jpg)
6. [KeymapEditor](https://nickcoutsos.github.io/keymap-editor/)にアクセス  
7. 「GitHub」を選択
![](img/keymapeditor1.jpg)  
8. 「Login with GitHub」からでログインし、「Authorize Keymap Editor」を選択  
9. 指示に従い、フォークしたzmk-config-moNaにKeymap Editorがアクセスできるように進める
10. Keymap Editor上でキーマップが表示されたら、好きにキーマップを編集する
11. 画面左上の「Save」を押すと、編集したキーマップが適用されてGitHub Actionsが走り、自動的にビルドが開始します
![](img/keymapeditor2.jpg)
12. 「Save」の隣に表示される「Latest」をクリックするとGitHubに移動し、ビルドが完了するとファームウェアがダウンロードできるようになります。  
（ビルドには2～4分かかる場合があります。）
13. [書込み手順](#4-2ファームウェアの書き込み方法)に従い、ファームウェアを書き込みます。  
    + キーマップの編集のみの場合はトラックボール側(セントラル)のみを書き換えることで変更が適用されます。  
    リセットファームウェアの書込みも基本的には必要ありません。
    + KeymapEditorを用いずにmoNa.keymap以外のファイルの内容を書き換えた場合は、左右のファームウェアを書き換えてください。  
    + ファームウェアを書き直した際は、PC側のペアリング情報も削除してから再度ペアリングを行ってください。
14. 無事に変更したキーマップが適用されていれば成功です。

### 4-2.ファームウェアの書き込み方法

1. PCと左側のマイコンをUSBで接続します。はじめはキーボードの電源はオフで大丈夫です。
2. マイコンのリセットボタンを2回押すと、「XIAO SENSE」という名前でUSBドライブとして認識されるかと思います。(ブートローダの起動)
3. 「XIAO SENSE」ドライブにsettings_reset-seeeduino_xiao_ble-zmk.uf2をドラッグアンドドロップします。  
4. 書込み完了すると、「XIAO SENSE」というドライブは消えますが、再度セットボタンを2回押し、ブートローダを起動します。  
5. 「XIAO SENSE」ドライブにroBa_L-seeeduino_xiao_ble-zmk.uf2をドラッグアンドドロップします。  
6. 右側も同様の手順でsettings_reset-seeeduino_xiao_ble-zmk.uf2とroBa_R-seeeduino_xiao_ble-zmk.uf2を順番に書き込みます。
7. 両方の書込みが完了したら、電源を入れ、それぞれのマイコンのリセットボタンを**1回**押します。
8. PCでbluetoothデバイスとして「moNa」が認識され接続できればOKです。  



## 自作キーボードに興味のある方
[Zenn]()
知識ゼロの自分がこのキーボードを完成させるまでの道のりを書いています。
自分だけの自作キーボードを作りたい！と思っている人、目を通してみてください！

> [!WARNING]
> 現在作成中です。