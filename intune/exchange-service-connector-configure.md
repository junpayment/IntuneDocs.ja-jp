---
title: Exchange Online 用の Intune Exchange Connector
titleSuffix: ''
description: Exchange ActiveSync モバイル デバイス管理 (MDM) をサポートするために、Intune を Office 365 Exchange サービスに接続する。
keywords: ''
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 05/01/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
ms.reviewer: muhosabe
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 640d1a5cbd785248cb309bc250c95631295955b3
ms.sourcegitcommit: 71497f0215fc8bed454ac318b0548b1281a8fe0f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2018
---
# <a name="configure-the-exchange-service-connector-for-intune-and-exchange-online"></a>Intune および Exchange Online 用に Exchange サービス コネクタを構成する

この記事では、Microsoft Intune サービスを Exchange Online サービスまたは新しい Exchange Online Dedicated サービスに接続する方法を説明します。 Exchange Online Dedicated 環境が**新しい**バージョンか**従来の**バージョンかを確認するには、アカウント マネージャーに問い合わせてください。

## <a name="service-to-service-connector-requirements"></a>Service to Service Connector の要件
**Service to Service Connector** は、Exchange Online または Exchange Online Dedicated のみをサポートします。また、オンプレミス インフラストラクチャの要件はありません。


|              要件               |                                                                                                            詳細情報                                                                                                            |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Online が構成済みで実行中である |                                                                                 [Exchange Online](https://technet.microsoft.com/library/jj200580.aspx)                                                                                 |
|   モバイル デバイス管理機関   |                                                       [モバイル デバイスの管理機関を Microsoft Intune に設定します。](mdm-authority-set.md)                                                       |
|       Microsoft Exchange のバージョン       |                                                                                      Exchange Online サービスまたは新しい Exchange Online Dedicated サービス                                                                                      |
|    Active Directory の同期    | Intune Connector を使用できるようにするには、[Active Directory の同期をセットアップ](/intune/users-add)して、ローカル ユーザーとセキュリティ グループが Azure Active Directory のインスタンスと同期されるようにする必要があります。 |

### <a name="exchange-cmdlet-requirements"></a>Exchange コマンドレットの要件

Intune Exchange サービス コネクタが使用する Exchange Online ユーザー アカウントも作成する必要があります。 アカウントには、次の必須の Windows PowerShell Exchange コマンドレットを実行するための権限が必要です。

 - Get-ActiveSyncOrganizationSettings, Set-ActiveSyncOrganizationSettings
 - Get-MobileDeviceMailboxPolicy、Set-MobileDeviceMailboxPolicy、New-MobileDeviceMailboxPolicy、Remove-MobileDeviceMailboxPolicy
 - Get-ActiveSyncDeviceAccessRule、Set-ActiveSyncDeviceAccessRule、New-ActiveSyncDeviceAccessRule、Remove-ActiveSyncDeviceAccessRule
 - Get-MobileDeviceStatistics
 - Get-MobileDevice
 - Get-ActiveSyncDeviceClass

## <a name="set-up-the-service-to-service-connector"></a>Service to Service Connector を設定します。

1. Exchange 管理者権限と[上記](#exchange-cmdlet-requirements)のコマンドレットのアクセス許可を持つユーザー アカウントで、[Azure portal](http://portal.azure.com) にサインインします。 Microsoft Intune は、現在サインインしているユーザーの電子メール アドレスを使用して、接続をセットアップします。

2. 左側のメニューから **[すべてのサービス]** を選択し、テキスト ボックス フィルターに「**Intune**」と入力します。

3. **[Intune]** を選んで、Microsoft Intune ダッシュボードを開きます。 **[条件付きアクセス]** を選び、**[セットアップ]** で **[Exchange サービス コネクタ]** を選びます。

4.  **[条件付きアクセス - Exchange サービス コネクタ]** ページで、**[Service To Service Connector のセットアップ]** を選びます。 
   
     ![[Service To Service Connector のセットアップ] リンクの選択を示す画像](media/exchange_service_connector.png)

Service to Service Connector は自動的に構成され、Exchange Online 環境または新しい Exchange Online Dedicated 環境と同期されます。

## <a name="validate-your-exchange-connection"></a>Exchange 接続の確認

Exchange Service to Service Connector を正常に構成した後、**[条件付きアクセス - Exchange サービス コネクタ]** ページで Exchange Connector Server の情報を確認します。

**[接続の状態]** と、前回いつ同期が完了したかを確認することもできます。

## <a name="next-steps"></a>次の手順
[Microsoft Intune で Exchange の条件付きアクセスを監視する](conditional-access-exchange-monitor.md)