---
title: Intune App SDK の利点
titlesuffix: Microsoft Intune
description: Intune アプリ SDK は、iOS プラットフォームと Android プラットフォームの両方で利用でき、Microsoft Intune を使ったモバイル アプリ管理機能が有効になります。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/15/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: cd9f05e7-26e6-45e0-8d38-67d8232b1cae
ms.reviewer: aanavath
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 33e1cb6953891fa6d62841d10bc8011768938ee1
ms.sourcegitcommit: 34e96e57af6b861ecdfea085acf3c44cff1f3d43
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
# <a name="intune-app-sdk-overview"></a>Intune App SDK の概要
iOS と Android の両方で使用可能な Intune App SDK で、Intune アプリ保護ポリシーに対してご使用のアプリを有効にすることができます。 アプリの開発者が必要なコード変更が最小限に抑えられます。 SDK の機能の多くは、アプリの動作を変更せずに利用できます。 エンド ユーザーと IT 管理者のエクスペリエンスを向上させるために、API を利用してアプリの動作をカスタマイズし、アプリ側の処理が必要な機能を実現できます。

アプリ保護ポリシーに対してアプリを有効にしたら、IT 管理者はそのポリシーを展開し、アプリ内の会社のデータを保護することができます。

## <a name="app-protection-features"></a>アプリ保護機能

SDK で有効にできる Intune アプリ保護機能の例を以下に示します。

### <a name="control-users-ability-to-move-corporate-files"></a>ユーザーに会社のファイルの移動を許すかどうかを制御
IT 管理者は、アプリ内の職場または学校のデータを移動できる場所を制御できます。 たとえば、アプリで会社のデータをクラウドにバックアップできないようにするポリシーを展開できます。

### <a name="configure-clipboard-restrictions"></a>クリップボードの制限の構成
IT 管理者は、Intune の管理対象アプリにおけるクリップボードの動作を構成できます。 たとえば、エンド ユーザーがアプリからデータを切り取るかコピーして、管理されていない個人アプリに貼り付けられないようにするポリシーを展開できます。

### <a name="enforce-encryption-on-saved-data"></a>保存データへの暗号化の適用
IT 管理者は、アプリによってデバイスに保存されたデータを確実に暗号化するポリシーを適用できます。

### <a name="remotely-wipe-corporate-data"></a>会社のデータのリモート ワイプ
IT 管理者は、Intune で管理されたアプリから会社のデータをリモートでワイプできます。 これは ID ベースの機能で、エンドユーザーの社内 ID に関連付けられたファイルのみが削除されます。 この機能を実行するには、アプリによる処理が必要です。 アプリは、ワイプする必要のある ID を、ユーザー設定を基に指定できます。 指定されたユーザー設定がアプリにない場合、既定の動作では、アプリケーションのディレクトリがワイプされ、エンド ユーザーにアクセスが削除されたことが通知されます。

### <a name="enforce-the-use-of-a-managed-browser"></a>管理対象ブラウザーの使用を強制
IT 管理者は、アプリ内の Web リンクを開くときに、[Intune Managed Browser アプリ](/intune-classic/deploy-use/manage-internet-access-using-managed-browser-policies)の使用を強制することができます。 この機能により、企業環境で表示されるリンクが Intune で管理されたアプリのドメイン内に維持されることが保証されます。

### <a name="enforce-a-pin-policy"></a>暗証番号 (PIN) ポリシーの適用
IT 管理者は、エンド ユーザーがアプリ内の企業データにアクセスする前に PIN の入力を求めることができます。 これにより、アプリを使用するユーザーが、職場または学校のアカウントで最初にサインインしたユーザーであることが保証されます。 エンド ユーザーが自分の PIN を構成するときに、Intune App SDK は Azure Active Directory を使用して、エンド ユーザーの資格情報を登録されている Intune アカウントに照らして確認します。

### <a name="require-users-to-sign-in-with-work-or-school-account-for-app-access"></a>ユーザーはアプリにアクセスするために職場または学校のアカウントでサインインする必要がある
IT 管理者は、アプリへのアクセスに、職場または学校のアカウントを使用してサインインすることをユーザーに求めることができます。 Intune App SDK は Azure Active Directory を使用してシングル サインオン エクスペリエンスを提供します。1 回入力した資格情報が、それ以降のログインで再利用されます。 Azure Active Directory とフェデレーションしている ID 管理ソリューションの認証もサポートしています。

### <a name="check-device-health-and-compliance"></a>デバイスのヘルスとコンプライアンスの確認
エンド ユーザーがアプリにアクセスする前に、IT 管理者は、デバイスのヘルスと Intune ポリシーに対するコンプライアンスを確認できます。 iOS では、このポリシーにより、デバイスがジェイルブレイクされているかどうかを確認できます。 Android では、このポリシーにより、デバイスがルート化されているかどうかを確認できます。

### <a name="multi-identity-support"></a>複数 ID のサポート
複数 ID のサポートは、ポリシーで管理された (会社) アカウントと、管理されていない (個人) アカウントとが 1 つのアプリに共存できるようにする SDK の機能です。

たとえば、多くのユーザーは、iOS 用および Android 用の Office モバイル アプリで、会社と個人の両方のメール アカウントを構成しています。 ユーザーが会社のアカウントでデータにアクセスする場合、IT 管理者はアプリ保護ポリシーが確実に適用されるようにする必要があります。 一方、ユーザーが個人用のメール アカウントにアクセスする場合、データは IT 管理者の管理下にありません。 Intune App SDK では、アプリの会社 ID **のみ**をアプリ保護ポリシーの対象として、これを実現します。

複数 ID 機能は、個人と職場の両方のアカウントをサポートするストア アプリを使用することで組織が直面しているデータ保護の問題を解決するのに役立ちます。
 
### <a name="app-protection-without-device-enrollment"></a>デバイス登録が不要なアプリの保護

>[!IMPORTANT]
>デバイス登録のない Intune アプリ保護は、Intune App ラッピング ツール、Intune App SDK for Android、Intune App SDK for iOS、Intune App SDK Xamarin バインディングで利用できます。

個人用デバイスを使用するユーザーの多くは、モバイル デバイス管理 (MDM) プロバイダーを使用して自分の個人用デバイスを登録せずに、会社のデータにアクセスしたいと考えます。 MDM 登録にはデバイスのグローバル制御が必要になるため、多くの場合、ユーザーは自分の個人用デバイスの制御を会社に任せることをためらいます。

デバイス登録が不要なアプリの保護を使用すると、Microsoft Intune サービスでアプリ保護ポリシーを直接アプリに展開することができ、ポリシーの展開でデバイス管理チャネルに依存する必要がなくなります。
