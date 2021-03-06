---
title: Microsoft Intune で SCEP 証明書を使用する - Azure | Microsoft Docs
description: SCEP 証明書を Microsoft Intune で使うには、オンプレミスの AD ドメインを構成し、証明機関を作成し、NDES サーバーをセットアップして、Intune Certificate Connector をインストールします。 その後、SCEP 証明書プロファイルを作成して、グループにこのプロファイルを割り当てます。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/23/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.reviewer: kmyrup
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: f67ccf1c2fb3b708916ef4ed4209bd3be07d9a5e
ms.sourcegitcommit: 6a9830de768dd97a0e95b366fd5d2f93980cee05
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
---
# <a name="configure-and-use-scep-certificates-with-intune"></a>Intune で SCEP 証明書を構成して使用する

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

この記事では、インフラストラクチャを構成してから、Intune で SCEP (Simple Certificate Enrollment Protocol) 証明書プロファイルを作成して割り当てる方法について説明します。

## <a name="configure-on-premises-infrastructure"></a>オンプレミス インフラストラクチャを構成する

- **Active Directory ドメイン**: このセクションで示されているすべてのサーバー (Web アプリケーション プロキシ サーバーを除く) は、Active Directory ドメインに参加する必要があります。

- **証明機関** (CA): Windows Server 2008 R2 以降の Enterprise エディションで実行するエンタープライズ証明機関 (CA) が必要です。 スタンドアロン CA はサポートされません。 詳細については、「[Install the Certification Authority (証明機関のインストール)](http://technet.microsoft.com/library/jj125375.aspx)」をご覧ください。
    CA が Windows Server 2008 R2 を搭載している場合は、 [KB2483564 の修正プログラムをインストール](http://support.microsoft.com/kb/2483564/)する必要があります。

- **NDES サーバー**: Windows Server 2012 R2 以降を実行しているサーバーに、ネットワーク デバイス登録サービス (NDES) を設定する必要があります。 エンタープライズ CA も実行しているサーバーで Intune を実行する場合には、ネットワーク デバイス登録サービスは使用できません。 ネットワーク デバイス登録サービスをホストするための Windows Server 2012 R2 の構成方法については、「[ネットワーク デバイス登録サービスのガイダンス](http://technet.microsoft.com/library/hh831498.aspx)」を参照してください。
NDES サーバーは、CA をホストしているドメインに参加する必要があります。CA と同じサーバーに置くことはできません。 別個のフォレスト、分離ネットワーク、内部ドメインで NDES サーバーを展開する方法については、「[ポリシー モジュールとネットワーク デバイス登録サービスの使用](https://technet.microsoft.com/library/dn473016.aspx)」を参照してください。

- **Microsoft Intune Certificate Connector**: Azure Portal を使用して **Certificate Connector** インストーラー (**ndesconnectorssetup.exe**) をダウンロードします。 その後は、Certificate Connector をインストールするネットワーク デバイス登録サービス (NDES) の役割をホストするサーバーで **ndesconnectorssetup.exe** を実行できます。 
- **Web アプリケーション プロキシ サーバー** (省略可能): Web アプリケーション プロキシ (WAP) サーバーとして Windows Server 2012 R2 以降を実行しているサーバーを使用します。 この構成は:
  -  デバイスはインターネット接続を使用して証明書を受信できます。
  -  デバイスがインターネット接続経由で証明書を受信して更新する場合のセキュリティ推奨事項です。

#### <a name="additional"></a>Additional
- WAP をホストするサーバーは、ネットワーク デバイス登録サービスで使用される長い URL のサポートを有効にする [更新プログラムをインストールする](http://blogs.technet.com/b/ems/archive/2014/12/11/hotfix-large-uri-request-in-web-application-proxy-on-windows-server-2012-r2.aspx) 必要があります。 この更新プログラムは、 [2014 年 12 月の更新プログラムのロールアップ](http://support.microsoft.com/kb/3013769)に含まれます。または、 [KB3011135](http://support.microsoft.com/kb/3011135)から個別に入手できます。
- WAP サーバーは、外部クライアントに公開される名前と一致する SSL 証明書を持ち、NDES サーバーで使用される SSL 証明書を信頼する必要があります。 これらの証明書を使用すると、WAP サーバーはクライアントからの SSL 接続を終了し、NDES サーバーへの新しい SSL 接続を作成できます。

詳しくは、[Plan certificates for WAP](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11)#plan-certificates) (WAP の証明書の計画) に関するページおよび [general information about WAP servers](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn584113(v=ws.11)) (WAP サーバーについての一般情報) に関するページをご覧ください。

### <a name="network-requirements"></a>ネットワークの要件

インターネットから境界ネットワークまでを範囲として、インターネット上のあらゆるホスト/IP アドレスから NDES サーバーへの送信にポート 443 を割り当てます。

境界ネットワークから信頼されたネットワークまでを範囲として、ドメイン参加 NDES サーバーのドメイン アクセスに必要なすべてのポートとプロトコルを割り当てます。 NDES サーバーは、証明書サーバー、DNS サーバー、構成マネージャー サーバー、ドメイン コントローラーへのアクセス許可を必要とします。

NDES サーバーは、[Azure AD アプリケーション プロキシ](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-publish/)、[Web アクセス プロキシ](https://technet.microsoft.com/library/dn584107.aspx)、サード パーティ製のプロキシなどのプロキシを通じて公開することをお勧めします。

### <a name="certificates-and-templates"></a>証明書とテンプレート

|オブジェクト|説明|
|----------|-----------|
|**証明書テンプレート**|発行元 CA でこのテンプレートを構成します。|
|**クライアント認証証明書**|発行元 CA またはパブリック CA から要求されます。この証明書を NDES サーバーにインストールします。|
|**サーバー認証証明書**|発行元 CA またはパブリック CA から要求されます。この SSL 証明書をインストールし NDES サーバーの IIS にバインドします。|
|**信頼されたルート CA 証明書**|この証明書をルート CA またはルート CA を信頼するデバイスから **.cer** ファイルとしてエクスポートし、信頼された CA 証明書プロファイルを使用してデバイスに割り当てます。<br /><br />オペレーティング システムのプラットフォームごとに 1 つの信頼されたルート CA 証明書を使用し、作成する各信頼されたルート証明書プロファイルに関連付けます。<br /><br />必要に応じて、信頼されたルート CA 証明書を追加して使用できます。 ルート CA 証明書を追加する局面としては、Wi-Fi アクセス ポイント用のサーバー認証証明書に署名する CA の信頼性を担保する必要がある場合などが考えられます。|

### <a name="accounts"></a>[アカウント]

|名前|説明|
|--------|-----------|
|**NDES サービス アカウント**|NDES サービス アカウントとして使うドメイン ユーザー アカウントを入力します。|

## <a name="configure-your-infrastructure"></a>インフラストラクチャを構成する
証明書プロファイルを構成するには、次のタスクを実行します。 以下のタスクには、Windows Server 2012 R2 と Active Directory 証明書サービス (ADCS) についての知識が必要となります。

**手順 1**: NDES サービス アカウントを作成する

**手順 2**: 証明機関で証明書テンプレートを構成する

**手順 3**: NDES サーバーで前提条件を構成する

**手順 4**: Intune で使用するための NDES を構成する

**手順 5**: Intune Certificate Connector を有効にし、インストールし、構成する

#### <a name="step-1---create-an-ndes-service-account"></a>手順 1 - NDES サービス アカウントを作成する

NDES サービス アカウントとして使用するドメイン ユーザー アカウントを作成します。 NDES をインストールして構成する前に、発行元 CA でテンプレートを構成するときに、このアカウントを入力します。 既定の権限である、**ローカル ログオン**、**サービスとしてログオン**、**バッチ ジョブとしてログオン**などの権限がユーザーに付与されていることを確認します。 ポリシーを強化し、これらの権限を無効にしている組織もあります。

#### <a name="step-2---configure-certificate-templates-on-the-certification-authority"></a>手順 2 - 証明機関で証明書テンプレートを構成する
このタスクでは次のことを行います。

- NDES の証明書テンプレートを構成します
- NDES に証明書テンプレートを発行します

##### <a name="configure-the-certification-authority"></a>証明機関を構成する

1. エンタープライズ管理者としてサインインします。

2. 発行元 CA で、証明書テンプレート スナップインを使って、新しいカスタム テンプレートを作成します。 または、既存のテンプレートをコピーしてから、NDES で使うために既存のテンプレート (ユーザー テンプレートなど) を更新します。

   >[!NOTE]
   > NDES 証明書テンプレートは、v2 証明書テンプレートを基盤とする必要があります (Windows 2003 の互換性あり)。

   テンプレートには次の構成が必要です。

   - テンプレートのわかりやすい**テンプレート表示名**を入力します。

   - **[サブジェクト名]** で **[要求に含まれる]** を選択します。 (セキュリティが NDES の Intune ポリシー モジュールによって適用されます)。

   - **[拡張機能]** で、**[アプリケーション ポリシーの説明]** に **[クライアント認証]** が含まれることを確認します。

     > [!IMPORTANT]
     > iOS および macOS の証明書テンプレートの場合、**[拡張機能]** タブで、**[キー使用法]** を編集し、**[署名は発行元の証明である]** がオンになっていないことを確認します。

   - **[セキュリティ]** で、NDES サービス アカウントを追加し、テンプレートの **[登録]** アクセス許可を付与します。 SCEP プロファイルを作成する Intune 管理者は、SCEP プロファイルの作成時にテンプレートを閲覧できるように、**読み取り**権限を必要とします。

     > [!NOTE]
     > 証明書を失効させるには、証明書プロファイルで使用されている証明書テンプレートごとに*証明書の発行および管理*の権限が NDES サービス アカウントに必要です。

3. **[一般]** タブでテンプレートの **[有効期間]** を確認します。 既定では、Intune はテンプレートで構成されている値を使用します。 ただし、要求元が異なる値を入力できるように CA を構成できます。異なる値は、Intune 管理者コンソールから設定できます。 常にテンプレートの値を使用する場合は、この手順の残りの部分をスキップします。

   > [!IMPORTANT]
   > iOS および macOS は、他の構成に関係なく、常にテンプレートで設定される値を使用します。

テンプレート構成の例:

![テンプレート、[要求処理] タブ](./media/scep_ndes_request_handling.png)

![テンプレート、[サブジェクト名] タブ](./media/scep_ndes_subject_name.jpg)

![テンプレート、[セキュリティ] タブ](./media/scep_ndes_security.jpg)

![テンプレート、[拡張] タブ](./media/scep_ndes_extensions.jpg)

![テンプレート、[発行要件] タブ](./media/scep_ndes_issuance_reqs.jpg)

> [!IMPORTANT]
> アプリケーション ポリシーの場合、必要なアプリケーション ポリシーのみを追加します。 セキュリティ管理者の選択を確定します。

要求元が有効期間を入力できるように CA を構成します。

1. CA で次のコマンドを実行します。
   - **certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**
   - **net stop certsvc**
   - **net start certsvc**

2. 発行元 CA で、証明機関スナップインを使用して証明書テンプレートを発行します。
   **[証明書テンプレート]** ノードを選択し、**[アクション]** > **[新規]** > **[発行する証明書テンプレート]** の順にクリックして、手順 2 で作成したテンプレートを選択します。

3. **[証明書テンプレート]** フォルダーに表示されることで、テンプレートが発行されたことを確認します。

#### <a name="step-3---configure-prerequisites-on-the-ndes-server"></a>手順 3 - NDES サーバーで前提条件を構成する
このタスクでは次のことを行います。

- Windows サーバーに NDES を追加し、NDES をサポートするように IIS を構成する
- NDES サービス アカウントを IIS_IUSR グループに追加します
- NDES サービス アカウントの SPN を設定します

1. NDES をホストするサーバーに**エンタープライズ管理者**としてサインインし、[役割と機能の追加ウィザード](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11))を使って NDES をインストールします。

   1. ウィザードで、**[Active Directory 証明書サービス]** を選択して AD CS 役割サービスにアクセスできるようにします。 **[ネットワーク デバイス登録サービス]** をオンにし、**[証明機関]** をオフにして、ウィザードを完了します。

      > [!TIP]
      > **[インストールの進行状況]** では、**[閉じる]** をオンにしないでください。 代わりに、**[対象サーバーに Active Directory 証明書サービスを構成する]** リンクを選択します。 次のタスクで使う **[AD CS の構成]** ウィザードが開きます。 [AD CS の構成] が開いた後は、役割と機能の追加ウィザードを閉じてかまいません。

   2. NDES がサーバーに追加されるときに、ウィザードは IIS もインストールします。 IIS が次の構成であることを確認します。

   3. **[Web サーバー]** > **[セキュリティ]** > **[要求のフィルタリング]**

   4. **[Web サーバー]** > **[アプリケーション開発]** > **[ASP.NET 3.5]**。 ASP.NET 3.5 をインストールすると、.NET Framework 3.5 がインストールされます。 .NET Framework 3.5 をインストールするとき、**[.NET Framework 3.5]** のコア機能および **[HTTP アクティブ化]** の両方をインストールします。

   5. **[Web サーバー]** > **[アプリケーション開発]** > **[ASP.NET 4.5]**。 ASP.NET 4.5 をインストールすると、.NET Framework 4.5 がインストールされます。 .NET Framework 4.5 をインストールするときに、**[.NET Framework 4.5]** のコア機能、**[ASP.NET 4.5]**、および **[WCF サービス]** > **[HTTP アクティブ化]** 機能をインストールします。

   6. **[管理ツール]** > **[IIS 6 と互換性のある管理]** > **[IIS 6 メタベース互換]**

   7. **[管理ツール]** > **[IIS 6 と互換性のある管理]** > **[IIS 6 WMI 互換性]**

   8. サーバーで、**IIS_IUSR** グループのメンバーとして NDES サービス アカウントを追加します。

2. 管理者特権のコマンド プロンプトで、次のコマンドを実行して、NDES サービス アカウントの SPN を設定します。

    `setspn -s http/<DNS name of NDES Server> <Domain name>\<NDES Service account name>`

    たとえば、NDES サーバーの名前が **Server01**、ドメインが **Contoso.com**、サービス アカウントが **NDESService**の場合は、次のようになります。

    `setspn –s http/Server01.contoso.com contoso\NDESService`

#### <a name="step-4---configure-ndes-for-use-with-intune"></a>手順 4 - Intune で使用するための NDES を構成する
このタスクでは次のことを行います。

- 発行元 CA で使用するための NDES を構成する
- IIS でサーバー認証 (SSL) 証明書をバインドします
- IIS で要求フィルター処理を構成します

1. NDES サーバーで AD CS 構成ウィザードを開き、次の更新を行います。

    > [!TIP]
    > 前のタスクでリンクをクリックした場合、このウィザードは既に開いています。 それ以外の場合、サーバー マネージャーを開いて Active Directory 証明書サービスの展開後構成にアクセスします。

   - **[役割サービス]** で、**[ネットワーク デバイス登録サービス]** を選択します
   - **[NDES のサービス アカウント]** で、NDES サービス アカウントを入力します
   - **[NDES 用の CA]** で、**[選択]** をクリックして、証明書テンプレートを構成した発行元 CA を選択します
   - **[NDES の暗号化]** で、会社の要件を満たすキーの長さを設定します。
   - **[確認]** で、**[構成]** を選択してウィザードを完了します。

2. ウィザードが完了した後、NDES サーバーで次のレジストリ キーを更新します。

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP\`

    このキーを更新するには、証明書テンプレートの**目的**を明らかにします (**[要求の処理]** タブでわかります)。 その後、既存のデータを、タスク 1 で指定した証明書テンプレートの (表示名ではなく) 名前に置き換えることで、対応するレジストリ エントリを更新します。 次の表では、証明書テンプレートの目的とレジストリの値の対応を示します。

    |証明書テンプレートの目的 ([要求の処理] タブ)|編集するレジストリ値|SCEP プロファイルについて Intune 管理コンソールに表示される値|
    |---|---|---|
    |署名|SignatureTemplate|デジタル署名|
    |暗号化|EncryptionTemplate|キーの暗号化|
    |署名と暗号化|GeneralPurposeTemplate|キーの暗号化<br/>デジタル署名|

    たとえば、証明書テンプレートの目的が **[暗号化]** の場合、 **EncryptionTemplate** の値を証明書テンプレートの名前に編集します。

3. NDES サーバーは、長い URL (クエリ) を受け取ります。2 つのレジストリ エントリを追加する必要があります。


   |                        場所                        |      値      | 型  |      データ       |
   |--------------------------------------------------------|-----------------|-------|-----------------|
   | HKLM\SYSTEM\CurrentControlSet\Services\HTTP\Parameters | MaxFieldLength  | DWORD | 65534 (10 進数) |
   | HKLM\SYSTEM\CurrentControlSet\Services\HTTP\Parameters | MaxRequestBytes | DWORD | 65534 (10 進数) |


4. IIS マネージャーで、**[既定の Web サイト]** > **[要求のフィルタリング]** > **[機能設定の編集]** の順に選びます。 次のように、**[URL の最大長]** と **[クエリ文字列の最大長]** を *65534* に変更します。

    ![IIS の URL とクエリの最大長](./media/SCEP_IIS_max_URL.png)

5. サーバーを再起動します。 サーバーで実行されている **iisreset** は、これらの変更をファイナライズするために十分ではないでしょう。
6. `http://*FQDN*/certsrv/mscep/mscep.dll` を参照します。 次のような NDES ページが表示されます。

    ![NDES のテスト](./media/SCEP_NDES_URL.png)

    「**503 サービスを利用できません**」が表示された場合、イベント ビューアを確認します。 おそらくは、NDES ユーザーに権限がないため、アプリケーション プールが停止しているでしょう。 それらの権限に関する説明はタスク 1 にあります。

##### <a name="install-and-bind-certificates-on-the-ndes-server"></a>NDES サーバーで証明書をインストールしてバインドする

1. NDES サーバーで、内部 CA またはパブリック CA に **サーバー認証** 証明書を要求してインストールします。 その後、この SSL 証明書を IIS でバインドします。

    > [!TIP]
    > IIS で SSL 証明書をバインドした後、クライアント認証証明書をインストールします。 この証明書は、NDES サーバーによって信頼されている CA によって発行できます。 最善の方法ではありませんが、証明書にサーバーとクライアント両方の EKU (Enhance Key Usage) がある場合は、同じ証明書をサーバー認証とクライアント認証の両方に使用できます。 これらの認証証明書については、次の手順を確認してください。

   1. サーバー認証証明書を取得した後、**IIS マネージャー**を開き、**[既定の Web サイト]** を選択します。 **[操作]** ウィンドウで、**[バインド]** を選択します。

   2. **[追加]** をクリックし、**[種類]** を **[https]** に設定して、ポートが **443** であることを確認します。 スタンドアロンの Intune ではポート 443 のみがサポートされます。

   3. **[SSL 証明書]** で、サーバー認証証明書を入力します。

      > [!NOTE]
      > NDES サーバーが 1 つのネットワーク アドレスに対して外部名と内部名を使っている場合は、サーバー認証証明書が必要です。
      > - 外部パブリック サーバー名を含む **[サブジェクト名]**
      > - 内部サーバー名を含む **[サブジェクトの別名]**

2. NDES サーバーで、内部 CA またはパブリック CA に **クライアント認証** 証明書を要求してインストールします。 証明書に両方の機能がある場合、これはサーバー認証証明書と同じ証明書でもかまいません。

    クライアント認証証明書には次のプロパティが必要です。

    - **[拡張キー使用法]**: この値は、**[クライアント認証]** を含む必要があります

    - **[サブジェクト名]**: この値は、証明書をインストールするサーバー (NDES サーバー) の DNS 名と同じである必要があります

##### <a name="configure-iis-request-filtering"></a>IIS 要求フィルタリングを構成する

1. NDES サーバーで **IIS マネージャー**を開き、**[接続]** ウィンドウの **[既定の Web サイト]** を選択し、**[要求のフィルタリング]** を開きます。

2. **[機能設定の編集]** を選択し、次のように値を設定します。

    - **[クエリ文字列の最大長 (バイト)]** = **65534**
    - **URL の最大長 (バイト)** = **65534**

3. 次のレジストリ キーを確認します。

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters`

    次の値が DWORD エントリとして設定されていることを確認します。

    - 名前: **MaxFieldLength**、10 進数値 **65534**
    - 名前: **MaxRequestBytes**、10 進数値 **65534**

4. NDES サーバーを再起動します。 サーバーは証明書コネクタをサポートする準備ができました。

#### <a name="step-5---enable-install-and-configure-the-intune-certificate-connector"></a>手順 5 - Intune Certificate Connector を有効にし、インストールし、構成する
このタスクでは次のことを行います。

- Intune で NDES のサポートを有効にします。
- 環境内のネットワーク デバイス登録サービス (NDES) の役割をホストするサーバーで Certificate Connector をダウンロード、インストール、構成します。 組織内の NDES の実装のスケールを大きくするには、各 NDES サーバー上の Microsoft Intune Certificate Connector で複数の NDES サーバーをインストールできます。

##### <a name="download-install-and-configure-the-certificate-connector"></a>証明書コネクタをダウンロードし、インストールして、構成する
![ConnectorDownload](./media/certificates-download-connector.png)

1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[すべてのサービス]** を選択し、**[Intune]** をフィルターとして適用し、**[Microsoft Intune]** を選択します。
3. **[デバイス構成]** を選択し、**[証明機関]** を選択します。
4. **[追加]** を選択し、**[Download the Connector file]\(コネクタ ファイルをダウンロードします\)** を選択します。 インストールするサーバーからアクセスできる場所にダウンロードしたものを保存します。
5. ダウンロードが完了した後、ダウンロードしたインストーラー (**ndesconnectorssetup.exe**) を、ネットワーク デバイス登録サービス (NDES) の役割をホストしているサーバーで実行します。 インストーラーは、NDES のポリシー モジュールと CRP Web サービスもインストールします。 (CRP Web サービス CertificateRegistrationSvc は IIS のアプリケーションとして実行されます)。

    > [!NOTE]
    > スタンドアロン Intune の NDES をインストールする場合、CRP サービスは証明書コネクタと共に自動的にインストールされます。 構成マネージャーで Intune を使用する場合は、証明書登録ポイントを別のサイト システムの役割としてインストールします。

6. 証明書コネクタのクライアント証明書の入力を求められたら、**[選択]** を選択し、タスク 3 で NDES サーバーにインストールした**クライアント認証**証明書を選択します。

    クライアント認証証明書を選択した後、**[Microsoft Intune 証明書コネクタのクライアント証明書]** 画面に戻ります。 選択した証明書は表示されませんが、**[次へ]** を選択してその証明書のプロパティを表示します。 **[次へ]** を選択して、**[インストール]** を選択します。
    
    > [!IMPORTANT]
    > Intune 証明書コネクタは、Internet Explorer セキュリティ強化の構成が有効になっているデバイスでは登録できません。 Intune 証明書コネクタを使うには、[IE セキュリティ強化の構成を無効にします](https://technet.microsoft.com/library/cc775800(v=WS.10).aspx)。

7. ウィザードが完了した後、ウィザードを閉じる前に、**証明書コネクタの UI を起動**します。

    > [!TIP]
    > 証明書コネクタの UI を起動する前にウィザードを閉じた場合は、次のコマンドを実行して再び開くことができます。
    >
    > <インストール パス>\NDESConnectorUI\NDESConnectorUI.exe

8. **証明書コネクタ** UI で:

    **[サインイン]** を選択し、Intune サービス管理者の資格情報、またはグローバル管理アクセス許可を持つテナント管理者の資格情報を入力します。

    > [!IMPORTANT]
    > ユーザー アカウントに有効な Intune ライセンスが割り当てられている必要があります。 ユーザー アカウントに有効な Intune ライセンスがない場合、NDESConnectorUI.exe は失敗します。

    組織でプロキシ サーバーを使用していて、NDES サーバーがインターネットにアクセスするためにプロキシが必要な場合は、**[プロキシ サーバーを使用する]** を選択し、接続するためのプロキシ サーバーの名前、ポート、およびアカウント資格情報を入力します。

    **[詳細設定]** タブを選択し、発行元 CA で**証明書の発行と管理**アクセス許可を持つアカウントの資格情報を入力します。 変更を**適用**します。

    これで、証明書コネクタ UI を閉じることができます。

9. コマンド プロンプトを開き、「**services.msc**」と入力して、**Enter** キーを押します。 **[Intune コネクタ サービス]** を右クリックして、**再起動**します。

サービスが実行していることを確認するには、ブラウザーを開き、次の URL を入力します。 **403** エラーが返る必要があります。

`http://<FQDN_of_your_NDES_server>/certsrv/mscep/mscep.dll`

## <a name="create-a-scep-certificate-profile"></a>SCEP 証明書プロファイルを作成する

1. Azure Portal で Microsoft Intune を開きます。
2. **[デバイス構成]**、**[プロファイル]**、**[プロファイルの作成]** の順に選択します。
3. SCEP 証明書プロファイルの **[名前]** と **[説明]** を入力します。
4. **[プラットフォーム]** ドロップダウン リストで、この SCEP 証明書のデバイス プラットフォームを選択します。 現時点では、デバイスの制限設定に対応している次のいずれかのプラットフォームを選択できます。
   - **Android**
   - **Android**
   - **macOS**
   - **Windows Phone 8.1**
   - **Windows 8.1 以降**
   - **Windows 10 以降**
5. **[プロファイルの種類]** ドロップダウン リストで、**[SCEP 証明書]** を選択します。
6. **[SCEP 証明書]** ウィンドウで、次の設定を構成します。

   - **[証明書の有効期間]**: 発行元 CA で `certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE` コマンドを実行してカスタム有効期間を設定できるようにした場合は、証明書が失効するまでの期間を入力します。<br>証明書テンプレートの有効期限よりも小さい値を入力できますが、大きい値は指定できません。 たとえば、証明書テンプレートで証明書の有効期限が 2 年の場合は、この値を 1 年にすることはできますが、5 年にすることはできません。 また、発行元の CA の証明書の残りの有効期限よりも小さい値を指定する必要があります。 
   - **[キー格納プロバイダー (KSP)]** (Windows Phone 8.1、Windows 8.1、Windows 10): 証明書のキーを格納する場所を入力します。 次のいずれかの値を選択します。
     - **トラステッド プラットフォーム モジュール (TPM) KSP が存在する場合は TPM KSP に登録する (それ以外はソフトウェア KSP に登録する)**
     - **トラステッド プラットフォーム モジュール (TPM) KSP に登録する (それ以外は失敗)**
     - **Passport に登録する、それ以外は失敗 (Windows 10 以降)**
     - **ソフトウェア KSP に登録する**

   - **[サブジェクト名の形式]**: 一覧から、Intune が証明書要求のサブジェクト名をどのように自動生成するかを指定します。 証明書がユーザー用の場合、サブジェクト名にユーザーのメール アドレスを追加することもできます。 次の中から選択します。
     - **未構成**
     - **共通名**
     - **電子メールを含む共通名**
     - **電子メールとしての共通名**
     - **IMEI (International Mobile Equipment Identity)**
     - **シリアル番号**
     - **[カスタム]**: このオプションを選択すると、別のドロップダウン フィールドが表示されます。 このフィールドを使って、カスタムのサブジェクト名の形式を入力します。 カスタム形式は、**共通名 (CN)** と**電子メール (E)** という 2 つの変数をサポートします。 **共通名 (CN)** は、次のいずれかの変数に設定できます。
       - **CN={{UserName}}**: ユーザーのユーザー プリンシパル名 (例: janedoe@contoso.com)
       - **CN={{AAD_Device_ID}}**: Azure Active Directory (AD) でデバイスを登録するときに割り当てられた ID。 通常、この ID は Azure AD での認証に使われます。
       - **CN={{SERIALNUMBER}}**: 一意のシリアル番号 (SN)。通常はデバイスを識別するために製造元によって使われます
       - **CN={{IMEINumber}}**: 携帯電話の識別に使用される IMEI (International Mobile Equipment Identity) の一意の番号
       - **CN={{OnPrem_Distinguished_Name}}**: コンマで区切られた相対識別名のシーケンス、`CN=Jane Doe,OU=UserAccounts,DC=corp,DC=contoso,DC=com` など

          `{{OnPrem_Distinguished_Name}}` 変数を使用するには、[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) を使用して、`onpremisesdistingishedname` ユーザー属性を Azure AD と同期させます。

       - **CN={{onPremisesSamAccountName}}**: 管理者は、Azure AD Connect を使って、Active Directory の samAccountName 属性を、Azure AD の `onPremisesSamAccountName` という属性に同期できます。 Intune は、SCEP 証明書のサブジェクト内の証明書発行要求の一部として、その変数を置き換えることができます。  samAccountName 属性は、以前のバージョンの Windows (windows 2000 より前) のクライアントとサーバーをサポートするために使われるユーザー ログオン名です。 ユーザー ログオン名の形式は、`DomainName\testUser` または単に `testUser` です。

          `{{onPremisesSamAccountName}}` 変数を使用するには、[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) を使用して、`onPremisesSamAccountName` ユーザー属性を Azure AD と同期させます。

       これらの変数の 1 つ以上と静的な文字列の組み合わせを使うことで、カスタム サブジェクト名の形式を作成できます (例: **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**)。 <br/> この例では、CN 変数と E 変数に加えて、組織単位、組織、場所、州、および国の値の文字列を使ってサブジェクト名形式を作成しています。 [CertStrToName 関数](https://msdn.microsoft.com/library/windows/desktop/aa377160.aspx)の記事では、この関数とそのサポートされる文字列について説明されています。

- **[サブジェクトの別名]**: Intune が証明書要求のサブジェクトの別名 (SAN) をどのように自動生成するかを入力します。 たとえば、ユーザー証明書の種類を選択した場合は、サブジェクトの別名にユーザー プリンシパル名 (UPN) を含めることができます。 クライアント証明書を Windows ポリシー サーバーでの認証に使用する場合は、サブジェクトの別名を UPN に設定する必要があります。
- **[キー使用法]**: 証明書のキー使用法のオプションを入力します。 次のようなオプションがあります。
  - **[キーの暗号化]**: キーが暗号化されている場合だけキーを交換できます
  - **[デジタル署名]**: キーがデジタル署名で保護されている場合だけ、キーを交換できます
- **[キー サイズ (ビット)]**: キーに含まれるビット数を選択します
- **[ハッシュ アルゴリズム]** (Android、Windows Phone 8.1、Windows 8.1、Windows 10): この証明書で使用するハッシュ アルゴリズムの種類を 1 つ選択します。 接続しているデバイスをサポートするセキュリティの最も強力なレベルを選択します。
- **[ルート証明書]**: 既に構成してユーザーまたはデバイスに割り当てているルート CA 証明書プロファイルを選択します。 この CA 証明書は、この証明書プロファイルで構成している証明書を発行する CA のルート証明書である必要があります。
- **[拡張キー使用法]**: 証明書の使用目的に対応する値を**追加**します。 ほとんどの場合、ユーザーまたはデバイスがサーバーに対して認証できるように、証明書には **[クライアント認証]** が必要です。 ただし、必要に応じてその他のキー使用法を追加できます。
- **登録設定**
  - **[更新しきい値 (%)]**: 証明書の有効期間の残りがどの程度 (%) になったら、デバイスが更新を要求するかを入力します。
  - **[SCEP サーバーの URL]**: SCEP 経由で証明書を発行する NDES サーバーの URL を 1 つまたは複数入力します。
  - **[OK]**、**[作成]** の順に選んでプロファイルを作成します。

プロファイルが作成され、プロファイルの一覧ウィンドウに表示されます。

## <a name="assign-the-certificate-profile"></a>証明書プロファイルを割り当てる

証明書プロファイルをグループに割り当てる前に、次の点を考慮します。

- 証明書プロファイルをグループに割り当てるときに、信頼された CA 証明書プロファイルの証明書ファイルは、デバイスにインストールされます。 デバイスは、SCEP 証明書プロファイルを使用してデバイスによる証明書要求を作成します。
- 証明書プロファイルは、プロファイルを作成するときに使用するプラットフォームを実行しているデバイスのみにインストールされます。
- ユーザー コレクションまたはデバイス コレクションに証明書プロファイルを割り当てることができます。
- デバイス登録後すぐに証明書をデバイスに公開するには、証明書プロファイルをデバイス グループではなくユーザー グループに割り当てます。 デバイス グループに割り当てた場合は、デバイスがポリシーを受け取る前に、デバイスの登録を完全に行う必要があります。
- 各プロファイルは個別に割り当てますが、信頼されたルート CA と、SCEP または PKCS プロファイルを割り当てる必要もあります。 そうしないと、SCEP または PKCS 証明書ポリシーは失敗します。

    > [!NOTE]
    > iOS では、同じ証明書プロファイルを使う複数のリソース プロファイルを展開した場合は、管理プロファイルに証明書の複数のコピーが表示されます。
    
プロファイルを割り当てる方法については、[デバイス プロファイルを割り当てる方法](device-profile-assign.md)に関する記事をご覧ください。
