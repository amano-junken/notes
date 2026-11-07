# **hokurenAA**
## ホクレン 基幹システム再構築 コア開発用プロジェクト
### フォルダ構成
[google](https://google.com) <br>
[Google](https://www.google.com) <br>
![img](logo.png)


|フォルダ|説明|
|---|---|
|hokurenACA|ユーザ情報管理(オンライン)|
|hokurenACA_BAT|ユーザ情報管理(バッチ)|
|hokurenACAlib|ユーザ情報管理jarライブラリ(ビルド専用。ソースはACAを更新のこと)|
|hokurenADA|メニュー管理(オンライン)|
|hokurenADA_BAT|メニュー管理(バッチ)|
|hokurenADAlib|メニュー管理jarライブラリ(ビルド専用。ソースはADAを更新のこと)|
|hokurenAGA|開閉局管理(オンライン)|
|hokurenAGA_BAT|開閉局管理(バッチ)|
|hokurenAGAlib|開閉局管理jarライブラリ(ビルド専用。ソースはAGAを更新のこと)|
|hokurenAHA|異常終了管理(オンライン)|
|hokurenAHA_BAT|異常終了管理(バッチ)|
|hokurenAHAlib|異常終了管理jarライブラリ(ビルド専用。ソースはAHAを更新のこと)|
|hokurenAJA|ワークフロー管理(オンライン)|
|hokurenAJA_BAT|ワークフロー管理(バッチ)|
|hokurenAJAlib|ワークフロー管理jarライブラリ(ビルド専用。ソースはAJAを更新のこと)|
|hokurenAQA|共通マスタ管理(オンライン)|
|hokurenAQA_BAT|共通マスタ管理(バッチ)|
|hokurenAQAlib|共通マスタ管理jarライブラリ(ビルド専用。ソースはAQAを更新のこと)|
|hokurenAWA|Web共通(オンライン)|
|hokurenAWA_BAT|AWA業務バッチjar。AZA_BATとAWAlibを組み込み|
|hokurenAWAlib|Web共通jarライブラリ(ビルド専用。ソースはAWAを更新のこと)|
|hokurenAZA|Web共通F/W(ビルド対象外：製造時はAWA内のものを使用)|
|hokurenAZAforBAT|バッチ用AZA.jar(ビルド対象外)|
|hokurenAZA_BAT|バッチ起動jar。業務バッチはこれを組み込む|

### プロジェクトの配置について

- このプロジェクトは次のフォルダに配置される想定で設定されている。

c:\hokuren2\workspaces\hokurenAWA\Root
>\\\\10.50.10.85\\kikan_disk02\\21_(AW)Web共通S\\60_製造\\01_開発環境（コア）\\開発環境構築手順(コア).xlsx<br>

を参照のこと

[環境手順](//10.50.10.85/kikan_disk02/21_(AW)Web共通S/60_製造/01_開発環境（コア）/開発環境構築手順(コア)%20Ver1.10.xlsx)

### .projectの更新検知を外す手順

.projectファイルの更新をコミット対象から外すために、ローカルにクローン後、Rootの直下でコマンドプロンプトから次のコマンドを実行しておく。
（最初に1度でよいが、プロジェクトフォルダが増えた場合は再実行しておく）

>gitskip

### ブランチ

1. main<br>
(本番用予約：現在は未使用)

2. develop<br>
当面のマスターブランチ。マージリクエストはこのブランチに対してマージする。

3. developXXX<br>
各チーム(XXX=運用管理コード or HC/CSC/CC等)確認用ブランチ。<br>
使用するしないも含め、運用方法はチームで判断してよい。<br>
想定はここにチーム内で各自のマージを集めて動作確認後、developにメンテナがマージしていく。<br>
<strong>※チーム間のソースの乖離を防ぐためこのブランチにコミットをため込まず、すみやかにdevelopにマージしていくこと。</strong>

### 各自のブランチ

作業時は、各自ローカルでブランチを作成し、コミット＆プッシュ後、マージリクエストする。
マージ担当は、各チームでメンテナをアサインする。

ブランチ名ルール

<運用管理コード>-<ユーザ名>-<任意のラベル>

例<br>
>ada-hanamura-20250602 (日付)<br>
>ada-hanamura-adad202 (Lvl3のid)<br>
>ada-hanamura-issue#12 (イシュー#12の対応)<br>

マージリクエストでは基本的に元のブランチは削除するようにする。<br>
リモートに放置されたブランチは定期的(1週間を目途)にチェックして削除する。

### マージ時の注意点(＝メンテナが承認時の注意点)

1. かならず、リクエストされたブランチで手元でビルドしてエラーが無いことを確認する。<br>
エラーがある場合は、差し戻す。

2. 可能であればサーバ起動してエラーが出ないところまで確認する。

3. 共通部(Root直下のファイル群、hokurenAWA内)の変更は、よく確認する。

### バッチのビルドと実行

1. Root直下でgradleでbuild後、プロジェクトフォルダにcdして、batchコマンドにjobidを指定して実行する。

>cd \hokuren2<br>
>env<br>
>cd workspaces\hokurenAWA\Root<br>
>build<br>
>cd hokurenADA_BAT<br>
>batch ADAA302_DeleteMyMenuJob<br>

2. eclipse上では、プロジェクトフォルダ直下のlaunchフォルダ内の各*.launchファイルを実行する。

3. うまく動かないときは、hokurenXXX_BATフォルダ内の、build\libsフォルダを空にしてやり直す。

### spotbugsレポートの作成

1. Root直下で次のコマンドを実行する

>spotbugs<br>

2. 実行後、各プロジェクトフォルダの

```
<プロジェクトID>/build/reports/spotbugs/main.html
```
にspotbugsの解析レポートが出力されるので、ブラウザで確認する。


