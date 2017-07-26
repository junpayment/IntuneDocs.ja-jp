---
title: "Intune デバイス インベントリの表示"
titleSuffix: Intune on Azure
description: "Intune で管理するデバイスを表示して、ハードウェアとインストールされているアプリを把握する方法について説明します。\""
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 07/11/2017
ms.topic: get-started-article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 3618c5ee0b4a7ff0e7b6a4d6ed58f77a2af0ba66
ms.sourcegitcommit: fb17b59f4aa2b994b149fcc6d32520f74b0de6a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2017
---
# <a name="how-to-view-intune-device-inventory"></a>Intune デバイス インベントリを表示する方法


[!INCLUDE[azure_portal](./includes/azure_portal.md)]

**デバイス** ワークロードでは、ハードウェアの機能やインストールされているアプリなど、管理するデバイスを把握することができます。 

デバイス インベントリを表示するには、以下を行います。

1. Azure ポータルにサインインします。
2. **[その他のサービス]** > **[監視 + 管理]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[デバイス]** を選択します。

ここで、次のいずれかのオプションを選択します。

- **[概要]** 登録したデバイスと、各デバイスで実行されているオペレーティング システムについての情報が得られます。
- **[管理]** - **[すべてのデバイス]** を選択すると、管理しているすべてのデバイスの一覧が表示されます。
    一覧からいずれかのデバイスを選択すると、[<*デバイス名*> **概要]** ブレードが開き、以下のいずれかを選択できます。
    - **[概要]** - デバイスの名前、所有者、BYOD デバイスかどうか、最終チェックイン日時など、デバイスについての一般情報が表示されます。
    ![デバイスの概要](./media/device-overview.png)
    - **[ハードウェア]** - デバイスの記憶域の空き容量、モデル、製造元など、デバイスについてのさらに詳細な情報が表示されます。
    ![管理対象デバイスのハードウェア インベントリ](./media/hardware-inventory.png)
    - **[検出されたアプリ]** - Intune でデバイスにインストールされていると判断されたすべてのアプリの一覧が表示されます。
    ![[検出されたアプリ] のノード](./media/detected-applications.png)
    


    - **[デバイスのポリシー準拠]** - デバイスに割り当てられているすべてのコンプライアンス ポリシーのコンプライアンス対応状態が表示されます。
    - **[デバイス構成]** - デバイスに割り当てられているすべてのデバイス構成ポリシーのコンプライアンス対応状態が表示されます。
- **[監視]** - **[デバイス アクション]** を選択すると、管理対象のデバイスで実行されたデバイス アクションの一覧と、その現在の状態が表示されます。
- **[セットアップ]** > **[TeamViewer Connector]** - TeamViewer のソフトウェアを使用して、デバイスのリモート管理を構成できます。 詳細については、「[Intune 管理対象の Android デバイスにリモート アシスタンスを提供する](/intune/device-profile-android-teamviewer)」を参照してください。

>[!NOTE]
> Intune は会社所有のデバイスでのみアプリのインベントリを収集します。 個人のデバイスではアプリがインベントリされません。 Windows 10 の PC の場合、最新のアプリのインベントリのみが会社所有のデバイスで収集されます。 Intune は、デバイス上の Win32 アプリに関する情報を収集しません。