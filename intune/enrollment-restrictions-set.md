---
title: Microsoft Intune で登録制限を設定する
titlesuffix: ''
description: Intune でプラットフォームごとに登録を制限し、デバイス登録の上限数を設定します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/02/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 9691982c-1a03-4ac1-b7c5-73087be8c5f2
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 9b17cb50ead094962196bb030c3a18e4119c6904
ms.sourcegitcommit: 5eba4bad151be32346aedc7cbb0333d71934f8cf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
---
# <a name="set-enrollment-restrictions"></a>登録制限を設定する

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

ユーザーは Intune 管理者として、Intune での管理に登録できるデバイスの数と種類を定義した登録の制限を作成して管理することができます。 制限を複数作成して、さまざまなユーザー グループに適用することができます。 さまざまな制限を作成した場合は、[優先度](#change-enrollment-restriction-priority)を設定することができます。

>[!NOTE]
>登録の制限はセキュリティ機能ではありません。 侵害されたデバイスでは特徴が正しく示されない可能性があります。 これらの制限は、悪意のないユーザーにとって最善の防御策となります。

>[!NOTE]
>この記事で説明している、グループに割り当てられた登録制限と優先順位の機能は、Intune の顧客ベース全体にロールアウトしている過程にあります。 このロールアウトが完了するまで、グループと優先順位の機能にアクセスできないことがあります。

具体的に作成できる登録の制限には、次のようなものがあります。

- 登録されるデバイスの最大数。
- 登録できるデバイスのプラットフォーム:
  - Android。
  - Android for Work。
  - iOS。
  - macOS。
  - 使用できるようになります。
- iOS、Android、Android for Work、および Windows のプラットフォームのオペレーティング システム バージョン  (使用できる Windows のバージョンは 10 のみです。 Windows 8.1 が許可される場合は、空白のままにしておきます)。
  - 最小バージョン。
  - 最大バージョン。
- 個人所有デバイスを制限します (iOS、Android、Android for Work、macOS のみ)。

## <a name="default-restrictions"></a>既定の制限

デバイスの種類とデバイス数の両方の登録制限には、既定の制限が提供されています。 既定の制限のオプションは変更することができます。 既定の制限は、すべてのユーザー登録とユーザーなし登録に適用されます。 このような既定の制限を上書きするには、優先度の高い新しい制限を作成します。

## <a name="create-a-restriction"></a>制限を作成する

1. Azure ポータルにサインインします。
2. **[その他のサービス]** を選択し、**Intune** を検索して **[Intune]** を選択します。
3. **[デバイスの登録]** > **[登録の制限]** を選択します。
4. **[制限の作成]** を選択します。
5. 制限に名前付け、説明を加えます。
6. **[制限の種類]** を選択し、**[作成]** を選択します。
7. デバイス数の制限については、**[デバイスの制限]** を選択して、ユーザーが登録できるデバイスの最大数を設定します。
8. デバイスの種類の制限については、**[プラットフォーム]**、**[プラットフォーム構成]** の順に選択して、各種のプラットフォームおよびバージョンを許可またはブロックします。
9. **[割り当て]** > **[+ グループの選択]** を選択します。
10. **[グループの選択]** で、1 つ以上のグループを選択し、**[選択]** を選択します。 制限が適用されるのは、制限が割り当てられているグループのみです。 少なくとも 1 つのグループに割り当てていない限り、制限は何も影響しません。
11. **[保存]** を選択します。
12. 既定値の制限のすぐ上の優先度を持つ新しい制限が作成されます。 [優先度は変更](#change-enrollment-restriction-priority)することができます。

## <a name="set-device-type-restrictions"></a>デバイスの種類の制限を設定する

デバイスの種類の制限に対する設定は、次の手順で変更することができます。

1. Azure ポータルにサインインします。
2. **[その他のサービス]** を選択し、**Intune** を検索して **[Intune]** を選択します。
3. **[デバイスの登録]** > **[登録の制限]** を選択します。
4. **[デバイスの種類の制限]** で、設定する制限を選択します。
5. 制限の名前 (既定の制限の場合は **[すべてのユーザー]**) で、**[プラットフォーム]** を選択します。 一覧されたプラットフォームごとに、**[許可]** または **[ブロック]** を選択します。
6. **[保存]** を選択します。
7. 制限の名前 (既定の制限の場合は **[すべてのユーザー]**) で、**[プラットフォーム構成]** を選択します。 次に、リストされているプラットフォームの最小および最大の **[バージョン]** を選択します。 サポートされているバージョンは次のとおりです。
    - Android および Android for Work は、major.minor.rev.build をサポートします。
    - iOS では major.minor.rev がサポートされます。
    - Windows では major.minor.rev.build がサポートされます (Windows 10 の場合のみ)。
  オペレーティング システムのバージョンは、Device Enrollment Program、Apple School Manager、または Apple Configurator アプリを使用して登録する Apple デバイスには適用されません。
8. 一覧されているプラットフォームごとに、**個人所有**のデバイスを**許可**するか**ブロック**するかを指定します。
    ![個人所有設定の構成を示す既定デバイス プラットフォーム構成のデバイス制限ワークスペース](media/device-restrictions-platform-configurations.png)
9. **[保存]** を選択します。


>[!NOTE]
>- 個人所有の Android デバイスの登録をブロックした場合でも、個人所有の Android for Work デバイスは登録できます。
>- 既定では、Android for Work デバイス設定は Android デバイスの設定と同じになります。 Android for Work 設定の変更後は、同じではなくなります。
>- 個人の Android for Work 登録をブロックした場合、会社の Android デバイスのみを Android for Work として登録できます。

## <a name="set-device-limit-restrictions"></a>デバイス数の制限を設定する

デバイス数の制限の設定は、次の手順に従って変更できます。

1. Azure ポータルにサインインします。
2. **[その他のサービス]** を選択し、**Intune** を検索して **[Intune]** を選択します。
3. **[デバイスの登録]** > **[登録の制限]** を選択します。
4. **[デバイス数の制限]** で、設定する制限を選択します。
5. **[デバイスの制限]** を選択し、ドロップダウン リストで、ユーザーが登録できるデバイスの最大数を選択します。
    ![デバイス数の制限を示す [デバイス数の制限] ブレード](./media/device-restrictions-limit.png)
6. **[保存]** を選択します。


ユーザーがデバイス登録の上限に達すると、そのことを伝える通知が表示されます。 たとえば、iOS では次のようになります。

![iOS のデバイス制限通知](./media/enrollment-restrictions-ios-set-limit-notification.png)

## <a name="change-enrollment-restriction-priority"></a>登録制限の優先度を変更する

優先度は、制限が割り当てられた複数のグループにユーザーが存在する場合に使用されます。 ユーザーは、自分が属するグループに割り当てられている最も高い優先度の制限からのみ影響を受けます。 たとえば、Joe が優先度 5 の制限に割り当てられたグループ A に属しており、優先度 2 の制限に割り当てられたグループ B にも属しているとします。 Joe は優先度 2 の制限にのみ影響を受けます。

制限を作成すると、リストの既定の制限のすぐ上に追加されます。

デバイスの登録には、デバイスの種類の制限とデバイス数の制限の両方に対する既定の制限が含まれます。 これら 2 つの制限は、より高い優先度の制限で上書きされない限り、すべてのユーザーに適用されます。

既定以外の制限の優先度は、変更することができます。

1. Azure ポータルにサインインします。
2. **[その他のサービス]** を選択し、**Intune** を検索して **[Intune]** を選択します。
3. **[デバイスの登録]** > **[登録の制限]** を選択します。
4. 優先度リスト内の制限にマウス ポインタを移動させます。
5. 3 つの縦向きドットを使用して、リスト内の目的の位置に優先度をドラッグします。
