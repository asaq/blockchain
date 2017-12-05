---

copyright:
  years: 2017
lastupdated: "2017-07-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.blockchain}}・ネットワークのモニタリング

このチュートリアルでは、{{site.data.keyword.Bluemix_short}} で{{site.data.keyword.blockchain}}・ネットワークの状況情報を表示し、モニターする方法を示します。{:shortdesc}

ネットワーク・モニターを開始し、「チャネル」画面で表示してモニターするチャネルを見つけます。特定のチャネル画面にある 3 つのタブで、このチャネルのデータ状況情報、メンバー、インスタンス化されたチェーンコードを表示できます。

* **チャネルの概要 (Channel Overview)**  
「チャネルの概要 (Channel Overview)」タブには、このチャネルに関する以下のブロック情報が示されます。
    * 作成されたブロックの総数、最後のトランザクション以降の時間、チェーンコードのインスタンス化の数、チェーンコードの呼び出しの数を含む、一連のデータ・ポイント。
    * このチャネルにあるすべてのブロックをリストした表。ブロックを展開して、そのブロックの詳細情報を表示できます。  

  ![チャネルの概要](../images/channel_overview_detail.png "チャネルの概要")  

* **メンバー**  
「メンバー」タブには、組織のオペレーターの E メール・アドレスなど、このチャネルのメンバーに関する情報が示されます。![チャネル・メンバー](../images/channel_members.png "チャネル・メンバー")  
  
* **チェーンコード**  
「チェーンコード」タブには、このチャネルでインスタンス化されたすべてのチェーンコードがリストされ、チェーンコード ID、バージョン、チェーンコードを実行しているピアの数が示されます。   
    
  チェーンコードの行を展開すると、そのチェーンコードの詳細情報が得られます。  
    * **「JSON」**をクリックすると、チェーンコードの JSON ファイルを表示できます。
    * **「ログ」**をクリックすると、チェーンコードのログを表示できます。
    * **「削除」**をクリックすると、実行中のチェーンコード・コンテナーを削除できます。
  
  ![チャネル・チェーンコード](../images/channel_chaincode.png "チャネル・チェーンコード") 
  