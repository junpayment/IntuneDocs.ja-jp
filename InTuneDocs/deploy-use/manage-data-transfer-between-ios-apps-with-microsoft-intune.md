---
title: "iOS アプリ間のデータ転送を管理する | Microsoft Intune"
description: "このトピックを使用すると、iOS の開く機能とモバイル アプリ管理ポリシーを使用してアプリ間のデータ転送を管理する方法を把握できます。"
keywords: 
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.date: 11/14/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 3a4515c1-b325-4ac1-9f0a-45ac27e00681
ms.reviewer: jeffgilb
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 87e37cd8334ddb9331c0662b691545cd0ab0553a
ms.openlocfilehash: 94163d5f303b293da2301b81a5c96f6c9c2e5e5d


---

# <a name="manage-data-transfer-between-ios-apps-with-microsoft-intune"></a>Microsoft Intune を使用して iOS アプリ間のデータ転送を管理する
## <a name="manage-ios-apps"></a>iOS アプリを管理する
会社データの保護には、ファイル転送を管理対象のアプリに限定する処理も含まれます。  iOS アプリは次の方法で管理できます。

-   アプリ (**ポリシーで管理されている**アプリと呼ばれます) の MAM ポリシーを構成して、会社データの損失を回避します。

-   また、アプリは **MDM チャネル**から展開して管理することもできます。  これには、デバイスが MDM ソリューションに登録されていることが必要です。 これらは**ポリシーで管理されている**アプリであるか、またはその他の管理対象アプリである必要があります。

iOS デバイスの **Open In Management** 機能を使用すると、**MDM チャネル**を使用して展開されているアプリ間でのみファイル転送が行われるよう制限できます。 Open In Management の制限は、構成設定で設定され、MDM ソリューションを使用して展開されます。  展開されているアプリをユーザーがインストールすると、管理者が設定した制限が適用されます。
##  <a name="using-mam-with-ios-apps"></a>iOS アプリで MAM を使用する
モバイル アプリ管理 (MAM) ポリシーは、iOS の **Open in Management** 機能と共に使用して、以下のように会社データを保護できます。

-   **MDM ソリューションで管理されていない従業員所有のデバイス:** MAM ポリシー設定を **[アプリで管理対象アプリへのデータ転送のみ許可する]**に設定できます。 保護されたファイルをポリシーで管理されていないアプリでアプリで開くと、エンドユーザーはファイルを読み取れません。

-   **Intune で管理されているデバイス:** Intune で登録したデバイスの場合、MAM ポリシーを使用するアプリと、他の Intune で展開された管理対象の iOS アプリの間で自動的にデータを転送できるようになります。 MAM ポリシーを使用するアプリ間でデータを転送できるようにするには、**[アプリで管理対象アプリへのデータ転送のみ許可する]** 設定を有効にします。 **Open in Management** 機能を使用して、Intune で展開されているアプリ間のデータ転送を制御できます。   

-   **サード パーティの MDM ソリューションで管理されているデバイス:** iOS の **Open In Management** 機能を使用して、データ転送が管理対象のアプリに対してのみ行われるよう制限できます。
サードパーティの MDM ソリューションを使用して展開するアプリを、Intune で構成した MAM ポリシーとも関連付けるには、「[ユーザー UPN 設定を構成する](#configure-user-upn-setting)」のチュートリアルに従ってユーザー UPN 設定を構成する必要があります。  アプリがユーザー UPN 設定を使用して展開されている場合、エンドユーザーが職場アカウントを使用してサインインすると、MAM ポリシーがアプリに適用されます。

> [!IMPORTANT]
> ユーザー UPN 設定は、サード パーティの MDM によって管理されるデバイスに展開されたアプリに対してのみ必要です。  Intune の管理対象デバイスの場合は、この設定は必要ありません。

## <a name="configure-user-upn-setting"></a>ユーザー UPN 設定を構成する
この構成は、サード パーティの MDM ソリューションによって管理されているデバイスに必要となります。 以下に示す手順では、UPN 設定の一般的な実装方法と、その結果として得られるのエンドユーザー エクスペリエンスを示しています。


1.  Azure ポータルで、iOS プラットフォームの[モバイル アプリ管理ポリシーを構成します](create-and-deploy-mobile-app-management-policies-with-microsoft-intune.md)。 企業の要件に合わせてポリシー設定を構成し、このポリシーを使用するアプリを選択します。

2.  手順 3 と 4 で説明した設定を使用して、**サードパーティの MDM ソリューションで**管理するアプリと電子メール プロファイルを展開します。

3.  key=IntuneMAMUPN, Value=<username@company.com> [例: ‘IntuneMAMUPN’, ‘jondoe@microsoft.com’]

4.  Open In Management ポリシーを登録済みデバイスに展開します。

### <a name="example-end-user-experience"></a>エンド ユーザー エクスペリエンスの例

1.  エンド ユーザーは、デバイスに Microsoft Word アプリをインストールします。

2.  エンド ユーザーが管理対象のネイティブ メール アプリを起動して、自分の電子メールにアクセスします。

3.  エンド ユーザーがネイティブ メールから Microsoft Word でドキュメントを開こうとします。

4.  Word アプリが起動するとき、エンド ユーザーは職場アカウントを使用してログインするよう求められます。  プロンプトが表示されたときにエンド ユーザーが入力するこの職場アカウントは、Microsoft Word アプリのアプリ構成設定で構成し、指定したアカウントと一致する必要があります。

    > [!NOTE]
    > エンド ユーザーは、私用で Word アプリを使用するときに、個人の作業に使用し、MAM ポリシーの影響を受けない個人アカウントを Word に追加することができます。

5.  ログインが成功すると、アプリのポリシー設定が Word アプリに適用されます。

6.  これでデータ転送が成功し、ドキュメントにはアプリで企業 ID のタグが付けられます。 また、データが作業コンテキスト内で処理されるときには、ポリシー設定が適切に適用されます。

### <a name="see-also"></a>関連項目
[Microsoft Intune でモバイル アプリケーション管理ポリシーを使用してデータを保護する](protect-app-data-using-mobile-app-management-policies-with-microsoft-intune.md)



<!--HONumber=Dec16_HO2-->

