---
title: SAP HANA バックアップのサポート マトリックス
description: この記事では、Azure Backup を使用して Azure VM 上の SAP HANA データベースをバックアップするときにサポートされるシナリオと制限事項について説明します。
ms.topic: conceptual
ms.date: 11/7/2019
ms.openlocfilehash: 8496dc4996cac68535bfe9be30e4b5f72e2d5721
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "79227459"
---
# <a name="support-matrix-for-backup-of-sap-hana-databases-on-azure-vms"></a>Azure VM 上の SAP HANA データベースのバックアップに関するサポート マトリックス

Azure Backup では、Azure への SAP HANA データベースのバックアップがサポートされます。 この記事では、Azure Backup を使用して Azure VM 上の SAP HANA データベースをバックアップするときにサポートされるシナリオと適用される制限事項についてまとめます。

> [!NOTE]
> ログ バックアップの頻度を最大 15 分ごとに設定できるようになりました。 ログ バックアップでは、データベースの完全バックアップが正常に完了した後にのみ、フローが開始されます。

## <a name="scenario-support"></a>シナリオのサポート

| **シナリオ**               | **サポートされている構成**                                | **サポートされていない構成**                              |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **トポロジ**               | Azure Linux VM 実行されている SAP HANA のみ                    | HANA ラージ インスタンス (HLI)                                   |
| **地域**                   | **一般公開:**<br> **アメリカ** – 米国中部、米国東部 2、米国東部、米国中北部、米国中南部、米国西部 2、米国中西部、米国西部、カナダ中部、カナダ東部、ブラジル南部 <br> **アジア太平洋** – オーストラリア中部、オーストラリア中部 2、オーストラリア東部、オーストラリア南東部、東日本、西日本、韓国中部、韓国南部、東アジア、東南アジア、インド中部、インド南部、インド西部、中国東部、中国北部、中国東部 2、中国北部 2 <br> **ヨーロッパ** – 西ヨーロッパ、北ヨーロッパ、フランス中部、英国南部、英国西部、ドイツ北部、ドイツ中西部、スイス北部、スイス西部、中央スイス北部 <br> **アフリカ/中東** – 南アフリカ北部、南アフリカ西部、アラブ首長国連邦北部、アラブ首長国連邦中部  <BR>  **Azure Government リージョン** | フランス南部、ドイツ中部、ドイツ北東部、US Gov アイオワ |
| **OS のバージョン**            | SLES 12 SP2、SP3、または SP4。SLES 15 SP1                              | RHEL                                                |
| **HANA のバージョン**          | HANA 1.x の場合は SDC、SPS04 Rev 46 以下の HANA 2.x の場合は MDC       | -                                                            |
| **HANA のデプロイメント**       | 単一の Azure VM 上の SAP HANA - スケールアップのみ。 <br><br> 高可用性のデプロイでは、2 つの異なるマシン上の両方のノードが、個別のデータ チェーンを持つ個々のノードとして扱われます。               | スケールアウト <br><br> 高可用性のデプロイでは、バックアップはセカンダリ ノードに自動的にフェールオーバーされません。 バックアップの構成は、ノードごとに個別に行う必要があります。                                           |
| **HANA インスタンス**         | 単一の Azure VM 上の単一の SAP HANA インスタンス – スケールアップのみ | 単一の VM 上の複数の SAP HANA インスタンス                  |
| **HANA データベースの種類**    | 1\.x の場合は SDC (Single Database Container)、2.x の場合は MDC (Multi-Database Container) | HANA 1.x での MDC                                              |
| **HANA データベースのサイズ**     | HANA によって報告された 2 TB の完全バックアップサイズ                   |                                                              |
| **バックアップの種類**           | 完全バックアップ、差分バックアップ、ログ バックアップ                          | 増分、スナップショット                                       |
| **復元の種類**          | サポートされている復元の種類については、SAP HANA ノート [1642148](https://launchpad.support.sap.com/#/notes/1642148) を参照してください |                                                              |
| **バックアップの制限**          | SAP HANA インスタンスごとに最大 2 TB の完全バックアップ サイズ         |                                                              |
| **特殊な構成** |                                                              | SAP HANA + Dynamic Tiering <br>  LaMa を使用した複製        |

------

> [!NOTE]
> SAP HANA ネイティブ クライアント (SAP HANA Studio/Cockpit/DBA Cockpit) からのバックアップおよび復元操作は、現在サポートされていません。

## <a name="next-steps"></a>次のステップ

* [Azure VM で稼働している SAP HANA データベースをバックアップする](https://docs.microsoft.com/azure/backup/backup-azure-sap-hana-database)方法を学習する
* [Azure VM で稼働している SAP HANA データベースを復元する](https://docs.microsoft.com/azure/backup/sap-hana-db-restore)方法を学習する
* [Azure Backup を使用してバックアップされた SAP HANA データベースを管理する](sap-hana-db-manage.md)方法を学習する
* [SAP HANA データベースのバックアップ時に発生する一般的な問題をトラブルシューティングする](https://docs.microsoft.com/azure/backup/backup-azure-sap-hana-database-troubleshoot)方法を学習する
