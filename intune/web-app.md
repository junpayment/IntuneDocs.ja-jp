---
title: Web アプリを Microsoft Intune に追加する
titleSuffix: ''
description: Web アプリを Microsoft Intune に追加する方法について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/15/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 5f08752f-0e87-4ad9-a34c-4991b3150775
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 0d62341e35bf851bb429b15a582183bec62a9d4a
ms.sourcegitcommit: 34e96e57af6b861ecdfea085acf3c44cff1f3d43
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
# <a name="add-web-apps-to-microsoft-intune"></a>Web アプリを Microsoft Intune に追加する

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

Intune では、Web アプリなど、さまざまなアプリの種類がサポートされています。 Web アプリはクライアント/サーバー アプリケーションです。 サーバーから Web アプリが提供されます。これには UI、コンテンツ、および機能が含まれます。 さらに、最新の Web ホスティング プラットフォームでは一般的にセキュリティや負荷分散などの利点が提供されます。 Web アプリは Web 上で個別に維持されます。 Microsoft Intune を使って、このアプリの種類を参照します。 また、このアプリへのアクセスを許可するユーザー グループを割り当てます。 

ユーザー用アプリを管理して割り当てるには、そのアプリを Intune に追加します。 Intune によって、ユーザーのデバイスのホーム画面に Web アプリへのショートカットが作成されます。

> [!Note]
> Web アプリは、Android for Work デバイスと macOS ではサポートされていません。

## <a name="add-a-web-app-to-intune"></a>Web アプリを Intune に追加する
Web 上のアプリへのショートカットとしてアプリを Intune に追加するには、次の操作を行います。

1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[すべてのサービス]** > **[Intune]** の順に選択します。  
    Intune は **[監視 + 管理]** セクションにあります。
3. **[Intune]** ウィンドウで、**[モバイル アプリ]** を選択します。
4. **[モバイル アプリ]** ワークロード ウィンドウで、**[管理]** の **[アプリ]** を選択します。
5. **[アプリ]** ウィンドウで **[追加]** を選択します。
6. **[アプリの追加]** ウィンドウの **[アプリの種類]** ドロップダウン リストで、**[Web リンク]** という種類を選択します。
7. **[構成]** を選択します。
8. **[アプリ情報]** ウィンドウで、以下の情報を追加します。
    - **[名前]**: アプリの名前を入力します。この名前は会社のポータルに表示されます。
    - **[説明]**: アプリの説明を入力します。 この説明は会社のポータルでユーザーに表示されます。
    - **[発行元]**: このアプリの発行元の名前を入力します。
    - **[アプリ URL]**: 割り当てるアプリをホストする Web サイトの URL を入力します。
    - **[カテゴリ]**: 必要に応じて、1 つ以上の組み込みアプリ カテゴリ、または作成したカテゴリを選択します。 そうすると、会社のポータルを閲覧するときに、ユーザーがアプリを探しやすくなります。
    - **[会社のポータルでおすすめアプリとして表示します]**: この設定では、ユーザーがアプリを探すときに、会社のポータルのメイン ページでアプリ スイートが目立つように表示されます。
    - **[このリンクを開くには Managed Browser が必要です]**: Web サイトまたは Web アプリへのリンクをユーザーに割り当てて、ユーザーが Intune Managed Browser で開けるようにするには、このオプションを選択します。 このブラウザーをデバイスにインストールする必要があります。
    - **[ロゴ]**: アプリに関連付けるアイコンをアップロードします。 ユーザーが会社のポータルを参照するとき、アプリにこのアイコンが表示されます。
9. **[OK]** を選択します。
10. **[アプリの追加]** ウィンドウで **[追加]** を選択します。

> [!Note]
> ユーザーは、Android デバイスに割り当てられた Web アプリを表示するには、ホーム画面に Intune ウィジェットを追加する必要があります。

## <a name="next-steps"></a>次の手順

作成したアプリはアプリの一覧に表示され、選択したグループに割り当てることができるようになります。 詳細については、[アプリをグループに割り当てる方法](apps-deploy.md)に関するページを参照してください。 
