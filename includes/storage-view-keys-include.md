---
title: インクルード ファイル
description: インクルード ファイル
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 11/06/2019
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: e3b3d944508a4261b78def0b3bee13f7395a8bf0
ms.sourcegitcommit: 827248fa609243839aac3ff01ff40200c8c46966
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73749006"
---
Azure portal からストレージ アカウントのアクセス キーまたは接続文字列を表示およびコピーするには:

1. [Azure Portal](https://portal.azure.com) に移動します。
2. 自分のストレージ アカウントを探します。
3. ストレージ アカウントの概要の **[設定]** セクションで、 **[アクセス キー]** を選択します。 アカウント アクセス キーと、各キーの完全な接続文字列が表示されます。
4. **[key1]** で **[キー]** 値を見つけ、 **[コピー]** ボタンをクリックしてアカウント キーをコピーします。
5. あるいは、接続文字列全体をコピーできます。 **[Key1]** の **[接続文字列]** の値を見つけて **[コピー]** ボタンをクリックし、接続文字列をコピーします。

    ![Azure portal でアクセス キーを表示する方法を示したスクリーンショット](media/storage-view-keys-include/portal-connection-string.png)

どちらのキーを使用して Azure Storage にアクセスすることもできますが、一般的には、最初のキーを使用し、キーのローテーション時に 2 番目のキーの使用を予約することをお勧めします。
