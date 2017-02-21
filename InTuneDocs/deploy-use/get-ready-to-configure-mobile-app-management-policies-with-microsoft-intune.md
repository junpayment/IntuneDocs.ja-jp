---
title: "MAM ポリシーの前提条件 | Microsoft Docs"
description: "このトピックでは、モバイル アプリ管理ポリシーを作成する前にユーザーを設定するための前提条件について説明します。"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 11/29/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 7e6a85e7-e007-41b6-9034-64d77f547b87
ms.reviewer: joglocke
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9e208608d50c9b5f7fe66743de0d3c7e741dbfbd
ms.openlocfilehash: cb525deb240668c0f0f14b19f39eb1226e338629


---

# <a name="get-ready-to-configure-mobile-app-management-policies-on-the-azure-portal"></a>Azure ポータルでモバイル アプリ管理ポリシーを作成し、展開する

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

このトピックでは、Azure ポータルでモバイル アプリ管理 (MAM) ポリシーを作成する**前に**完了しておく必要がある前提条件と手順について説明します。

Intune MAM ポリシーで会社のデータを守る方法については、「[Protect apps and data using mobile app management policies](protect-apps-and-data-with-microsoft-intune.md)」 (モバイル アプリ管理ポリシーを利用してアプリとデータを保護する) を参照してください。

## <a name="what-is-the-azure-portal"></a>Azure ポータルとは?

Azure ポータルは MAM ポリシーを作成するための新しい管理コンソールです。 Azure Portal では、次の MAM シナリオをサポートします。
- Intune に登録されたデバイス
- 別のモバイル デバイス管理 (MDM) ソリューションによって管理されるデバイス
- MDM ソリューションで管理されないデバイス (BYOD)

現在のところ、**Intune 管理者コンソール**と **Azure Portal **の両方で MAM ポリシーを構成できます。  次の点を考慮します。

* **Azure Portal ** で作成するポリシーは、上記の**すべての MAM シナリオ**でサポートされます。 **Intune 管理者コンソール**は、**Intune で登録し、管理するデバイス**のポリシー作成にのみ対応しています。

* **新しい設定**は **Azure Portal **にのみ追加できるため、一部の MAM ポリシー設定は Intune 管理者コンソールに表示されない場合があります。

* Intune 管理コンソールと Azure ポータルの**両方**で MAM ポリシーを作成した場合、**Azure ポータルのポリシーがアプリに適用され、ユーザーに展開されます**。
    * Intune 管理コンソールで作成した MAM ポリシーを Azure ポータルにインポートすることはできません。  Azure ポータルで MAM ポリシーを作成し直す必要があります。


* アプリやアプリ構成ポリシーの展開などの、**他のアプリ管理機能**は、現在のところ、**Intune 管理コンソール**でのみ利用できます。


初めて Azure Portal を使用する場合は、「[Azure Portal の Microsoft Intune MAM ポリシー対応](azure-portal-for-microsoft-intune-mam-policies.md)」で Azure Portal の基本を確認してください。

Intune 管理コンソールで MAM ポリシーを作成する方法については、「[Microsoft Intune コンソールでモバイル アプリケーション管理ポリシーを構成して展開する](configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console.md)」を参照してください。


##  <a name="supported-platforms"></a>サポートされているプラットフォーム
- iOS 8.1 以降
- Android 4 以降

>[!NOTE]
>Windows デバイスでは、これらのモバイル アプリケーション管理ポリシーはサポートされていません。 ただし、Intune で Windows 10 デバイスを登録すると、同様の機能を提供する Windows 情報保護を使用できます。 詳細については、「[Protect your enterprise data using Windows Information Protection (WIP)](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/protect-enterprise-data-using-wip)」 (Windows 情報保護 (WIP) を使用してエンタープライズ データを保護する) を参照してください。

##  <a name="supported-apps"></a>サポートされているアプリ
* **Microsoft アプリ:** これらのアプリには Intune アプリ SDK が組み込まれているので、MAM ポリシーを適用する前に必要な処理はありません。
サポートされている Microsoft アプリの完全な一覧については、Microsoft Intune アプリケーション パートナー ページの [Microsoft Intune モバイル アプリケーション ギャラリー](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-apps)を参照してください。 アプリをクリックし、サポートされるシナリオ、プラットフォーム、アプリのマルチ ID 対応について確認してください。

* **社内で構築した基幹業務アプリ:** MAM ポリシーを適用する前に、Intune アプリ SDK を含めるようにアプリを準備する必要があります。

  * Intune で管理されているデバイスについては、「[Decide how to prepare apps for MAM](decide-how-to-prepare-apps-for-mobile-application-management-with-microsoft-intune.md)」 (MAM 用にアプリを準備する方法を決める) を参照してください。

  * 従業員が所有するデバイスなど管理対象ではないデバイスや、別のモバイル デバイス管理ソリューションで管理されているデバイスの場合は、「[Microsoft Intune に登録されていないデバイスの基幹業務アプリとデータを保護する](protect-line-of-business-apps-and-data-on-devices-not-enrolled-in-microsoft-intune.md)」を参照してください。

