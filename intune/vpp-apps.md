---
title: Microsoft Intune によるボリューム購入アプリとブックの管理
titlesuffix: ''
description: Microsoft Intune を使用して、ストアからのボリューム購入アプリとブックの使用状況を管理および監視する方法について説明します。"
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/15/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 85b07f57-661a-4bc8-87d2-7b446d5cf4d6
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 39478853531d924806b34c64253a128c4e7afc8e
ms.sourcegitcommit: 34e96e57af6b861ecdfea085acf3c44cff1f3d43
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
# <a name="manage-volume-purchased-apps-and-books-with-microsoft-intune"></a>Microsoft Intune によるボリューム購入アプリとブックの管理

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

## <a name="introduction"></a>概要

一部のアプリ ストアでは、社内で使用するアプリやブックの複数のライセンスを購入できます。 ライセンスの一括購入は、購入したアプリとブックの複数コピーを追跡する管理オーバーヘッドを削減するのに役立ちます。

Microsoft Intune を使用することで、このようなプログラムを通じて購入したアプリとブックを管理できます。 ストアからライセンス情報をインポートし、使用したライセンスの数を追跡できます。 このプロセスにより、所有している数より多くのアプリまたはブックのコピーがインストールされないようにできます。

## <a name="which-types-of-apps-and-books-can-you-manage"></a>管理できるアプリとブックの種類

Intune では、iOS ストアからボリューム購入したアプリとブックを管理し、ビジネス向け Microsoft ストアからボリューム購入したアプリを管理できます。 各ストアからライセンスを購入したアプリを管理する方法については、次のトピックのいずれかをご覧ください。

- [iOS のボリューム購入アプリの管理](vpp-apps-ios.md)
- [ビジネス向け Microsoft ストアからボリューム購入したアプリの管理](windows-store-for-business.md)
- [Volume Purchase Program で購入した iOS 電子ブックを Microsoft Intune で管理する方法](vpp-ebooks-ios.md)
