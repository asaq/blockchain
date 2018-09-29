---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# スターター・プランからエンタープライズ・プランへのマイグレーション
{: #migrate_starter_to_enterprise}


***[このページは参考になりましたか。 ご意見をお聞かせください。](https://www.surveygizmo.com/s3/4501493/IBM-Blockchain-Documentation)***


{{site.data.keyword.blockchainfull}} Platform の[スターター・プラン](../starter_plan.html)は、PoC やデモを実行したり、チェーンコードやアプリケーションを試用したりするためのテスト/開発環境を提供します。実稼働環境に移行する準備ができたら、スターター・プラン・ネットワークから[エンタープライズ・プラン](../enterprise_plan.html)・ネットワークにマイグレーションすることができます。
{:shortdesc}

エンタープライズ・プラン・ネットワークは、実稼働環境に対応した以下の機能を提供して、実動ワークロードをサポートします。

- ブロックチェーン・ネットワークを使用できるグローバルなロケーションが、スターター・プラン・ネットワークより多い。
- ストレージ制限なし (スターター・プランでは 20 GB)。
- すべてのネットワークを円滑に実行できるように強化された CPU と RAM の管理。
- 次の機能を含むセキュリティーの強化。
  - Secure Service Container (SSC) により、ブロックチェーン・イメージの改ざんとロードを常に防止し、アプライアンスの転送中および保存中のコードやデータを保護。
  - [ハードウェア・セキュア・モジュール (HSM)](../glossary.html#hsm) による鍵管理と鍵保管。
  - 全方位型ディスク暗号化。
- 高可用性、災害復旧、異常終了時耐障害機能、ローリング・アップグレード。
- オプションの拡張サポート。

## 考慮事項
{: #migrate_starter_to_enterprise_considerations}

スターター・プラン・ネットワークからエンタープライズ・プラン・ネットワークにマイグレーションする前に、以下の考慮事項を確認してください。

- **料金:** 組織でエンタープライズ・プラン・ネットワークを使用するための月額料金には、1 インスタンスあたり $1000 のメンバーシップ料金と、1 ピアあたり $1000 のピア料金が含まれます。詳しくは、[エンタープライズ・プランの料金](pricing.html#enterprise-plan-pricing)を参照してください。
- **Hyperledger Fabric のバージョン:** エンタープライズ・プラン・ネットワークは Hyperledger Fabric v1.1 で実行されます。  
- **影響を受けるリソース:** チェーンコード (スマート・コントラクト)、ビジネス・ネットワーク定義、クライアント・アプリケーション。
- **所要時間:** 基本的なネットワークをスターター・プランからエンタープライズ・プランにマイグレーションするのに、少なくとも半日かかります。
- **既存の台帳データ**は、スターター・プラン・ネットワークからエンタープライズ・プラン・ネットワークに移行できません。テスト・データが実稼働環境に存在するのは、適切でないためです。

**注:** *基本的な* ネットワークとは、2 つの組織と、ピア 2 つ、チャネル 1 つ、チェーンコードまたはビジネス・ネットワーク・アーカイブ (`.bna`) ファイル 1 つが存在するものです。マイグレーションにかかる実際の時間は、エンタープライズ・プラン・ネットワークに必要なネットワーク・コンポーネントの規模と複雑さに応じて異なります。

## マイグレーション・チェックリスト
{: #migrate_starter_to_enterprise_checklist}

スターター・プラン・ネットワークからエンタープライズ・プラン・ネットワークへの移行を準備するには、いくつかのタスクを実行する必要があります。詳細な手順については後のセクションで説明しますが、以下に概要を示します。

- エンタープライズ・プラン・ネットワークを作成します。
- Hyperledger Composer を使用して `.bna` を開発した場合は、`.bna` ファイルを見つけてマイグレーションします。
- スターター・プランのテスト・ネットワークを基に、必要な構成の組織とピアを再作成します。
- エンタープライズ・プラン・ネットワークで実行する Go または Node 言語の作成済みチェーンコードを決定します。
- エンタープライズ・プラン・ネットワーク用の新規 API エンドポイント情報を使用して、クライアント・アプリケーションを更新します。

### エンタープライズ・プラン・ネットワークの作成
{: #migrate_starter_to_enterprise_create_network}

マイグレーションを行う前に、エンタープライズ・プラン・ネットワークを作成する必要があります。詳しくは、[エンタープライズ・プラン・ネットワークの作成](../get_start.html#creating-a-network)を参照してください。

### `.bna` ファイルのマイグレーション
{: #migrate_starter_to_enterprise_bna}

**注:** スターター・プラン・ネットワークで `.bna` ファイルを使用していない場合は、この手順をスキップできます。

Hyperleger Composer を使用してビジネス・ネットワークを定義し、`.bna` ファイルをスターター・プラン・ネットワークにデプロイした場合は、同じ `.bna` ファイルをエンタープライズ・プラン・ネットワークにデプロイできます。

- ビジネス・ネットワーク・アーカイブ・ファイル (`.bna`) がある場合は、[エンタープライズ・プランへのビジネス・ネットワークのデプロイ](../develop_enterprise.html)の説明に従ってください。
- `.bna` ファイルがない場合は、`composer network download` コマンドを使用してスターター・プラン・インスタンスから取得します。 `composer network download` コマンドについて詳しくは、[Hyperledger Composer コマンド・ラインの資料![「外部リンク」アイコン](../images/external_link.svg "「外部リンク」アイコン")](https://hyperledger.github.io/composer/latest/reference/commands){:new_window} を参照してください。 そして、[エンタープライズ・プランへのビジネス・ネットワークのデプロイ](../develop_enterprise.html)の説明に従うことができます。

### ネットワーク構成の再作成
{: #migrate_starter_to_enterprise_config_network}

スターター・プラン・ネットワークの組織 (メンバー)、チャネル、ピアの構成をエンタープライズ・プラン・ネットワークで再作成することができます。これらのネットワーク・リソースは、ネットワーク・モニター UI を使用して再作成できます。具体的には、該当する組織を招待し (注: スターターと同じように組織を**切り替える**ことはできないので注意してください)、チャネルを作成し、ピアを作成します (やはり、招待された組織がピアを各自で作成する必要があります)。

1. {{site.data.keyword.cloud_notm}} でエンタープライズ・プラン・ネットワークにログインし、ネットワーク・モニターを開始します。
2. 「メンバー」画面で組織 (メンバー) を再作成し、「チャネル」画面でチャネルを再作成し、「概説」画面でピアを再作成します。ネットワーク・リソースの作成方法について詳しくは、[エンタープライズ・プラン・ネットワークの操作](../v10_dashboard.html#overview)を参照してください。
3. スターター・プラン・ネットワークの場合と同様に、メンバーを追加し、チャネル・ポリシーを設定してチャネルを構成します。

**注:** 高可用性を実現するには、組織に 2 つ以上のピアを作成し、それらを同じチャネルに参加させ、必要時にピアを切り替えるようにクライアント・アプリケーションを適切にコーディングする必要があります。

### チェーンコードのマイグレーション
{: #migrate_starter_to_enterprise_cc}

チェーンコードは、外部のローカル環境で開発するものであり、クライアント・アプリケーションによって呼び出されます。スターター・プラン・ネットワークでテストしたチェーンコードを、エンタープライズ・プラン・ネットワーク上の選択したピアにインストールしてインスタンス化するには、[チェーンコードのインストール、インスタンス化、および更新](./install_instantiate_chaincode.html#installchaincode)の説明に従ってください。

### クライアント・アプリケーションの更新
{: #migrate_starter_to_enterprise_app}

スターター・プラン・ネットワークでテストした既存のクライアント・アプリケーションを、エンタープライズ・プラン・ネットワーク用の新規 API エンドポイント情報を使用して更新する必要があります。詳しくは、[ネットワーク資格情報と接続プロファイルの取得](../get_start.html#retrieving-network-credentials-and-connection-profile)を参照してください。

高可用性のために、応答していないピアを検知してトランザクションを別のピアに転送する処理は、クライアント・アプリケーションが行う必要があります。

## 既存のスターター・プラン・ネットワークの利用方法
{: #migrate_starter_to_enterprise_existing_network}

既存のスターター・プラン・ネットワークをサンドボックス環境として引き続き使用して、新規プロジェクトを作成したり、既存のチェーンコードに対する変更をテストしたりできます。さらに、エンタープライズ・プラン・ネットワークにマイグレーションしないテスト台帳データを、スターター・プラン・ネットワークで維持することができます。

すべてのテストが完了し、すべてが正常に機能することを確認するまでは、スターター・ネットワークを削除しないでください。しかし、スターター・ネットワークと台帳データが不要になったら、ネットワークを安全に削除することができます。詳しくは、[ネットワークの削除または離脱](../get_start_starter_plan.html#deleting-or-leaving-a-network)を参照してください。