## <a name="prerequisites"></a>必要条件

-   **Microsoft Intune サブスクリプション**。 MAM ポリシーが適用されているアプリを入手するには、[!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] ライセンスが必要です。
デバイスを管理するために現在 [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] を使用している場合、既に [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] サブスクリプションを所有していることになります。 Enterprise Mobility Suite (EMS) ライセンスを購入している場合も、[!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] サブスクリプションを所有しています。 MAM 機能を調べるために [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] を試してみる場合は、試用アカウントを [Microsoft Intune Web ページ](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/)から取得できます。

    自分が [!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] サブスクリプションを所有しているかどうかを確認するには、Office ポータルの**課金情報**のページをご覧ください。  サブスクリプションを所有している場合は、[!INCLUDE[wit_nextref](../includes/wit_nextref_md.md)] が **Active** になっているはずです。

-   **Office 365 サブスクリプション**。これは、以下で必要となります。

  - 複数の ID をサポートするアプリに MAM ポリシーを適用する。

  - SharePoint Online および Exchange Online 作業アカウントを作成する。 Exchange On-Premises と SharePoint On-Premises はサポートされていません。

-   **Skype for Business Online の先進認証の設定**。 詳細については、「[Enable modern authentication](http://social.technet.microsoft.com/wiki/contents/articles/34339.skype-for-business-online-enable-your-tenant-for-modern-authentication.aspx)」 (先進認証の有効化) をご覧ください。


- ユーザーを作成するための Azure Active Directory (Azure AD)。 Azure AD では、ユーザーがアプリを開いて作業用の資格情報を入力するときに、ユーザーを認証します。

    > [!NOTE]
    > ユーザー グループは Azure AD で設定する必要があります。 Azure ポータルで Intune ユーザー グループを利用して MAM ポリシーを展開することはできません。

### <a name="create-users-and-assign-microsoft-intune-licenses"></a>ユーザーの作成と Microsoft Intune ライセンスの割り当て

1.  管理者資格情報で [Office ポータル](http://portal.office.com)にサインインします。

2.  [Intune の評価ガイド](https://docs.microsoft.com/en-us/intune/understand-explore/get-started-with-a-30-day-trial-of-microsoft-intune)の、**Intune の 30 日間評価版の完了手順**のセクションにある説明に従ってユーザーを追加して、Intune ライセンスを割り当てます。 ユーザーが Office ポータル、Azure AD ポータル、Azure ポータルにアクセスできるようにするには、**全体管理者ロール**をユーザーに割り当てます。

5.  MAM ポリシーは、Azure Active Directory のユーザー グループに展開されます。 MAM ポリシーのユーザー グループを作成するには、「[Create groups to organize evaluation subscription users and devices](https://docs.microsoft.com/en-us/intune/understand-explore/get-started-with-a-30-day-trial-of-microsoft-intune-step-3)」 (評価版サブスクリプションのユーザーとデバイスを編成するグループを作成する) の「**ユーザー グループの作成**」セクションの説明にあるようにユーザー グループを作成します。

### <a name="assign-roles-to-non-global-admin-users"></a>グローバル管理者でないユーザーにロールを割り当てる

全体管理者には [Azure ポータル](https://portal.azure.com)へのアクセス権があります。  グローバル管理者ではないユーザーもポリシーを構成して他のモバイル アプリ管理タスクを実行できるようにする場合は、ユーザーに共同作成者ロールを割り当てることができます。 詳細については、「[Use role assignments to manage access to your Azure subscription resources](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-configure/)」 (ロールの割り当てを利用し、Azure サブスクリプション リソースへのアクセスを管理する) を参照してください。



次の表に、管理ユーザーに対して割り当てることができるロールとアクセス許可の一覧を示します。



|||
|--|----|
|**ロール**|**アクセス許可**|
|全体管理者 (Office 365 ポータル)|Office 365 ポータルと Azure AD ポータルへのアクセス。<br /><br />Azure ポータルへのアクセス (ロール管理タスクとモバイル アプリ管理タスクの両方が可能)。|
|所有者 (Azure ポータル)|Azure ポータルへのアクセス (ロール管理タスクとモバイル アプリ管理タスクの両方が可能)。|
|共同作成者 (Azure ポータル)|Azure ポータルへのアクセス (モバイル アプリ管理タスクのみ実行可能)。|




## <a name="next-steps"></a>次のステップ
[Microsoft Intune でのモバイル アプリ管理ポリシーの作成および展開](create-and-deploy-mobile-app-management-policies-with-microsoft-intune.md)



<!--HONumber=Dec16_HO3-->

