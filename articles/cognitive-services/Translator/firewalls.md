---
title: ファイアウォールの内側で翻訳する - Translator Text API
titleSuffix: Azure Cognitive Services
description: Azure Cognitive Services Translator Text API による翻訳は、ドメイン名フィルタリングまたは IP フィルタリングを使用して、ファイアウォールの内側で実行できます。
services: cognitive-services
author: swmachan
manager: nitinme
ms.service: cognitive-services
ms.subservice: translator-text
ms.topic: conceptual
ms.date: 06/04/2019
ms.author: swmachan
ms.openlocfilehash: cd7904fedd3ab3f64315cb6f98d99b8fd12254f6
ms.sourcegitcommit: 35715a7df8e476286e3fee954818ae1278cef1fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73837397"
---
# <a name="how-to-translate-behind-ip-firewalls-with-the-translator-text-api"></a>IP ファイアウォールの内側で Translator Text API を使用して翻訳する方法

Translator Text API による翻訳は、ドメイン名フィルタリングまたは IP フィルタリングを使用して、ファイアウォールの内側で実行できます。 可能であればドメイン名フィルタリングの使用をお勧めします。 IP フィルタリング ファイアウォールの内側から Microsoft Translator を実行することは**お勧めしません**。 この構成は将来、予告なく動作不能になる可能性があります。

## <a name="translator-ip-addresses"></a>Translator の IP アドレス
2019 年 8 月 21 日における api.cognitive.microsofttranslator.com (Microsoft Translator Text API) の IP アドレスは次のとおりです。

* **アジア太平洋:** 20.40.125.208、20.43.88.240、20.184.58.62、40.90.139.163、104.44.89.44
* **ヨーロッパ:** 40.90.138.4、40.90.141.99、51.105.170.64、52.155.218.251
* **北米:** 40.90.139.36、40.90.139.2、40.119.2.134、52.224.200.129、52.249.207.163


## <a name="next-steps"></a>次の手順
> [!div class="nextstepaction"]
> [IP ファイアウォールの内側から Translator API 呼び出しで翻訳する](reference/v3-0-translate.md)
