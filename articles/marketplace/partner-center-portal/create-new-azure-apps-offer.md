---
title: Azure アプリケーション オファーを作成する - Microsoft 商業マーケットプレース
description: パートナー センターの商業マーケットプレース ポータルで、新しい Azure アプリケーション オファーを作成するための手順と考慮事項について学習します。 Azure Marketplace で、またはクラウド ソリューション プロバイダー (CSP) プログラムを使用して、Azure アプリケーション オファーを一覧表示したり、販売したりすることができます。
author: qianw211
ms.author: dsindona
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
ms.date: 05/03/2020
ms.openlocfilehash: 22d6c37b59488633394d7f3ed5ca5b0c78371e7d
ms.sourcegitcommit: e0330ef620103256d39ca1426f09dd5bb39cd075
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82790689"
---
# <a name="create-an-azure-application-offer"></a>Azure アプリケーション オファーを作成する

この記事では、商業マーケットプレースで新しい Azure アプリケーション オファーを作成するための手順と考慮事項について説明します。 新しい Azure アプリケーション オファーを作成する前に、これらの概念についてよく理解しておく必要があります。 

新しい Azure アプリケーション オファーを公開する前に、[パートナー センターで商業マーケットプレース アカウントを作成](https://docs.microsoft.com/azure/marketplace/partner-center-portal/create-account)し、アカウントが商業マーケットプレース プログラムに登録されていることを確認します。

## <a name="before-you-begin"></a>開始する前に

Azure アプリケーション オファーを設計、構築、およびテストするには、Azure プラットフォームと、そのオファーの構築に使用されるテクノロジの両方の技術的な知識が必要です。 エンジニアリング チームには､Microsoft の次の技術に関する知識も必要です｡

* [Azure のサービス](https://azure.microsoft.com/services/)に関する基本知識。
* [Azure アプリケーションとそのアーキテクチャを設計する](https://azure.microsoft.com/solutions/architecture/)方法。
* [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/)、[Azure Storage](https://azure.microsoft.com/services/?filter=storage#storage)、[Azure ネットワーク](https://azure.microsoft.com/services/?filter=networking#networking)に関する実用的な知識。
* [Azure Resource Manager](https://azure.microsoft.com/features/resource-manager/) に関する実用的な知識。
* [JSON](https://www.json.org/) に関する実用的な知識。

### <a name="technical-documentation-and-resources"></a>技術ドキュメントとリソース

商業マーケットプレース用に Azure アプリケーション オファーを準備する際には、次のリソースを確認してください。

* [Azure Resource Manager テンプレートについての理解](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates)

* クイック スタート:

    * [Azure クイック スタート テンプレート](https://azure.microsoft.com/documentation/templates/)
    * [GitHub Azure クイックスタート テンプレート](https://github.com/azure/azure-quickstart-templates)
    * [アプリケーション定義の発行](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app)
    * [サービス カタログ アプリのデプロイ](https://docs.microsoft.com/azure/managed-applications/deploy-service-catalog-quickstart)

* チュートリアル:

    * [定義ファイルの作成](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app)
    * [マーケットプレース アプリケーションの発行](https://docs.microsoft.com/azure/managed-applications/publish-marketplace-app)

* サンプル:

    * [Azure CLI](https://docs.microsoft.com/azure/managed-applications/cli-samples)
    * [Azure PowerShell](https://docs.microsoft.com/azure/managed-applications/powershell-samples)
    * [マネージド アプリケーション ソリューション](https://docs.microsoft.com/azure/managed-applications/sample-projects)

「[Azure Marketplace 向けのソリューション テンプレートとマネージド アプリケーションの作成](https://channel9.msdn.com/Events/Build/2018/BRK3603)」ビデオでは、Azure アプリケーション オファーの種類について包括的に紹介しています。

* 使用できるオファーの種類
* 必要な技術資産
* Azure Resource Manager テンプレートの作成方法
* アプリ UI の開発とテスト
* アプリ オファーを発行する方法
* アプリケーション レビュー プロセス

### <a name="suggested-tools"></a>推奨ツール

Azure アプリケーションを管理するためのスクリプト環境として、次のいずれか一方または両方を選択します。

* [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)
* [Azure CLI](https://docs.microsoft.com/cli/azure)

開発環境には次にツールを加えることを推奨します｡

* [Azure 記憶域エクスプローラー](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)
* [Visual Studio Code](https://code.visualstudio.com/) と次の拡張機能:
    * 拡張機能: [Azure リソース マネージャー ツール](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools)
    * 拡張機能: [Beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)
    * 拡張機能: [Prettify JSON](https://marketplace.visualstudio.com/items?itemName=mohsen1.prettify-json)

使用できるツールについては、[Azure 開発者ツール](https://azure.microsoft.com/tools/)に関するページをご覧ください。 また、Visual Studio を使用している場合は、[Visual Studio Marketplace](https://marketplace.visualstudio.com/) をご覧ください。

## <a name="types-of-azure-application-plans"></a>Azure アプリケーション プランの種類

Azure アプリケーション プランには、ソリューション テンプレートとマネージド アプリケーションの 2 種類があります。

* **ソリューション テンプレート**は、マーケットプレースでソリューションを発行するための主要な手段の 1 つです。 ソリューションで、単一の仮想マシン (VM) の範囲を超える追加のデプロイと構成の自動化が必要な場合は、このプランの種類を使用します。 ソリューション テンプレートを使うと、複雑な IaaS ソリューションを提供するための VM、ネットワーク、ストレージ リソースなどの複数のリソースの提供を自動化できます。  ソリューション テンプレートの作成について詳しくは、[Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)に関するページをご覧ください。

* **マネージド アプリケーション**はソリューション テンプレートと似ていますが、大きな違いが 1 つあります。 マネージド アプリケーションでは、アプリの発行元によって管理されているリソース グループが、リソースのデプロイ先となります。 リソース グループはユーザーのサブスクリプション内に存在しますが、そのリソース グループにアクセスできるのは、発行元のテナントの ID です。 発行元は、ソリューションの継続的なサポートにかかるコストを指定します。 フル マネージドのターンキー アプリケーションを簡単に構築して顧客に提供するには、マネージド アプリケーションを使用します。  マネージド アプリケーションの利点と種類について詳しくは、「[Azure マネージド アプリケーションの概要](https://docs.microsoft.com/azure/managed-applications/overview)」をご覧ください。

## <a name="technical-requirements"></a>技術的な要件

すべての Azure アプリケーションでは、`.zip` アーカイブのルート フォルダーに少なくとも 2 つのファイルが含まれています。

* [mainTemplate.json](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) という名前の Resource Manager テンプレート ファイル。  このテンプレートでは、顧客の Azure サブスクリプションにデプロイするリソースが定義されます。  Resource Manager テンプレートの例については、[Azure クイック スタート テンプレート ギャラリー](https://azure.microsoft.com/resources/templates/)または対応する [GitHub: Azure Resource Manager クイックスタート テンプレート](https://github.com/azure/azure-quickstart-templates) リポジトリをご覧ください。

* [createUiDefinition.json](https://docs.microsoft.com/azure/managed-applications/create-uidefinition-overview) という名前の、Azure アプリケーション作成エクスペリエンス用のユーザー インターフェイス定義。  ユーザー インターフェイスでは、コンシューマーがパラメーター値を入力できるようにする要素を指定します。

すべての新しい Azure アプリケーション オファーには、[Azure パートナーの顧客の使用状況の属性 GUID](https://docs.microsoft.com/azure/marketplace/azure-partner-customer-usage-attribution) が含まれている必要があります。 

各アプリケーション プランの公開の要件について詳しくは、[ソリューション テンプレート オファーの公開の要件](../marketplace-solution-templates.md)と[マネージド アプリケーション オファーの公開の要件](../marketplace-managed-apps.md)に関するページをご覧ください。

## <a name="create-a-new-offer"></a>新しいオファーを作成する

>[!NOTE]
>オファーが公開された後にパートナー センターで編集した内容は、そのオファーを再公開するまでネットショップに表示されません。 変更後は必ずオファーを再公開してください。

1. [パートナー センター](https://partner.microsoft.com/dashboard/home)にサインインします。

1. 左側のメニューで、 **[コマーシャル マーケットプレース]**  >  **[概要]** の順に選択します。

1. [概要] ページで、 **[+ 新しいオファー]**  >  **[Azure アプリケーション]** の順に選択します。

    ![左側のナビゲーション メニューの画像。](./media/new-offer-azure-app.png)

1. **[新しいオファー]** ページで、 **[オファー ID]** を入力します。 これは、アカウントのオファーごとに一意の識別子です。

     * この ID は、マーケットプレース オファーの Web アドレスと Azure Resource Manager テンプレート (該当する場合) で顧客に表示されます。
     * 使用できるのは小文字と数字だけです。 ハイフンとアンダースコアを含めることができますが、スペースは使用できず、文字数は 50 文字に制限されています。 たとえば、「**test-offer-1**」と入力すると、オファーの Web アドレスは `https://azuremarketplace.microsoft.com/marketplace/../test-offer-1` になります。
     * **[作成]** を選択した後で、オファー ID を変更することはできません。

1. **[オファーのエイリアス]** を入力します。 これは、パートナー センター内でオファーに使用される名前です。

     * この名前はマーケットプレースでは使用されず、顧客に表示されるオファー名やその他の値とは異なります。
     * **[作成]** を選択した後で、オファーの別名を変更することはできません。

1. **[作成]** を選択してオファーを生成し、続行します。

## <a name="offer-setup"></a>オファーのセットアップ

**[オファーのセットアップ]** ページでは、オファーの体験版とリード管理を構成することができます。 

### <a name="test-drive"></a>体験版

体験版は、"購入前に試用する" オプションを提供することで潜在顧客へのオファーを紹介し、その結果、コンバージョンが増加し、見込みの高いリードが生成される優れた方法です。 [体験版の詳細についてはこちらを参照してください](https://docs.microsoft.com/azure/marketplace/cloud-partner-portal/test-drive/what-is-test-drive)。

一定期間、体験版を有効にするには、 **[体験版を有効にする]** チェック ボックスをオンにします。 オファーから体験版を削除するには、このチェック ボックスをオフにします。 このトピックの後述の「[体験版の技術的な構成](#test-drive-technical-configuration)」セクションで、体験版環境を構成します。

詳細については、[商業マーケットプレースでのオファーの体験](https://docs.microsoft.com/azure/marketplace/partner-center-portal/test-drive)に関するページを参照してください。 また、[体験版のベスト プラクティス](https://github.com/Azure/AzureTestDrive/wiki/Test-Drive-Best-Practices)を参照し、[体験版の概要に関する PDF](https://assetsprod.microsoft.com/mpn/azure-marketplace-appsource-test-drives.pdf) をダウンロードすることもできます (ポップアップ ブロックがオフになっていることを確認してください)

>[!Note]
>すべての Azure アプリケーションは Azure Resource Manager テンプレートを使用して実装されるため、Azure アプリケーションで使用可能な体験版の種類は [Azure Resource Manager ベースの体験版](https://docs.microsoft.com/azure/marketplace/cloud-partner-portal/test-drive/azure-resource-manager-test-drive)のみです。

## <a name="lead-management"></a>リードの管理

[!INCLUDE [Connect lead management](./includes/connect-lead-management.md)]

詳しくは、[リード管理の概要](./commercial-marketplace-get-customer-leads.md)に関する記事をご覧ください。

続行する前に、 **[下書きの保存]** を選択します。

## <a name="properties"></a>Properties

**[プロパティ]** ページでは、マーケットプレース上でのオファーのグループ分けに使用するカテゴリと業界、アプリのバージョン、オファーがサポートされる法的契約を定義します。

オファーを適切なマーケットプレース検索領域に配置するには、少なくとも 1 つ、最大で 3 つのカテゴリを選択します。 オファーでこれらのカテゴリがどのようにサポートされるかを、必ずオファーの説明に記述してください。

### <a name="legal"></a>法的情報

[!INCLUDE [Commercial marketplace Standard Contract](./includes/marketplace-contract-text.md)]

## <a name="offer-listing"></a>オファーのリスト登録

このページでは、商業マーケットプレース オファーのコピーとイメージを管理します。 

### <a name="marketplace-details"></a>Marketplace の詳細

> [!NOTE]
> オファー登録情報の内容 (説明、ドキュメント、スクリーンショット、使用条件など) は、オファーの説明が "このアプリケーションは、<英語以外の言語> でのみ利用可能です" という文言で始まっていれば、英語である必要はありません。 また、オファー登録情報のコンテンツで使用されている言語以外の言語でコンテンツを提供するための*役に立つリンクの URL* を提供することもできます。

#### <a name="name"></a>名前

ここで入力する名前は、オファー登録情報のタイトルとして顧客に表示されます。 このフィールドには、オファーの作成時に **[オファーの別名]** に入力したテキストが事前に設定されていますが、この値は変更できます。 この名前は商標の場合もあります (商標または著作権マークを含めることもできます)。 名前は 50 文字以下にする必要があります。絵文字を含めることはできません。

#### <a name="search-results-summary"></a>検索結果の概要

オファーの簡単な説明 (最大 100 文字) を入力します。これは、検索結果で使用される場合があります。

#### <a name="long-summary"></a>詳細な概要

オファーの詳しい説明 (最大 256 文字) を入力します。 この説明は検索結果で使用される場合があります。

#### <a name="description"></a>説明

オファーの詳しい説明 (最大 3,000 文字) を入力します。 この説明は、一覧表示の概要で顧客に表示されます。 オファーの価値提案、主なメリット、カテゴリまたは業界との関連性、アプリ内の購入機会、必要な情報開示を含めます。

説明を記述するためのいくつかのヒントを次に示します。

* 説明の先頭の数文で、プランの価値提案を明確に説明します。 次の項目を含めます。
  * オファーの説明。
  * オファーから利益を得るユーザーの種類。
  * オファーが対応する顧客のニーズや問題。
* 先頭のいくつかの文が検索エンジンの結果に表示される場合があることに注意してください。
* 特徴や機能に頼ってオファーを販売しないでください。 代わりに、オファーによって提供される価値に焦点を当てます。
* 業界固有または特典ベースの表現を使用します。
* HTML タグを使用して、説明の書式を設定し、より魅力的なものにすることを検討してください。

#### <a name="search-keywords"></a>キーワード検索

オファーを顧客がマーケットプレースで検索できるように、必要に応じて最大 3 つの検索キーワードを入力することができます。 最良の結果を得るために、これらのキーワードを説明にも使用します。

#### <a name="privacy-policy-link"></a>プライバシー ポリシーのリンク

自分の組織のプライバシー ポリシーへの URL を入力します。 プライバシーに関する法律および規制にアプリが準拠していることを保証し、有効なプライバシー ポリシーを提供する責任があります。

### <a name="useful-links"></a>便利なリンク

**[+ リンクの追加]** を選択し、ソリューションに関する省略可能な補足オンライン ドキュメントへのリンクを追加します。

### <a name="contact-information"></a>連絡先情報

**サポートの連絡先**、**エンジニアリングの連絡先**、および **CSP プログラムの連絡先**の名前、メール、電話番号を指定します。 この情報は顧客には表示されませんが、Microsoft で利用できるようになり、CSP パートナーに提供される場合があります。 連絡先によっては追加情報が必要になる場合があります。

### <a name="marketplace-media"></a>Marketplace メディア

オファーで使用するロゴと画像を提供します。 画像はすべて PNG 形式である必要があります。 画像がぼやけていると、送信が拒否されます。

>[!Note]
>ファイルのアップロードで問題が発生した場合は、確実に、パートナー センターで使用されている https://upload.xboxlive.com サービスがローカル ネットワークでブロックされないようにしてください。

#### <a name="store-logos"></a>ストア ロゴ

オファーのロゴの PNG ファイルを次の 3 つのピクセル サイズで提供します。

- **小** (48 x 48)
- **中** (90 x 90)
- **大** (216 x 216)
- **ワイド** (255 x 115)

3 つすべてのロゴが必要であり、一覧のさまざまな場所で使用されます。

#### <a name="screenshots"></a>Screenshots (スクリーンショット)

オファーがどのように動作するかを示すスクリーンショットを最大 5 つ追加します。 各スクリーンショットは、サイズが 1280 x 720 ピクセルの PNG 形式にする必要があります。 各スクリーンショットにはキャプションが含まれている必要があります。

#### <a name="videos"></a>ビデオ

オファーをデモンストレーションするビデオを最大 5 つ追加します。 これらは、外部のビデオ サービスでホストされている必要があります。 各ビデオの名前、Web アドレス、ビデオのサムネイルの PNG 画像 (1280 x 720 ピクセル) を入力します。

#### <a name="additional-marketplace-listing-resources"></a>マーケットプレースのリスト登録に関するその他のリソース

- [マーケットプレース オファーのリスト登録に関するベスト プラクティス](https://docs.microsoft.com/azure/marketplace/gtm-offer-listing-best-practices)

続行する前に、 **[下書きの保存]** を選択します。

## <a name="preview-audience"></a>プレビュー対象ユーザー

[プレビュー] タブでは、マーケットプレースの幅広い対象ユーザーに対して一般公開する前にオファーを検証するため、限られた**プレビュー対象ユーザー**を選択します。

> [!IMPORTANT]
> プレビューでオファーを確認した後、 **[一般公開する]** を選択して、マーケットプレースのパブリック対象ユーザーにオファーを発行します。

プレビュー対象ユーザーは、Azure サブスクリプション ID の GUID と、それぞれの対するオプションの説明によって識別されます。 いずれのフィールドも顧客は表示できません。 Azure サブスクリプション ID は、Azure portal の **[サブスクリプション]** ページにあります。

少なくとも 1 つの Azure サブスクリプション ID を、個別に (最大 10 個)、または CSV ファイルをアップロードすることによって (最大 100 個) 追加します。 これらのサブスクリプション ID を追加することで、オファーを一般公開する前にプレビューできるユーザーを定義します。 オファーが既に公開されている場合も、オファーの変更や更新をテストするために、プレビュー対象ユーザーを定義することができます。

> [!NOTE]
> プレビュー対象ユーザーはプライベート対象ユーザーとは異なります。 プレビュー対象ユーザーは、マーケットプレースで一般公開される "_前に_"、オファーにアクセスすることができます。 オファーがマーケットプレースに完全に公開された後でプライベート対象ユーザーだけが使用できるプランも含めて、すべてのプランを表示し、検証することができます。 プライベート対象ユーザーは ( **[価格と利用可否]** タブで定義します)、特定のプランに排他的にアクセスできます。

続行する前に、 **[下書きの保存]** を選択します。

## <a name="technical-configuration"></a>技術的な構成

このセクションは、Marketplace Metering Service API を使用して計測イベントを生成するマネージド アプリケーションがオファーに含まれている場合にのみ、完了してください。 計測イベントを生成するときにサービスで使用される、**Azure Active Directory テナント ID** と **Azure Active Directory アプリケーション ID** を入力します。

続行する前に、 **[下書きの保存]** を選択します。

## <a name="technical-configuration-offer-level"></a>技術的な構成 (オファー レベル)

>[!Note]
>オファー レベルの技術的な詳細は省略可能です。  これらの詳細を構成する必要があるのは、従量制課金でマネージド アプリケーションを公開し、Azure AD セキュリティ トークンで認証するサービスがある場合のみです。 詳細については、「[認証の戦略](./marketplace-metering-service-authentication.md)」のさまざまな認証オプションを参照してください。

技術的な構成では、サービスを特定するために使用される詳細 (テナント ID とアプリ ID) を定義します。これにより、[Marketplace Metering Service API](./marketplace-metering-service-apis.md) を使用してマネージド アプリケーションの計測イベントが生成されます。  計測イベントを生成するときにサービスで使用される ID を入力します。

* **Azure AD テナント ID** (必須): Azure portal 内では、Microsoft の 2 つのサービス間の接続が認証済みの通信の背後で行われることを Microsoft が検証できるように、[Azure Active Directory (AD) アプリを作成](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal)する必要があります。 [テナント ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) を見つけるには、Azure Active Directory に移動して **[プロパティ]** を選択し、一覧表示される**ディレクトリ ID** 番号 (50c464d3-4930-494c-963c-1e951d15360e など) を探します。
* **Azure AD app ID (Azure AD アプリ ID)** (必須): また、自分の[アプリケーション ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) と認証キーも必要です。 これらの値を取得するには、Azure Active Directory に移動して **[アプリの登録]** を選択し、一覧表示される**アプリケーション ID** 番号 (50c464d3-4930-494c-963c-1e951d15360e など) を探します。 認証キーを見つけるには、 **[設定]** に移動して **[キー]** を選択します。 説明と期間を入力する必要があります。その後、数値が提供されます。

>[!Note]
>Azure アプリケーション ID は公開元 ID に関連付けられ、この公開元アカウント内でのみ再利用できます。

>[!Note]
>[Batch 使用状況イベント](https://docs.microsoft.com/azure/marketplace/partner-center-portal/marketplace-metering-service-apis#batch-usage-event)を使用する場合は、この構成が必要です。  [使用状況イベント](https://docs.microsoft.com/azure/marketplace/partner-center-portal/marketplace-metering-service-apis#usage-event)を送信する場合は、[インスタンス メタデータ サービス](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)を使用して、[JSON Web トークン (JWT) ベアラー トークン](https://docs.microsoft.com/azure/marketplace/partner-center-portal/pc-saas-registration#get-a-token-based-on-the-azure-ad-app)を取得することもできます。

## <a name="plan-overview"></a>プランの概要

このタブでは、同じオファー内でさまざまなプラン オプションを提供することができます。 これらのプラン (Cloud パートナー ポータルでは SKU と呼ばれます) は、プランの種類 (ソリューション テンプレートとマネージド アプリケーション)、収益化、または対象ユーザーが異なっていてもかまいません。  オファーがマーケットプレースの一覧に表示されるためには、少なくとも 1 つのプランを構成します。

作成後、オファーの名前、ID、プランの種類、利用可否 (パブリックまたはプライベート)、現在の公開状態、使用可能なアクションが、このタブに表示されます。

**[プランの概要]** で使用可能な**アクション**は、プランの現在の状態によって異なり、以下を含む場合があります。

* プランの状態が **[ドラフト]** の場合 – ドラフトの削除。
* プランの状態が **[ライブ]** の場合 – プランの販売の停止、またはプライベート対象ユーザーの同期。

### <a name="create-new-plan"></a>新しいプランを作成する

***[プラン ID]*** – このオファーのプランごとに一意のプラン ID を作成します。 この ID は、製品の URL で顧客に表示されます。  小文字の英数字、ダッシュ、アンダースコアのみを使用してください。 このプラン ID は最大で 50 文字にできます。 作成を選択した後で、この ID を変更することはできません。

***[プラン名]*** - この名前は、顧客がオファー内のどのプランを選択するかを決めるときに表示されます。 このオファーのプランごとに一意のオファー名を作成します。 プラン名は、同じオファーの一部である可能性があるソフトウェア プランを区別するために使用されます (たとえば、オファー名: Windows Server、プラン: Windows Server 2016 と Windows Server 2019)。

### <a name="plan-setup"></a>プランのセットアップ

このタブでは、プランの種類の大まかな構成、別のプランのパッケージを再利用するかどうか、およびプランを使用可能にする必要のあるクラウドを設定できます。 このタブでの設定により、同じプランの他のタブに表示されるフィールドが変わります。

#### <a name="plan-type"></a>プランの種類
オファーのプランの種類を選択します。 **ソリューション テンプレート** プランは、顧客によって完全に管理されます。 **マネージド アプリケーション** プランを使用すると、公開元が顧客に代わってアプリケーションを管理できます。 詳細については、「[Azure アプリケーション プランの種類](#types-of-azure-application-plans)」を参照してください。

#### <a name="re-use-technical-configuration"></a>技術的な構成を再利用する

同じ種類のプランが複数あり、それらの間でパッケージが同一である場合は、 **[this plan reuses packages from another plan]\(このプランで別のプランのパッケージを再利用する\)** を選択できます。  このオプションを選択すると、このオファーでパッケージを再利用するために、同じ種類の他のプランのいずれかを選択できるようになります。 

>[!Note]
>別のプランのパッケージを再利用すると、[技術的な構成] タブ全体がこのプランに対して表示されなくなります。 今後行う更新も含めて、他のプランの技術的な構成の詳細が、このプランにも使用されます。<br><br>このプランが公開された後にこの設定を変更することはできません。

#### <a name="azure-regions-cloud"></a>Azure リージョン (クラウド)

プランは、少なくとも 1 つの Azure リージョンで利用できる必要があります。

商業マーケットプレースが統合されているすべての Azure グローバル リージョンの顧客がプランを使用できるようにするには、 **[Azure Global]\(Azure グローバル\)** オプションを選択します。 詳細については、「[利用可能な地域と通貨サポート](https://docs.microsoft.com/azure/marketplace/marketplace-geo-availability-currencies)」を参照してください。

[Azure Government](https://docs.microsoft.com/azure/azure-government/documentation-government-welcome) リージョンでプランを使用できるようにするには、 **[Azure Government]** オプションを選択しします。 このリージョンは、アメリカの連邦政府顧客、州政府顧客、地方自治体顧客、部族政府顧客と、そのような顧客にサービスを提供する資格があるパートナーに、制御されたアクセスを提供します。 発行元は、コンプライアンス管理、セキュリティ対策、ベスト プラクティスについて責任を持ちます。 Azure Government では、物理的に離れた場所にあるデータ センターとネットワークが使用されます (場所は米国のみ)。

特定のエンドポイントが異なる可能性があるため、[Azure Government](https://docs.microsoft.com/azure/azure-government/documentation-government-manage-marketplace-partners) に発行する前に、環境でプランをテストおよび検証します。 プランを設定してテストするには、[Microsoft Azure Government 試用版](https://azure.microsoft.com/global-infrastructure/government/request/)に試用版アカウントを申請します。

>[!NOTE]
>プランが発行され、特定の Azure リージョンで利用できるようになったら、そのリージョンは削除できません。

#### <a name="azure-government-certifications"></a>Azure Government の認定資格

このオプションが表示されるのは、 **[Azure Government]** を選択した場合のみです。

Azure Government サービスでは、特定の政府の規制および要件の対象となるデータが処理されます。 FedRAMP、NIST 800.171 (DIB)、ITAR、IRS 1075、DoD L4、CJIS などです。 これらのプログラムの認定資格を認識させるため、認定資格について説明するリンクを 100 個まで提供することができます。 これらでは、プログラムでの一覧に直接リンクすることも、独自の Web サイトでのそれらについてのコンプライアンスに関する説明にリンクすることもできます。 これらのリンクは、Azure Government の顧客にのみ表示されます。

続行する前に、 **[下書きの保存]** を選択します。

### <a name="plan-listing"></a>プランのリスト登録

ここでは、プランのリストの詳細を構成します。 このタブには、同じオファーのプラン間で異なる可能性がある特定の情報が表示されます。

#### <a name="plan-name"></a>プラン名

ここには、登録時にプランに付けた名前が事前入力されます。 この名前は、このプランのタイトルとしてマーケットプレースに表示され、100 文字に制限されます。

#### <a name="plan-summary"></a>プラン概要

(オファーではなく) プランについて簡単にまとめた説明です。 この概要は、100 文字までに制限されています。

#### <a name="plan-description"></a>プラン説明

このソフトウェア プラン独特の要素やオファーに含まれる他のプランとの違いを説明します。 オファーについては説明しないでください。プランの説明だけです。 プランの説明は、最大 2,000 文字まで許されます。

続行する前に、 **[下書きの保存]** を選択します。

### <a name="availability-solution-template-plans-only"></a>可用性 (ソリューション テンプレート プランのみ)

プランを、すべてのユーザーに表示するか、または特定の顧客 (プライベート対象ユーザー) のみに表示するかを指定できます。また、プランを他のソリューション テンプレートまたはマネージド アプリケーションでのみ使用されるように非表示にするかどうかを指定できます。

#### <a name="plan-visibility"></a>プランの可視性

各プランは、すべてのユーザーに、あるいは自分が選択した特定の対象ユーザーにのみ表示されるように構成できます。 Azure サブスクリプション ID を使用して、この限定対象ユーザーにメンバーシップを割り当てることができます。

プランをプライベートにして、自分が選択した限定対象ユーザーにのみ表示されるようにするには、 **[This is a private plan]\(これはプライベート プランです\)** をオンにします。 プライベート プランとして公開すると、対象ユーザーを更新したり、そのプランをすべてのユーザーが利用できる状態にしたりできます。 プランは、すべてのユーザーに表示されるものとして公開すると、すべてのユーザーに表示したままにしなければなりません。プライベート プランとして再構成することはできません。

プランをプライベートにする場合は、**Azure サブスクリプション ID** とその説明を入力します。 それぞれが、このプライベート プランにアクセスできる対象ユーザーとなります。 アクセス権は Azure サブスクリプション ID を使用して割り当てられます。必要に応じて、割り当て先の各 Azure サブスクリプション ID の説明を含めることができます。 最大 10 個の顧客サブスクリプション ID を個別に、または CSV ファイルをインポートして 20,000 個を追加します。 Azure サブスクリプション ID は GUID として表されます。文字は小文字にする必要があります。

>[!Note]
>プライベートまたは制限付きの対象ユーザーは、 **[プレビュー]** タブで定義したプレビュー対象ユーザーとは異なります。プレビュー対象ユーザーは、マーケットプレースで公開される "_前の_" オファーにアクセスできます。 プライベート対象ユーザーの選択は特定のプランにのみ適用されますが、プレビュー対象ユーザーは (プライベートであるかどうかに関係なく) 検証のためすべてのプランを表示できます。

#### <a name="hide-plan"></a>プランの非表示

別のソリューション テンプレートまたはマネージド アプリケーションによって参照されることにより間接的にのみデプロイされることを意図されているソリューションテン プレートの場合、ソリューション テンプレートを発行しても、顧客が検索して直接参照できないようにするには、このチェック ボックスをオンにします。

続行する前に、 **[下書きの保存]** を選択します。

### <a name="pricing-and-availability-managed-application-plans-only"></a>価格と利用可否 (マネージド アプリケーション プランのみ)

これを使用して、このプランを利用可能にする**市場**、ソリューション管理の月単位の**価格**を構成します。また、特定の顧客にのみ表示する (プライベート対象ユーザー) 場合は**プランの可視性**を構成します。

続行する前に、 **[下書きの保存]** を選択します。

#### <a name="markets"></a>市場

すべてのプランは、少なくとも 1 つの市場で利用できる必要があります。 このプランを利用可能にしたい市場の場所について、このチェック ボックスを選択します。 (Microsoft が公開元に代わって消費税と使用税を送金する) "税送金" 国を選択するための検索ボックスおよびボタンが、補助として含まれています。

米国ドル (USD) でプランの価格を既に設定していて、別の市場の場所を追加する場合、新しい市場の価格は現時点の為替レートに従って計算されます。 常に、各市場の価格を発行前に確認します。 価格は、変更の保存後に "価格のエクスポート (xlsx)" リンクを使用して確認できます。

#### <a name="pricing"></a>価格

このプランの月ごとの価格を指定します。  このソリューションによってデプロイされるリソースによって発生する Azure インフラストラクチャまたは従量課金制ソフトウェアのコストに、この価格が追加されます。

月ごとの価格に加え、[従量制課金](./azure-app-metered-billing.md)を使用して、非標準ユニットの消費に対する価格を設定することもできます。  月ごとの価格を 0 に設定し、必要に応じて、従量制課金のみを使用して課金することができます。 

USD (USD = 米国ドル) で設定された価格は、保存時の最新の為替レートを使用して、選択されたすべての市場の現地通貨に変換されます。 これらの価格は公開前に検証してください。そのためには、価格スプレッドシートをエクスポートして各市場の価格を確認します。 個々の市場でカスタム価格を設定したい場合は、価格スプレッドシートを修正してインポートします。 

>[!Note]
>価格データのエクスポートを有効にするには、先に価格の変更を保存する必要があります。

プランの発行後に変更できる内容には一部制限があるため、価格は公開前に注意深く確認してください。  

>[!Note]
>プランの市場の価格は、公開されると後で変更することができません。

#### <a name="plan-visibility"></a>プランの可視性

各プランは、すべてのユーザーに、あるいは自分が選択した特定の対象ユーザーにのみ表示されるように構成できます。 Azure サブスクリプション ID を使用して、この限定対象ユーザーにメンバーシップを割り当てることができます。

プランをプライベートにして、自分が選択した限定対象ユーザーにのみ表示されるようにするには、 **[This is a private plan]\(これはプライベート プランです\)** をオンにします。 プライベート プランとして公開すると、対象ユーザーを更新したり、そのプランをすべてのユーザーが利用できる状態にしたりできます。 プランは、すべてのユーザーに表示されるものとして公開すると、すべてのユーザーに表示したままにしなければなりません。プライベート プランとして再構成することはできません。

プランをプライベートにする場合は、**Azure サブスクリプション ID** とその説明を入力します。 それぞれが、このプライベート プランにアクセスできる対象ユーザーとなります。 アクセス権は Azure サブスクリプション ID を使用して割り当てられます。必要に応じて、割り当て先の各 Azure サブスクリプション ID の説明を含めることができます。 最大 10 個の顧客サブスクリプション ID を個別に、または CSV ファイルをインポートして 20,000 個を追加します。 Azure サブスクリプション ID は GUID として表されます。文字は小文字にする必要があります。

>[!Note]
>プライベートまたは制限付きの対象ユーザーは、 **[プレビュー]** タブで定義したプレビュー対象ユーザーとは異なります。プレビュー対象ユーザーは、マーケットプレースで公開される "_前の_" オファーにアクセスできます。 プライベート対象ユーザーの選択は特定のプランにのみ適用されますが、プレビュー対象ユーザーは (プライベートであるかどうかに関係なく) 検証のためすべてのプランを表示できます。

### <a name="technical-configuration"></a>技術的な構成 

このタブでは、顧客がプランをデプロイできるようにする展開パッケージをアップロードできます。

>[!Note]
>**[プランのセットアップ]** タブで別のプランからパッケージを再利用するようにこのプランを構成した場合、このタブは表示されません。

#### <a name="package-details"></a>パッケージの詳細

このタブでは、技術的な構成のドラフト バージョンを編集できます。

**バージョン** – 技術的な構成の現在のバージョンを割り当てます。  このページに変更を発行するたびに、このバージョンをインクリメントします。 バージョンは `{integer}.{integer}.{integer}` の形式でなければなりません。

**パッケージ ファイル** (.zip) - このパッケージには、このプランに必要なすべてのテンプレート ファイルとすべての追加リソースが、`.zip` ファイルとしてパッケージ化されて含まれます。

すべての Azure アプリケーション プラン パッケージの `.zip` アーカイブのルート フォルダーには、次の 2 つのファイルが含まれている必要があります。

* [mainTemplate.json](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) という名前の Resource Manager テンプレート ファイル。 このテンプレートにより、顧客の Azure サブスクリプションへのリソースのデプロイが自動化されます。  Resource Manager テンプレートの例については、[Azure クイック スタート テンプレート ギャラリー](https://azure.microsoft.com/documentation/templates/)または対応する [GitHub: Azure Resource Manager クイックスタート テンプレート](https://github.com/azure/azure-quickstart-templates) リポジトリをご覧ください。
* [createUiDefinition.json](https://docs.microsoft.com/azure/azure-resource-manager/managed-application-createuidefinition-overview) という名前の、Azure アプリケーション作成エクスペリエンス用のユーザー インターフェイス定義。

サポートされる最大ファイル サイズは次のとおりです。

* `.zip` 圧縮アーカイブ サイズ合計で最大 1 GB
* `.zip` アーカイブ内の圧縮されていなり個々のファイルについて最大 1 GB  

すべての新しい Azure アプリケーション オファーには、[Azure パートナーの顧客の使用状況の属性 GUID](https://docs.microsoft.com/azure/marketplace/azure-partner-customer-usage-attribution) も含まれている必要があります。

>[!Note]
>ファイルのアップロードで問題が発生した場合は、パートナー センターで使用されている https://upload.xboxlive.com サービスがローカル ネットワークでブロックされていないことを確認してください。

マネージド アプリケーション プランには、このタブに関する追加情報が必要です。

#### <a name="previously-published-packages"></a>発行済みのパッケージ

**[発行済みのパッケージ]** サブタブでは、技術的な構成のすべての発行済みバージョンを見ることができます。

#### <a name="enable-just-in-time-jit-access"></a>Just-In-Time (JIT) アクセスの有効化

このプランに対して Just-In-Time (JIT) アクセスを有効にするには、このオプションを選択します。  JIT アクセスによって、発行元は、トラブルシューティングやメンテナンスを行うために、マネージド アプリケーションのリソースに対して昇格されたアクセス権を要求することができます。 発行元は、リソースへの読み取り専用アクセス権を常に所有していますが、特定の期間にさらに大きなアクセス権を持つことができます。  詳しくは、「[Azure Managed Applications でジャストインタイム アクセスを有効にして要求する](https://docs.microsoft.com/azure/managed-applications/request-just-in-time-access)」をご覧ください。  マネージド アプリケーションの顧客に対し、発行元のアカウントに永続アクセス権を付与するよう要求するには、このオプションをオフのままにします。

>[!Note]
>この機能をサポートするには、`createUiDefinition.json` ファイルを更新する必要があります。  

#### <a name="deployment-mode"></a>展開モード

このプランをデプロイするときに、**完全デプロイ モード**または**増分デプロイ モード**を構成するかどうかを選択します。 

* **完全モード**では、顧客がアプリケーションを再デプロイすると、`mainTemplate.json` で定義されていない管理対象リソース グループのリソースは削除されます。 
* **増分モード**では、アプリケーションを再デプロイしても、既存のリソースは変更されずに残ります。

デプロイ モードの詳細については、「[Azure Resource Manager のデプロイ モード](https://docs.microsoft.com/azure/azure-resource-manager/deployment-modes)」をご覧ください。

#### <a name="notification-endpoint-url"></a>通知エンドポイント URL

このプラン バージョンのマネージド アプリケーション インスタンスでのすべての CRUD 操作に関する通知を受け取るための、HTTPS Webhook エンドポイントを指定します。

#### <a name="customize-allowed-customer-actions"></a>許可されている顧客アクションのカスタマイズ

このオプションは、既定で使用できる "`*/read`" アクションに加えて、顧客がマネージド リソースに対してどのアクションを実行できるかを指定する場合に選択します。 

ここでは、顧客が実行できるようにする追加のアクションを、セミコロンで区切って列挙します。  詳しくは、「[Azure リソースの拒否割り当ての概要](https://docs.microsoft.com/azure/role-based-access-control/deny-assignments)」をご覧ください。  使用できるアクションについては、「[Azure Resource Manager のリソース プロバイダー操作](https://docs.microsoft.com/azure/role-based-access-control/resource-provider-operations)」を参照してください。 たとえば、仮想マシンの再起動をコンシューマーに許可するには、許可されているアクションに `Microsoft.Compute/virtualMachines/restart/action` を追加します。

#### <a name="global-azure--azure-government-cloud"></a>グローバル Azure/Azure Government クラウド

サポートされている各クラウドで、このマネージド アプリケーションに対する管理アクセス権を持つユーザーを指定します。 管理対象リソース グループに対するアクセス許可を付与するユーザー、グループ、またはアプリケーションは、Azure Active Directory (AAD) の ID を使用して識別されます。

**Azure Active Directory テナント ID** – アクセス許可を付与するユーザー、グループ、またはアプリケーションの ID が含まれる AAD テナントの ID (ディレクトリ ID とも呼ばれる)。 AAD テナント ID は、Azure portal の [Azure Active Directory のプロパティ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Properties)で確認できます。

**承認** – 管理対象リソース グループへのアクセス許可を付与するユーザー、グループ、アプリケーションの Azure Active Directory オブジェクト ID を追加します。 プリンシパル ID でユーザーを識別します。プリンシパル ID は、[Azure portal の Azure Active Directory ユーザー ブレード](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UsersManagementMenuBlade/AllUsers)にあります。

プリンシパルごとに、一覧から Azure AD 組み込みロールのいずれかを選択します (所有者または共同作成者)。 選択したロールによって、顧客のサブスクリプションのリソースに対してプリンシパルが持つアクセス許可が記述されます。 詳細については、「[Azure リソースの組み込みロール](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles)」を参照してください。 ロールベースのアクセス制御 (RBAC) について詳しくは、[Azure portal での RBAC の概要](https://docs.microsoft.com/azure/role-based-access-control/overview)に関する記事をご覧ください。

>[!Note]
>クラウドあたり最大 100 個の承認を追加できますが、一般には、Active Directory ユーザー グループを作成し、その ID を "プリンシパル ID" で指定する方が簡単です。 これにより、プランをデプロイした後で管理グループにより多くのユーザーを追加できるようになり、承認を追加するためだけにプランを更新する必要がなくなります。

#### <a name="policy-settings"></a>ポリシー設定

マネージド アプリケーションに [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) を適用して、デプロイしたソリューションのコンプライアンス要件を指定します。 ポリシーの定義とパラメーター値の形式については、「[Azure Policy のサンプル](https://docs.microsoft.com/azure/governance/policy/samples/index)」を参照してください。 最大 5 つのポリシーと、各ポリシー オプションのただ 1 つのインスタンスを構成できます。 一部のポリシーでは、追加のパラメーターが必要です。 監査ポリシーには Standard SKU が必要です。 ポリシーの名前は 50 文字に制限されています。

続行する前に、 **[下書きの保存]** を選択します。

## <a name="co-sell-with-microsoft"></a>Microsoft と共同販売する

オファーの公開の場合、[共同販売] タブでの情報提供はすべて省略可能です。 共同販売の準備完了と IP 共同販売の準備完了の状態になっている必要があります。 指定した情報は、お客様のニーズに合わせてソリューションを評価するときに、Microsoft のセールス チームによって使用されます。 お客様が直接使用することはできません。

このタブの詳細については、「[パートナー センターの [共同販売] オプション](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-co-sell)」を参照してください。

## <a name="resell-through-csps"></a>CSP を通して再販する

[クラウド ソリューション プロバイダー](https://azure.microsoft.com/offers/ms-azr-0145p/) (CSP) プログラムでパートナーがオファーを利用できるようにすることで、オファーのリーチを拡大します。 これにより、リセラーは顧客にオファーを販売し、バンドル ソリューションを作成できます。

続行する前に、 **[下書きの保存]** を選択します。

## <a name="test-drive"></a>体験版

購入前に顧客がオファーを試すことができるデモ (体験版) を設定します。 顧客が一定期間オファーを試すことができるデモ環境を作成するには、[コマーシャル マーケットプレースでのオファーの体験版](https://docs.microsoft.com/azure/marketplace/partner-center-portal/test-drive)に関する記事をご覧ください。

体験版を有効にするには、[[オファーのセットアップ]](#test-drive) タブで **[体験版を有効にする]** チェック ボックスをオンにします。オファーから体験版を削除するには、このチェック ボックスをオフにします。

### <a name="test-drive-technical-configuration"></a>体験版の技術的な構成

- **Azure AD app ID (Azure AD アプリ ID)** (必須): 自分の Azure Active Directory (AD) [アプリケーション ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) を入力します。 この ID を見つけるには、[Azure portal](https://portal.azure.com/) にサインインして左側のメニューで [Active Directory] タブを選択し、 **[アプリの登録]** を選んでから、一覧表示される**アプリケーション ID** 番号を探します (50c464d3-4930-494c-963c-1e951d15360e など)。

#### <a name="deployment-subscription-details"></a>デプロイ サブスクリプションの詳細

体験版をお客様に代わってデプロイできるようにするには、固有の Azure サブスクリプションを別に作成して指定します (Power BI 体験版では不要)。

* **Azure サブスクリプション ID** (Azure Resource Manager および Logic Apps では必須) – リソースの使用状況レポート用および課金用の Azure アカウント サービスへのアクセス権を付与するサブスクリプション ID を入力します。 まだお持ちでない場合、体験版に使用するために[別個の Azure サブスクリプションの作成](https://docs.microsoft.com/azure/billing/billing-create-subscription)を検討することをお勧めします。 Azure サブスクリプション ID は、[Azure portal](https://portal.azure.com/) にログインし、左側にあるメニューの **[サブスクリプション]** タブに移動して見つけることができます。 このタブを選択すると、自分のサブスクリプション ID (例: "a83645ac-1234-5ab6-6789-1h234g764ghty") が表示されます。
* **Azure AD テナント ID** (必須) – 自分の Azure Active Directory (AD) [テナント ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) を入力します。 この ID を見つけるには、[Azure portal](https://portal.azure.com/) にサインインして左側のメニューで [Active Directory] タブを選択し、 **[プロパティ]** を選んでから、一覧表示される**ディレクトリ ID** 番号 (50c464d3-4930-494c-963c-1e951d15360e など) を探します。 また、[https://www.whatismytenantid.com](https://www.whatismytenantid.com) で URL のドメイン名を使用して、組織のテナント ID を検索することもできます。
* **Azure AD テナント名** (Dynamic 365 では必須) – 自分の Azure Active Directory (AD) 名を入力します。 この名前を見つけるには、[Azure portal](https://portal.azure.com/) にサインインします。右上隅にある自分のアカウント名の下に、テナント名が表示されます。
* **Azure AD アプリ ID** (必須) – 自分の Azure Active Directory (AD) [アプリケーション ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) を入力します。 この ID を見つけるには、[Azure portal](https://portal.azure.com/) にサインインして左側のナビゲーション メニューで [Active Directory] タブを選択し、 **[アプリの登録]** を選択してから、表示される**アプリケーション ID** 番号 (50c464d3-4930-494c-963c-1e951d15360e など) を探します。
* **Azure Active Directory アプリケーションのクライアント シークレット** (必須) – 自分の Azure AD アプリケーションの[クライアント シークレット](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#certificates-and-secrets)を入力します。 この値を探すには、[Azure portal](https://portal.azure.com/) にサインインします。 左側のナビゲーション メニューにある **[Azure Active Directory]** タブを選択し、 **[アプリの登録]** を選んでから、体験版アプリを選択します。 次に、 **[Certificates and secrets]\(証明書とシークレット\)** 、 **[New client secret]\(新しいクライアント シークレット\)** の順に選択し、説明を入力し、 **[Expires]\(有効期限\)** で **[Never]\(なし\)** を選択してから、 **[追加]** を選択します。 このページから離れる前に、必ず値をコピーしておいてください。

続行する前に、 **[下書きの保存]** を選択します。

### <a name="marketplace-listing-optional"></a>Marketplace の一覧 (省略可能)

体験版エクスペリエンスについて説明します。

<!-- The **Test Drive listings** option found under the **Test drive** tab displays the languages (and markets) where your test drive is available (currently English (United States) is the only location available). Additionally, this page displays the status of the language-specific listing and the date/time that it was added. You will need to define the test drive details (description, user manual, videos, etc.) for each language/market. -->

* **説明** (必須) – ユーザーがお客様のオファーを購入するかどうかを決定するのに役立つように、体験版、デモの内容、試用するユーザーの目的、試せる機能、関連情報について説明します。 このフィールドには、最大で 3,000 文字のテキストを入力できます。 
* **アクセス情報** (Azure Resource Manager およびロジックの体験版では必須) – 顧客がこの体験版にアクセスして使用するうえで知っておく必要がある情報を説明します。 お客様のオファーの使用シナリオのほか、顧客が体験版を通じて機能にアクセスするために知っておくべき正確な情報を説明します。 このフィールドには、最大で 10,000 文字のテキストを入力できます。
* **ユーザー マニュアル** (必須) – 体験版エクスペリエンスの詳細なチュートリアル。 ユーザー マニュアルは、体験版のエクスペリエンスで顧客が使用できる内容を正確にカバーし、疑問がある場合に参照するものとして機能する必要があります。 ファイルは PDF 形式にして、アップロード後に名前 (最大 255 文字) を付ける必要があります。
* **ビデオ: ビデオの追加** (省略可能) – ビデオは YouTube または Vimeo にアップロードすることができ、リンクとサムネイル画像 (533 x 324 ピクセル) を使用してここで参照できます。これにより顧客は、オファーの機能を正しく使用する方法やそれらのメリットが際立つシナリオを把握する方法など、体験版への理解を深めるのに役立つ一連の情報を確認できます。
  * **名前** (必須)
  * **アドレス** (YouTube または Vimeo のみ。必須)
  * **サムネイル** (画像ファイルは PNG 形式で、533 x 324 ピクセルである必要があります)。

続行する前に、 **[下書きの保存]** を選択します。

## <a name="publish"></a>発行

オファーの必須セクションをすべて入力したら、ポータルの右上隅にある **[レビューと公開]** を選択します。

オファーの各セクションの完了状態を確認します。
    - *[未開始]* - セクションは着手されておらず、完了する必要があることを意味します。
    - *[未完了]* - 修正が必要なエラーがセクションにあり、追加の情報を入力する必要があることを意味します。 セクションに戻って更新してください。
    - *[完了]* - セクションが完了していることを意味します。必須のデータはすべて入力済みであり、エラーはありません。 オファーを送信するには、オファーのセクションがすべて完了状態でなければなりません。

このオファーを初めて公開する場合は、アプリを理解するのに役立つ補足事項に加え、証明書チームにテストの指示を提供し、確実にアプリが正しくテストされるようにすることができます。

**[送信]** を選択して、公開用のオファーを送信します。 お客様が確認して承認できるようにオファーのプレビュー バージョンが利用可能になったら、それを知らせるメールが Microsoft から届きます。

パートナー センターに戻り、そのオファーに対して **[一般公開する]** を選択して、自分のオファーを一般に公開します (プライベート オファーの場合はプライベート対象ユーザーに公開されます)。

### <a name="errors-and-review-feedback"></a>エラーとフィードバックの確認

発行プロセスの**手動検証**ステップには、オファーの広範なレビューとそれに関連する技術資産 (特に Azure Resource Manager テンプレートの場合) が含まれるため、通常、問題は pull request (PR) のリンクとして示されます。 これらの PR を表示してそれに対応する方法については、「[レビュー フィードバックの処理](./azure-apps-review-feedback.md)」をご覧ください。

1 つまたは複数の公開手順でエラーが発生した場合は、それらを修正してからオファーを再公開してください。

## <a name="next-steps"></a>次のステップ

* [商業マーケットプレースで既存のオファーを更新する](./update-existing-offer.md)
