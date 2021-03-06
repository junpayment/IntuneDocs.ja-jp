---
title: iOS アプリ保護ポリシー設定
titlesuffix: Microsoft Intune
description: このトピックでは、iOS デバイスのアプリ保護ポリシー設定について説明します。
keywords: ''
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 05/17/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 0f8b08f2-504c-4b38-bea2-b8a4ef0526b8
ms.reviewer: andcerat
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 26c2b00c1ac720ae3032b5b896489b9fe2972510
ms.sourcegitcommit: 698bd1488be3a269bb88c077eb8d99df6e552a9a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
#  <a name="ios-app-protection-policy-settings"></a>iOS アプリ保護ポリシー設定
[!INCLUDE [azure_portal](./includes/azure_portal.md)]

このトピックで説明するポリシーの設定は、Azure Portal の **[ポリシーの追加]** > **[設定]** ブレードでアプリ保護ポリシー用に[構成することができます](app-protection-policies.md)。

ポリシー設定には、データ再配置設定とアクセス設定の 2 つのカテゴリがあります。 このトピックの "***ポリシーで管理されているアプリ***" という用語は、アプリ保護ポリシーで構成されるアプリを示します。

##  <a name="data-relocation-settings"></a>データ再配置設定

| Setting | 使用する方法 | 既定値 |
|------|------|------|
| **iTunes と iCloud でのバックアップを禁止する** | このアプリが職場または学校のデータを iTunes および iCloud にバックアップできないようにするには、**[はい]** を選びます。 このアプリが職場または学校のデータを iTunes および iCloud にバックアップできるようにするには、**[いいえ]** を選びます。| はい |
| **[アプリで他のアプリへのデータ転送を許可する]** | このアプリからデータを受け取ることができるアプリを指定します。 <ul><li> **ポリシーで管理されているアプリ**: 他のポリシーで管理されているアプリへの転送のみを許可します。</li> <li>**すべてのアプリ**: すべてのアプリへの転送を許可します。 </li> <li>**なし**: 他のポリシーで管理されているアプリを含め、アプリへのデータ転送を許可しません。</li></ul> さらに、このオプションを **[ポリシーで管理されているアプリ]** または **[なし]** に設定すると、Spotlight 検索を使用してアプリ内のデータを検索できる iOS 9 の機能がブロックされます。 <br><br> Intune でデータ転送先として既定で許可される可能性のある除外対象アプリとサービスがいくつかあります。 さらに、Intune アプリ保護ポリシーをサポートしていないアプリに転送されるデータを許可する必要がある場合は、独自の例外を作成できます。 詳細については、「[データ転送の除外対象](#data-transfer-exemptions)」を参照してください。 | すべてのアプリ |
| **[アプリで他のアプリからのデータの受信を許可する]** | このアプリにデータを転送できるアプリを以下のように指定します。 <ul><li>**ポリシーで管理されているアプリ**: 他のポリシーで管理されているアプリからの転送のみを許可します。</li><li>**すべてのアプリ**: すべてのアプリからのデータ転送を許可します。</li><li>**なし**: 他のポリシーで管理されているアプリを含め、アプリからのデータ転送を許可しません。</li></ul> 一部の除外対象アプリとサービスは、Intune でデータ転送元として許可される可能性があります。 アプリとサービスの完全な一覧については、「[データ転送の除外対象](#data-transfer-exemptions)」をご覧ください。 登録されていない iOS デバイス上にある、複数 ID の MAM 対応のアプリケーションでは、このポリシーは無視され、すべての受信データが許可されます。 | すべてのアプリ |
| **[名前を付けて保存] を禁止する** | このアプリで [名前を付けて保存] オプションの使用を無効にするには、**[はい]** を選択します。 [名前を付けて保存] の使用を許可する場合は、**[いいえ]** を選択します。 | [いいえ] |
| **[切り取り、コピー、および他のアプリでの貼り付けを制限する]** | このアプリで切り取り、コピー、および貼り付け操作をいつ使用できるようにするかを指定します。 次の中から選択します。 <ul><li>**ブロック**: このアプリと他のアプリの間で、切り取り、コピー、および貼り付け操作を許可しません。</li><li>**ポリシーで管理されているアプリ**: このアプリと他のポリシーで管理されているアプリ間で、切り取り、コピー、および貼り付け操作を許可します。</li><li>**貼り付けを使用する、ポリシーで管理されているアプリ**: このアプリと他のポリシーで管理されているアプリ間で切り取りまたはコピーを許可します。 任意のアプリからこのアプリへのデータの貼り付けを許可します。</li><li>**すべてのアプリ**: このアプリに対する切り取り、コピー、貼り付けに制限はありません。 | すべてのアプリ |
|**Web コンテンツを管理対象ブラウザーで表示するように制限する** | **[はい]** を選択すると、アプリ内の Web リンクが Managed Browser アプリで強制的に開かれます。 <br><br> Intune に登録していないデバイスの場合は、ポリシーで管理されているアプリ内の Web リンクを Managed Browser アプリでのみ開くことができます。 <br><br> デバイスの管理に Intune を使用している場合は、「[Microsoft Intune と Managed Browser のポリシーを使用したインターネット アクセスの管理](app-configuration-managed-browser.md)」を参照してください。 | [いいえ] |
| **[アプリ データの暗号化]** | ポリシーで管理されているアプリでは、保存時のデータは iOS によって提供されるデバイス レベルの暗号化方式を使って暗号化されます。 PIN が要求されると、データはアプリ保護ポリシーの設定に従って暗号化されます。 <br><br> FIPS 140-2 認定済みまたは FIPS 140-2 認定保留中の iOS 暗号化モジュールについては、[こちら](https://support.apple.com/HT202739)で Apple の公式ドキュメントをご覧ください。 <br><br> このアプリの職場または学校のデータをどのようなときに暗号化するかを指定します。 次の中から選択します。 <ul><li>**デバイスのロック時**: デバイスのロック時に、このポリシーに関連付けられているすべてのアプリ データが暗号化されます。</li><li>**デバイスがロックされていて、開いているファイルがあるとき**: デバイスのロック時に、アプリで現在開いているファイル内のデータを除き、このポリシーに関連付けられているすべてのアプリ データが暗号化されます。</li><li>**デバイスの再起動後**: デバイスの再起動時、デバイスが最初にロック解除されるまで、このポリシーに関連付けられているすべてのアプリ データが暗号化されます。</li><li>**デバイスの設定を使用**: デバイス上の既定の設定に基づいて、アプリ データが暗号化されます。 </li></ul> この設定を有効にする場合、状況によっては、ユーザーが自分のデバイスにアクセスするために PIN をセットアップして使用する必要があります。  デバイスの PIN がなく、暗号化が必要な場合、アプリは開かず、"組織により、このアプリケーションにアクセスするには、最初にデバイス PIN を有効にする必要があります" というメッセージが表示され、ユーザーは PIN の設定を求められます。  | デバイスがロックされている場合 |
| **連絡先の同期を無効にする** | **[はい]** を選択すると、アプリでデバイス上のネイティブ連絡先アプリにデータを保存できなくなります。 **[いいえ]** を選択した場合は、アプリでデバイス上のネイティブ連絡先アプリにデータを保存できます。 <br><br>選択的ワイプを実行し、アプリから職場または学校のデータを削除すると、アプリからネイティブ連絡先アプリに直接同期されている連絡先が削除されます。 ネイティブ アドレス帳から別の外部ソースに同期された連絡先はワイプできません。 現在、これは Microsoft Outlook アプリにのみ適用されます。 | [いいえ] |
| **印刷を無効にする** | **[はい]** を選択すると、アプリで職場または学校のデータを印刷できなくなります。 | [いいえ] |
| **会社のデータを保存できるストレージ サービスの選択** | ユーザーは、選択したサービス (OneDrive for Business、SharePoint、ローカル ストレージ) に保存できます。 他のすべてのサービスはブロックされます。 | 0 件選択済み |

> [!NOTE]
> データ再配置の設定では、iOS デバイスの Apple Managed Open In 機能は制御されません。 Apple Managed Open In を使うには、「[Microsoft Intune を使用して iOS アプリ間のデータ転送を管理する](data-transfer-between-apps-manage-ios.md)」をご覧ください。

## <a name="data-transfer-exemptions"></a>データ転送の除外対象

特定のシナリオにおいて Intune アプリ保護ポリシーによってデータ転送が許可される可能性のある除外対象のアプリとプラットフォーム サービスがいくつかあります。 このリストは、セキュリティで保護された生産性向上に役立つと考えられるサービスとアプリを表しており、変更される可能性があります。

| アプリ/サービス名 | 説明 |
| ---- | --- |
|<code>tel; telprompt</code> | ネイティブの電話アプリ |
| <code>skype</code> | Skype |
| <code>app-settings</code> | デバイスの設定 |
| <code>itms; itmss; itms-apps; itms-appss; itms-services</code> | アプリ ストア |
| <code>calshow</code> | ネイティブのカレンダー |


## <a name="access-settings"></a>アクセス設定

| Setting | 使用する方法 | 既定値 |
|------|------|------|
| **[アクセスのために PIN を要求する]** | **[はい]** を選択すると、このアプリを使用する際に PIN が要求されます。 ユーザーは、職場または学校のコンテキストでアプリを初めて実行するときに、この PIN のセットアップを求められます。 PIN は、オンラインまたはオフラインで作業しているときに適用されます。 既定値 = **はい**。<br><br> PIN 強度について、次の設定を構成します。 <ul><li>**種類の選択**: アプリ保護ポリシーが適用されているアプリにアクセスする前に、数値またはパスコードのどちらの種類の PIN を入力する必要があるかを設定します。 数値の場合は数字だけですが、パスコードの場合は少なくとも 1 つのアルファベット**または**少なくとも 1 つの特殊文字で定義できます。 <br><br> **注:** パスコードの種類を構成するには、アプリに Intune SDK バージョン 7.1.12 以降が必要です。 数値型には、Intune SDK バージョンの制限はありません。 許可されている特殊文字には、iOS 英語キーボードの特殊文字と記号が含まれます。 既定値は **[数値]** です。</li><li>**PIN をリセットするまでの試行回数**: ユーザーが PIN をリセットするまでに許可される入力試行回数を指定します。 このポリシー設定の形式は、正の整数をサポートします。 既定値は **5** です。</li><li> **単純な PIN を許可する:** **[はい]** を選ぶと、1234、1111、abcd、aaaa などの単純な PIN シーケンスを使えるようになります。 **[いいえ]** を選択すると、単純なシーケンスは使用できなくなります。 <br><br>**注**: パスコードの種類として PIN が構成され、[単純な PIN を許可する] が [はい] に設定されている場合、少なくとも 1 つの文字**または**少なくとも 1 つの特殊文字を PIN に使用する必要があります。 パスコードの種類として PIN が構成され、[単純な PIN を許可する] が [いいえ] に設定されている場合、少なくとも 1 つの数字**および** 1 つの文字、**さらに**少なくとも 1 つの特殊文字を PIN に使用する必要があります。 既定値 = **はい**。 </li><li>**PIN の長さ**: PIN シーケンスの最小桁数を指定します。<br><br>**注**: 一部の iOS デバイスでは、6 桁を超える PIN の長さが構成されている場合、UI にテキスト入力フィールドが表示されますが、ユーザーは引き続き [種類の選択] 設定で決定された種類の PIN を入力する必要があります。 既定値 = **4**。 </li><li> **PIN の代わりに指紋を許可する (iOS 8 以降):** **[はい]** を選択すると、アプリへのアクセスに、PIN の代わりに [Touch ID](https://support.apple.com/HT201371) を使用できるようになります。 既定値 = **はい**。</li><li> **PIN の代わりに顔認識を許可する (iOS 11+)**: **[はい]** を選択すると、アプリへのアクセスに、PIN の代わりに [Face ID](https://support.apple.com/HT208109) を使用できるようになります。 既定値 = **はい**。 ユーザーは、職場アカウントを使ってアプリにアクセスするときに、顔の識別情報を提供するように求められます。</li><li> **デバイス PIN が管理されている場合にアプリ PIN を無効にする**: 登録されているデバイスでデバイス ロックが検出された場合にアプリの PIN を無効にするには、**[はい]** を選択します。 <br><br> **注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。 既定値 = **いいえ**。</li></ul> iOS デバイスでは、ユーザーが PIN の代わりに [Touch ID](https://support.apple.com/HT201371) または [Face ID](https://support.apple.com/HT208109) を使って身元を証明できるようにすることができます。 Intune は、[LocalAuthentication](https://developer.apple.com/documentation/localauthentication/) API を使って、Touch ID と Face ID によりユーザーを認証します。 Touch ID と Face ID については、「[iOS Security Guide](https://www.apple.com/business/docs/iOS_Security_Guide.pdf)」(iOS セキュリティ ガイド) をご覧ください。 ユーザーが職場または学校のアカウントでこのアプリを使用しようとすると、PIN を入力する代わりに指紋識別と顔識別を求められます。 この設定を有効にすると、会社または学校のアカウントの使用中には、使用中のアプリ一覧のプレビュー画像はぼやけます。 </li></ul><!-- <br><br>You can require a PIN expiration for targeted iOS apps. You can configure the PIN requirement and expiration date in days through the Azure portal. When required, a user will be required to set and use a new PIN before getting access to an iOS app. Only iOS apps that have app protection enabled with the Intune App SDK will support this feature.-->| アクセスのために PIN を要求する: はい <br><br> 種類の選択: 数値 <br><br> PIN のリセットの試行回数: 5 <br><br> 単純な PIN を許可する: はい <br><br> PIN の長さ: 4 <br><br> 指紋を許可する: はい <br><br> 顔認識を許可する: はい <br><br> アプリ PIN を無効にする: いいえ |
| **[アクセスには会社の資格情報が必要]** | **[はい]** を選択すると、ユーザーは、アプリへのアクセスに、PIN を入力する代わりに職場または学校のアカウントでのサインインが求められます。 これを **[はい]** に設定し、PIN または生体認証プロンプトが有効になっている場合は、会社の資格情報と、PIN または生体認証プロンプトの両方が表示されます。 | [いいえ] |
| **脱獄されたデバイスまたは root 化されたデバイスで管理対象アプリが実行されることを禁止する** |  このアプリが脱獄または root 化されたデバイスで実行されないようにする場合は、**[はい]** を選択します。 ユーザーは、引き続き個人のタスクにこのアプリを使用できますが、このアプリの職場または学校のデータにアクセスする場合は別のデバイスを使用する必要があります。 | はい |
| **[(分数) 後に、アクセス要件を再確認する]** | 次の設定を構成します。 <ul><li>**タイムアウト**: これは、(ポリシーで前に定義した) アクセス要件が再確認するまでの分数です。 たとえば、管理者がポリシーで PIN をオンにしてルート化されたデバイスをブロックする、ユーザーが Intune で管理されているアプリを開く、PIN を入力しなければならない、およびルート化されていないデバイスでアプリを使用していなければならないなどです。 この設定を使用する場合、ユーザーはすべての Intune 管理対象アプリでその後の **30 分** (既定値) PIN を入力したり、別のルート検出チェックを行う必要はありません。  <br><br>**注:** iOS では、**同じ公開元**のすべての Intune 管理対象アプリで PIN が共有されます。 デバイスで、アプリがフォアグラウンドを離れると、特定の PIN の PIN タイマーがリセットされます。 設定で定義されているタイムアウトの間、PIN を共有する Intune 管理対象アプリで、PIN を入力する必要はありません。 このポリシー設定の形式は、正の整数をサポートします。<br></li><li>**オフラインの猶予期間**: MAM デバイスをオフラインで実行できる分数です。アプリのアクセス要件を再確認するまでの時間 (分単位) を指定します。 既定値は、**720** 分 (12 時間) です。 これが期限切れになると、アプリを実行し続けることができるよう、ユーザーはアプリにより AAD に対する認証を求められます。 このポリシー設定の形式は、正の整数をサポートします。</li></ul>| タイムアウト: 30 <br><br> オフライン: 720 |
| **アプリ データをワイプするまでのオフライン間隔 (日)** | オフラインでの実行期間がこの日数 (管理者が定義) を超えると、アプリはユーザーに対してネットワークへの接続と再認証を要求します。 ユーザーが正常に認証された場合、引き続きデータにアクセスでき、オフライン間隔がリセットされます。  ユーザーの認証が失敗した場合、アプリはユーザーのアカウントとデータの選択的ワイプを実行します。  選択的ワイプで削除されるデータの詳細については、「[Intune で管理されているアプリから会社のデータをワイプする方法](https://docs.microsoft.com/intune/apps-selective-wipe)」を参照してください。 このポリシー設定の形式は、正の整数をサポートします。 <br> | 90 日間 |
| **iOS オペレーティング システムの最小要件** | このアプリを使用するための最小 iOS オペレーティング システムを要求するには **[はい]** を選択します。 デバイスの iOS バージョンが要件を満たさない場合、アクセスがブロックされます。 <br><br> **注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。 | [いいえ] |
| **iOS オペレーティング システムの最小要件 (警告のみ)** | このアプリを使用するための最小 iOS オペレーティング システムを要求するには **[はい]** を選択します。 デバイスの iOS バージョンが要件を満たさない場合、通知が表示されます。 この通知は閉じることができます。 <br><br> **注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。 | [いいえ] |
| **アプリの最小バージョン要件** | アプリを使用するための最小アプリ バージョンを要求するには **[はい]** を選択します。 デバイスのアプリ バージョンが要件を満たさない場合、アクセスがブロックされます。<br><br>多くの場合、アプリには個別のバージョン管理スキームがあるため、1 つのアプリを対象とした、1 つのアプリの最小バージョンでポリシー ("Outlook バージョン ポリシー" など) を作成します。 <br><br> このポリシー設定では、major.minor、major.minor.build、major.minor.build.revision のいずれの形式もサポートされます。 <br><br> **注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。 | [いいえ] | 
| **アプリの最小バージョン要件 (警告のみ)** | このアプリを使用するための最小アプリ バージョンを推奨するには **[はい]** を選択します。 デバイス上のアプリ バージョンが要件を満たさない場合、通知が表示されます。 この通知は閉じることができます。<br><br>多くの場合、アプリには個別のバージョン管理スキームがあるため、1 つのアプリを対象とした、1 つのアプリの最小バージョンでポリシー ("Outlook バージョン ポリシー" など) を作成します。 <br><br> このポリシー設定では、major.minor、major.minor.build、major.minor.build.revision のいずれの形式もサポートされます。 <br><br> **注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。 | [いいえ] | 
| **Intune アプリ保護ポリシー SDK バージョンの最小要件** | 使用するアプリで Intune アプリ保護ポリシー SDK バージョンの最小要件を要求するには **[はい]** を選択します。 アプリの Intune アプリ保護ポリシー SDK バージョンが要件を満たさない場合、アクセスがブロックされます。 <br> <br> Intune アプリ保護ポリシー SDK に関する詳細については、「[Intune App SDK の概要](app-sdk.md)」をご覧ください。 <br><br> このポリシー設定では、major.minor、major.minor.build、major.minor.build.revision のいずれの形式もサポートされます。 <br><br> **注:** アプリに Intune SDK バージョン 7.0.1 以降が必要です。 | [いいえ] |

> [!NOTE]
> [アクセス] セクションで同じアプリとユーザーの組み合わせに対して構成された複数の Intune アプリ保護設定が iOS 上でどのように動作するかについては、[Intune MAM についてよく寄せられる質問](https://docs.microsoft.com/en-us/intune/mam-faq#app-experience-on-ios)に関するページを参照してください。

##  <a name="add-ins-for-outlook-app"></a>Outlook アプリ用のアドイン

最近、よく使用されているアプリを電子メール クライアントと統合できるアドインが Outlook for iOS に追加されました。 Outlook 用のアドインは、Web、Windows、Mac、および Outlook for iOS で利用できます。 アドインは Microsoft Exchange を介して管理されるため、Exchange でユーザーに対してアドインがオフになっていない限り、ユーザーは Outlook と管理対象外のアドイン アプリケーションの間でデータとメッセージを共有できます。

エンド ユーザーによる Outlook アドインのアクセスとインストールを禁止する場合は (これは Outlook のすべてのクライアントに影響します)、Exchange 管理センターで役割に対して次の変更を行っていることを確認してください。

- ユーザーが Office ストアのアドインをインストールできないようにするには、ユーザーからマイ マーケットプレース役割を削除します。
- ユーザーがアドインをサイド ローディングできないようにするには、ユーザーからマイ カスタム アプリ役割を削除します。
- ユーザーがすべてのアドインをインストールできないようにするには、ユーザーからマイ カスタム アプリ役割とマイ マーケットプレース役割の両方を削除します。

次の手順は、Office 365、Exchange 2016、Exchange 2013 に適用され、Web、Windows、Mac、およびモバイルの Outlook が対象になります。

- Outlook 用アドインの詳細については、[こちら](https://technet.microsoft.com/library/jj943753(v=exchg.150).aspx)を参照してください。
- Outlook アプリ用のアドインをインストールおよび管理できる管理者とユーザーを指定する方法の詳細については、[こちら](https://technet.microsoft.com/library/jj943754(v=exchg.150).aspx)を参照してください。

##  <a name="linkedin-account-connections-for-microsoft-apps"></a>Microsoft アプリの LinkedIn アカウントの接続

LinkedIn アカウントの接続では、ユーザーは特定の Microsoft アプリ内の LinkedIn パブリック プロファイル情報を表示することができます。 既定で、ユーザーは LinkedIn と Microsoft の職場または学校アカウントを接続して、追加の LinkedIn プロファイル情報を表示するよう選択できます。 

> [!NOTE]
> LinkedIn 統合は現在、米国政府機関の顧客、およびオーストラリア、カナダ、中国、フランス、ドイツ、インド、韓国、英国、日本、南アフリカでホストされている Exchange Online メールボックスを使用する組織では利用できません。

組織全体に対して LinkedIn アカウントの接続を無効にすることも、組織内の選択したユーザー グループに対して LinkedIn アカウントの接続を有効にすることもできます。 これらの設定は、すべてのプラットフォーム (Web、モバイル、デスクトップ) 上の Office 365 アプリ間の LinkedIn 接続に影響します。 次の操作を行います。

- Azure portal で、テナントに対する LinkedIn アカウントの接続を有効または無効にします。 
- グループ ポリシーを使用して、組織の Office 2016 アプリに対する LinkedIn アカウントの接続を有効または無効にします。

テナントに対して LinkedIn 統合が有効になっている場合、組織内のユーザーが LinkedIn および Microsoft の職場または学校アカウントを接続したときに、次の 2 つのオプションを使用できます。 

- 両方のアカウント間でデータを共有するためのアクセス許可を付与することができます。 これは、LinkedIn アカウントに Microsoft の職場または学校アカウントとデータを共有するためのアクセス許可を与え、Microsoft の職場または学校アカウントに LinkedIn アカウントとデータを共有するためのアクセス許可を与えることを意味します。 LinkedIn と共有されるデータは、オンライン サービスを離れます。 
- LinkedIn アカウントからのみデータを共有するためのアクセス許可を、Microsoft の職場または学校アカウントに付与することができます

ユーザーがアカウント間でデータを共有することに同意した場合、Office アドインの場合と同様に、LinkedIn 統合では既存の Microsoft Graph API を使用します。 LinkedIn 統合では Office アドインで利用可能な API のサブセットのみを使用し、さまざまな除外をサポートします。


|Microsoft Graph に対するアクセス許可  |説明  |
|---------|---------|
|[人](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#people-permissions)に対する読み取りアクセス許可     |アプリがサインインしたユーザーに関連する人のスコア付きリストを読み取ることを許可します。 このリストには、ローカルの連絡先、ソーシャル ネットワーキングまたは組織のディレクトリからの連絡先、最近 (メールや Skype などで) 連絡した人が含まれる場合があります。         |
|[予定表](https://na01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdeveloper.microsoft.com%2Fen-us%2Fgraph%2Fdocs%2Fconcepts%2Fpermissions_reference%23calendars-permissions&data=04%7C01%7CCem.Aykan%40microsoft.com%7C59705402acc347cdf0d908d5b1d82d53%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636610464378331622%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwifQ%3D%3D%7C-1&sdata=fABkrlIxqggnB%2Bc%2BR%2BbFpuenhSg7OHfBhWcbv3ahmAU%3D&reserved=0)に対する読み取りアクセス許可     |アプリがユーザーの予定表内のイベントを読み取ることを許可します。 サインインしたユーザーの予定表の会議、その時間、場所、および出席者が含まれます。         |
|[ユーザー プロファイル](https://na01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdeveloper.microsoft.com%2Fen-us%2Fgraph%2Fdocs%2Fconcepts%2Fpermissions_reference%23user-permissions&data=04%7C01%7CCem.Aykan%40microsoft.com%7C59705402acc347cdf0d908d5b1d82d53%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636610464378341626%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwifQ%3D%3D%7C-1&sdata=RcnVIpntjyR4TXafOYTV0SffZuZWpshQQWY0e2VkkXg%3D&reserved=0)に対する読み取りアクセス許可     |ユーザーがアプリにサインインすることと、アプリがサインインしたユーザーのプロファイルを読み取ることを許可します。 アプリがサインインしたユーザーの基本的な会社情報を読み取ることも許可します。         |
|Subscriptions     |このスコープは使用不可であり、まだ使用されていません。 Office 365 などの Microsoft アプリとサービスに対する、ユーザーの組織によって提供されるサブスクリプションが含まれます。         |
|インサイト     |このスコープは利用できず、まだ使用されていません。 Microsoft サービスの使用に基づき、サインインしたユーザーのアカウントに関連付けられている関心が含まれます。         |

### <a name="learn-more"></a>詳細情報

- [Microsoft アプリの LinkedIn の情報と機能](https://go.microsoft.com/fwlink/?linkid=850740)について学習します。
- [Office 365 ロードマップ ページ](https://products.office.com/en-US/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc)に示されている LinkedIn アカウント接続のリリースについて学習します。 
- [LinkedIn アカウント接続の構成](https://docs.microsoft.com/en-us/azure/active-directory/linkedin-integration)について学習します。
- ユーザーの LinkedIn および Microsoft の職場または学校アカウント間で共有されるデータの詳細については、[職場または学校の Microsoft アプリケーションの LinkedIn](https://www.linkedin.com/help/linkedin/answer/84077) に関するページを参照してください。

