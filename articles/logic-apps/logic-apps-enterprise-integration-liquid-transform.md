---
title: Liquid 変換を使用して JSON データ変換をする
description: Logic Apps と Liquid テンプレートを使用して、高度な JSON 変換用の変換またはマップを作成します
services: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: estfan, logicappspm
ms.topic: article
ms.date: 04/01/2020
ms.openlocfilehash: d2598dfe9d7972dcb764abf4a1239613a1e8417a
ms.sourcegitcommit: 2d7910337e66bbf4bd8ad47390c625f13551510b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80879175"
---
# <a name="perform-advanced-json-transformations-with-liquid-templates-in-azure-logic-apps"></a>Azure Logic Apps で Liquid テンプレートを使用して高度な JSON 変換を実行する

ロジック アプリ内で **Compose** や **Parse JSON** などのネイティブなデータ操作アクションを使用して、基本的な JSON 変換を実行できます。 高度な JSON 変換を実行するために、柔軟な Web アプリ向けのオープン ソースのテンプレート言語である [Liquid](https://shopify.github.io/liquid/) を使用して、テンプレートまたはマップを作成できます。 Liquid テンプレートでは、JSON 出力の変換方法が定義されます。反復処理、制御フロー、変数などのより複雑な JSON の変換もサポートされます。

ロジック アプリで Liquid 変換を実行する前に、Liquid テンプレートを使用して JSON から JSON へのマッピングを定義し、そのマップを統合アカウントに格納する必要があります。 この記事では、この Liquid テンプレートまたはマップを作成して使用する方法を示します。

## <a name="prerequisites"></a>前提条件

* Azure サブスクリプション。 サブスクリプションをお持ちでない場合には、[無料の Azure アカウントにサインアップ](https://azure.microsoft.com/free/)してください。

* [ロジック アプリの作成方法](../logic-apps/quickstart-create-first-logic-app-workflow.md)に関する基本的な知識

* Basic [統合アカウント](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)

* [Liquid テンプレートの言語](https://shopify.github.io/liquid/)に関する基本的な知識

## <a name="create-liquid-template-or-map-for-your-integration-account"></a>統合アカウント用の Liquid テンプレートまたはマップを作成する

1. この例では、この手順で説明するサンプル Liquid テンプレートを作成します。 Liquid テンプレートでは、[Liquid のフィルター](https://shopify.github.io/liquid/basics/introduction/#filters)を使用できます。これらのフィルターでは、[DotLiquid](https://github.com/dotliquid/dotliquid) と C# 名前付け規則が使用されます。

   > [!NOTE]
   > テンプレートのフィルター名では "*センテンスの大文字小文字を区別*" してください。 そうしないと、フィルターが機能しません。 また、マップには[ファイル サイズ制限](../logic-apps/logic-apps-limits-and-config.md#artifact-capacity-limits)があります。

   ```json
   {%- assign deviceList = content.devices | Split: ', ' -%}
   
   {
      "fullName": "{{content.firstName | Append: ' ' | Append: content.lastName}}",
      "firstNameUpperCase": "{{content.firstName | Upcase}}",
      "phoneAreaCode": "{{content.phone | Slice: 1, 3}}",
      "devices" : [
         {%- for device in deviceList -%}
            {%- if forloop.Last == true -%}
            "{{device}}"
            {%- else -%}
            "{{device}}",
            {%- endif -%}
        {%- endfor -%}
        ]
   }
   ```

1. [Azure portal](https://portal.azure.com) で、検索ボックスに「`integration accounts`」と入力し、 **[統合アカウント]** を選択します。

   !["統合アカウント" を検索](./media/logic-apps-enterprise-integration-liquid-transform/find-integration-accounts.png)

1. 統合アカウントを探して選択します。

   ![統合アカウントを選択する](./media/logic-apps-enterprise-integration-liquid-transform/select-integration-account.png)

1. **[概要]** ウィンドウの **[コンポーネント]** で、 **[マップ]** を選択します。

    !["マップ" タイルを選択](./media/logic-apps-enterprise-integration-liquid-transform/select-maps-tile.png)

1. **[マップ]** ウィンドウで、 **[追加]** を選択して、マップの詳細を入力します。

   | プロパティ | 値 | 説明 | 
   |----------|-------|-------------|
   | **名前** | `JsonToJsonTemplate` | マップの名前 (この例では "JsonToJsonTemplate")。 | 
   | **マップの種類** | **liquid** | マップの種類。 JSON から JSON への変換では、 **[liquid]** を選択する必要があります。 | 
   | **Map** | `SimpleJsonToJsonTemplate.liquid` | 変換に使用する既存の Liquid テンプレートまたはマップ ファイル (この例では "SimpleJsonToJsonTemplate.liquid")。 このファイルを見つけるには、ファイル ピッカーを使用できます。 マップ サイズの制限については、[制限と構成](../logic-apps/logic-apps-limits-and-config.md#artifact-capacity-limits)に関する情報を参照してください。 |
   ||| 

   ![Liquid テンプレートを追加する](./media/logic-apps-enterprise-integration-liquid-transform/add-liquid-template.png)
    
## <a name="add-the-liquid-action-for-json-transformation"></a>JSON 変換のための Liquid アクションを追加する

1. Azure Portal で、次の手順に従って[空白のロジック アプリを作成](../logic-apps/quickstart-create-first-logic-app-workflow.md)します。

1. ロジック アプリ デザイナーで、ロジック アプリに[要求トリガー](../connectors/connectors-native-reqres.md#add-request)を追加します。

1. トリガーで、 **[新しいステップ]** を選択します。 検索ボックスに、フィルターとして「`liquid`」と入力し、アクションとして **[Transform JSON to JSON - Liquid]\(JSON から JSON への変換- Liquid\)** を選択します。

   ![Liquid アクションを見つけて選択する](./media/logic-apps-enterprise-integration-liquid-transform/search-action-liquid.png)

1. **[マップ]** 一覧を開いて、Liquid テンプレート (この例では "JsonToJsonTemplate") を選択します。

   ![マップを選択する](./media/logic-apps-enterprise-integration-liquid-transform/select-map.png)

   マップ一覧が空の場合は、おそらくロジック アプリが統合アカウントにリンクされていません。 
   Liquid テンプレートまたはマップが含まれた統合アカウントにロジック アプリをリンクするには、次の手順に従います。

   1. ロジック アプリのメニューで、 **[ワークフロー設定]** を選択します。

   1. **[統合アカウントを選択してください]** の一覧から統合アカウントを選択し、 **[保存]** をクリックします。

      ![ロジック アプリを統合アカウントにリンクする](./media/logic-apps-enterprise-integration-liquid-transform/link-integration-account.png)

1. ここで、このアクションに **[コンテンツ]** プロパティを追加します。 **[新しいパラメーターの追加]** 一覧を開いて、 **[コンテンツ]** を選択します。

   ![アクションに "コンテンツ" プロパティを追加する](./media/logic-apps-enterprise-integration-liquid-transform/add-content-property-to-action.png)

1. **[コンテンツ]** プロパティ値を設定するには、 **[コンテンツ]** ボックス内をクリックして、動的コンテンツ リストを表示します。 トリガーからの本文コンテンツ出力を表す **[本文]** トークンを選択します。

   !["コンテンツ" プロパティ値の "本文" トークンを選択する](./media/logic-apps-enterprise-integration-liquid-transform/select-body.png)

   作業が完了すると、アクションは次の例のようになります。

   ![[JSON を JSON に変換] アクションが完了](./media/logic-apps-enterprise-integration-liquid-transform/finished-transform-action.png)

## <a name="test-your-logic-app"></a>ロジック アプリをテストする

[Postman](https://www.getpostman.com/postman) などのツールからロジック アプリに JSON 入力を送信します。 ロジック アプリからの変換された JSON 出力は、次の例のようになります。
  
![出力例](./media/logic-apps-enterprise-integration-liquid-transform/example-output-jsontojson.png)

## <a name="more-liquid-action-examples"></a>その他の Liquid アクションの例
Liquid は、JSON 変換のみに使用されるわけではありません。 Liquid を使用して実行できるその他の変換アクションを以下に示します。

* JSON からテキストへの変換
  
  この例で使用する Liquid テンプレートを次に示します。
   
   ``` json
   {{content.firstName | Append: ' ' | Append: content.lastName}}
   ```
   サンプルの入力と出力を次に示します。
  
   ![JSON からテキストへの出力例](./media/logic-apps-enterprise-integration-liquid-transform/example-output-jsontotext.png)

* XML から JSON への変換
  
  この例で使用する Liquid テンプレートを次に示します。
   
   ``` json
   [{% JSONArrayFor item in content -%}
        {{item}}
    {% endJSONArrayFor -%}]
   ```
   サンプルの入力と出力を次に示します。

   ![XML から JSON への出力例](./media/logic-apps-enterprise-integration-liquid-transform/example-output-xmltojson.png)

* XML からテキストへの変換
  
  この例で使用する Liquid テンプレートを次に示します。

   ``` json
   {{content.firstName | Append: ' ' | Append: content.lastName}}
   ```

   サンプルの入力と出力を次に示します。

   ![XML からテキストへの出力例](./media/logic-apps-enterprise-integration-liquid-transform/example-output-xmltotext.png)

## <a name="next-steps"></a>次のステップ

* [Enterprise Integration Pack についての詳細情報](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack について学習する")  
* [マップについての詳細情報](../logic-apps/logic-apps-enterprise-integration-maps.md "Enterprise Integration マップについて学習する")  

