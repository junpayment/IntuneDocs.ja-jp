---
title: "Zimperium MTD を Microsoft Intune と統合する"
titleSuffix: 
description: "Microsoft Intune で Zimperium Mobile Threat Defense (MTD) ソリューションをセットアップし、モバイル デバイスから会社のリソースへのアクセスを制御する方法。"
keywords: 
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 12/29/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: fada315aad9bce47a3a04286d84e1c7dbdd2ce61
ms.sourcegitcommit: 4db0498342364f8a7c28995b15ce32759e920b99
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="integrate-zimperium-with-intune"></a>Zimperium を Intune と統合する

Zimperium Mobile Threat Defense ソリューションを Intune と統合するには、次の手順をすべて実行します。

## <a name="before-you-begin"></a>始める前に

> [!NOTE]
> 次の手順はすべて、[Zimperium MTD コンソール](https://staging2-console.zimperium.com)で実行します。

Zimperium と Intune の統合を始める前に、次のサブスクリプションと資格情報があることを確認します。

-   Microsoft Intune サブスクリプション

-   次のアクセス許可を付与する Azure Active Directory 管理者資格情報:

    -   サインインしてユーザー プロファイルを読み取る

    -   サインインしたユーザーとしてディレクトリにアクセスする

    -   ディレクトリ データの読み込み

    -   Intune にデバイス情報を送信する

-   Zimperium MTD コンソールにアクセスするための管理者資格情報。

### <a name="zimperium-app-authorization"></a>Zimperium アプリの承認

Zimperium アプリ承認プロセスは以下で構成されます。

-   Zimperium サービスがデバイスの正常性状態に関する情報を Intune に通知できるようにします。

-   Zimperium は、Azure Active Directory 登録グループ メンバーシップと同期してデバイスのデータベースを設定します。

-   Zimperium 管理者コンソールが Azure AD シングル サインオン (SSO) を使用できるようにします。

-   Zimperium アプリが Azure AD SSO を使用してサインインできるようにします。

## <a name="to-set-up-zimperium-integration"></a>Zimperium の統合を設定するには

1.  [Zimperium MTD コンソール](https://staging2-console.zimperium.com)に移動し、資格情報を使用してサインインします。

2.  左のメニューから **[Management]\(管理\)** を選択します。

3.  **[MDM settings]\(MDM の設定\)** タブを選択します。

4.  **[Add MDM]\(MDM の追加\)** を選択し、**[MDM provider]\(MDM プロバイダー\)** 一覧から **[Microsoft Intune]** を選択します。

5.  Microsoft Intune を MDM サービスとして設定すると、**[Microsoft Intune Configuration]\(Microsoft Intune 構成\)** ウィンドウが開くので、**[Zimperium zConsole]** と **[zIPS iOS and Android apps]\(zIPS iOS および Android アプリ\)** オプションのそれぞれに **[Azure Active Directory を追加する]** を選択します。これらのオプションは Zimperium が Azure AD シングル サインオンを使用して Intune および Azure AD と通信することを承認するものです。

    > [!IMPORTANT]
    > Intune との統合プロセスを完了するには、Zimperium zConsole、zIPS iOS および Android アプリを追加する必要があります。

6.  **[Accept\(承認\)]** を選択して、Zimperium アプリが Intune および Azure Active Directory と通信することを承認します。

7.  **[Zimperium zConsole]** および **[zIPS iOS and Android]\(zIPS および Android\)** アプリを Azure AD に追加したら、Azure AD セキュリティ グループを追加します。 これで、Zimperium が Azure AD セキュリティ グループとそのサービスを同期できるようになります。

8.  **[Finish]\(完了\)** を選択して構成を保存し、最初の Azure AD セキュリティ グループの同期を開始します。

## <a name="next-steps"></a>次の手順

-   [Zimperium アプリを設定する](mtd-apps-ios-app-configuration-policy-add-assign.md)
