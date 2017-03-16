---
title: "Intune アプリ構成ポリシーを使用する方法"
titleSuffix: Intune Azure preview
description: "Intune Azure プレビュー: アプリ構成ポリシーを使用して、実行時に構成データを iOS アプリに提供する方法について説明します。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 02/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: c9163693-d748-46e0-842a-d9ba113ae5a8
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
translationtype: Human Translation
ms.sourcegitcommit: 153cce3809e24303b8f88a833e2fc7bdd9428a4a
ms.openlocfilehash: 73360154765d53fe1f42e4e97699ad9385bfda6f
ms.lasthandoff: 02/18/2017

---

# <a name="how-to-use-microsoft-intune-app-configuration-policies"></a>Microsoft Intune アプリ構成ポリシーを使用する方法

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

Microsoft Intune のアプリ構成ポリシーを使用して、ユーザーがアプリを実行するときに必要となる可能性がある設定を指定できます。 たとえば、アプリは次の内容を指定することをユーザーに要求することがあります。

-   カスタム ポート番号。

-   言語設定。

-   セキュリティ設定。

-   会社のロゴなどのブランドの設定。

ユーザーがこれらの設定を誤って入力すると、ヘルプ デスクの負荷が増加し、新しいアプリの採用が遅くなる可能性もあります。

アプリ構成ポリシーを使用すると、ユーザーがアプリを実行する前にこれらの設定をポリシー内のユーザーに割り当てることができるため、上記の問題を排除するのに役立ちます。 設定が自動的に指定されるため、ユーザーの操作は不要です。

これらのポリシーをユーザーとデバイスに直接割り当てないでください。 代わりに、ポリシーをアプリに関連付け、そのアプリを展開します。 ポリシー設定は、アプリがポリシーを確認する際に (通常は初めて実行したときに) 必ず使用されます。

> [!TIP]
> この種類のポリシーは現在、iOS 8.0 以降を実行しているデバイスでのみ有効です。 次の種類のアプリ インストールをサポートします。
>
> -   **App Store の管理対象 iOS アプリ**
> -   **iOS 用アプリ パッケージ**
>
> アプリのインストールの種類の詳細については、「[How to add an app to Microsoft Intune (Microsoft Intune にアプリを追加する方法)](/intune-azure/manage-apps/add-apps)」を参照してください。

## <a name="create-an-app-configuration-policy"></a>アプリ構成ポリシーを作成する

1. Azure ポータルにサインインします。
2. **[その他のサービス]** > **[その他]** > **[Intune]** の順に選択します。
3. **[Intune]** ブレードで、**[アプリの管理]** を選択します。
1.  **[アプリの管理]** ワークロードで、**[管理]** > **[アプリの構成ポリシー]** の順に選択します。

2.  ポリシーの一覧ブレードで、**[追加]** を選択します。

3.  **[構成ポリシーの追加]** ブレードで、アプリ構成ポリシーの名前と説明 (省略可能) を入力します。
4.  **[関連アプリ]** を選択し、**[関連アプリ]** ブレードで、構成を適用する管理対象アプリを選択します。
5.  **[構成ポリシーの追加]** ブレードで **[構成設定]** を選択し、[構成設定] ブレードから、構成プロファイルを構成する XML 値を指定する方法を選択します。
    - **[XML データを入力する]** - 必要なアプリ構成設定を含む XML プロパティの一覧を入力するか貼り付けます。 XML プロパティ リストの形式は、構成するアプリによって異なります。 使用する形式の詳細については、アプリの供給元にお問い合わせください。
    Intune によって、入力した XML が有効な形式であるかどうかがチェックされます。 XML プロパティ リストが関連付けられているアプリで動作するかどうかはチェックされません。
    XML プロパティ リストの詳細については、iOS 開発者ライブラリの [XML プロパティ リスト](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)に関するページを参照してください。
    - **[構成デザイナーを使用する]** - XML キーと値のペアをポータルで直接指定できます。
8. 完了したら、**[構成ポリシーの追加]** ブレードに戻り、**[作成]** をクリックします。

ポリシーが作成され、ポリシーの一覧ブレードが表示されます。

その後、通常どおり、アプリの[割り当て](deploy-apps.md)と[監視](monitor-apps.md)に進みます。

割り当てたアプリをデバイスで実行すると、アプリ構成ポリシーで構成した設定を使用して実行されます。

> [!TIP]
> 1 つ以上のアプリ構成ポリシーが競合する場合は、どちらのポリシーも適用されません。

## <a name="information-about-the-xml-file-format"></a>XML ファイル形式に関する情報

Intune は、プロパティ リストで次のデータ型をサポートします。

- &lt;integer&gt;
- &lt;real&gt;
- &lt;string&gt;
- &lt;array&gt;
- &lt;dict&gt;
- &lt;true /&gt; または &lt;false /&gt;

データ型の詳細については、iOS 開発者ライブラリの [プロパティ リスト](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) に関するページを参照してください。

また、Intune は次のトークンの種類をプロパティ リストでサポートしています。
- \{\{userprincipalname\}\} - (例: **John@contoso.com**)
- \{\{mail\}\} - (例: **John@contoso.com**)
- \{\{partialupn\}\} - (例: **John**)
- \{\{accountid\}\} - (例: **fc0dc142-71d8-4b12-bbea-bae2a8514c81**)
- \{\{deviceid\}\} - (例: **b9841cd9-9843-405f-be28-b2265c59ef97**)
- \{\{userid\}\} - (例: **3ec2c00f-b125-4519-acf0-302ac3761822**)
- \{\{username\}\} - (例: **John Doe**)
- \{\{serialnumber\}\} - (例: **F4KN99ZUG5V2**) iOS デバイスの場合
- \{\{serialnumberlast4digits\}\} - (例: **G5V2**) iOS デバイスの場合

\{\{ 文字と \}\} 文字を使用できるのはトークンの種類のみであり、他の目的には使用しないでください。





## <a name="example-format-for-an-app-configuration-xml-file"></a>アプリ構成 XML ファイルの形式の例

アプリ構成ファイルを作成する場合、この形式を使用して次の値を&1; つ以上指定できます。

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>

```
