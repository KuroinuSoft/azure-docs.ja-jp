---
title: セキュリティ - Azure Database for MySQL
description: Azure Database for MySQL のセキュリティ機能の概要。
author: ajlam
ms.author: andrela
ms.service: mysql
ms.topic: conceptual
ms.date: 12/02/2019
ms.openlocfilehash: fb0a71a650a8c36d4da962adaf3f1f314c30d4c2
ms.sourcegitcommit: 3dc1a23a7570552f0d1cc2ffdfb915ea871e257c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2020
ms.locfileid: "75980004"
---
# <a name="security-in-azure-database-for-mysql"></a>Azure Database for MySQL のセキュリティ

Azure Database for MySQL サーバーには、データを保護するために使用できるセキュリティのレイヤーが複数あります。 この記事では、これらのセキュリティ オプションについてまとめています。

## <a name="information-protection-and-encryption"></a>情報の保護と暗号化

### <a name="in-transit"></a>転送中
Azure Database for MySQL では、トランスポート層セキュリティを使用して転送中のデータを暗号化することによってデータをセキュリティで保護します。 既定では、暗号化 (SSL/TLS) が適用されます。

### <a name="at-rest"></a>保存
Azure Database for MySQL サービスでは、保存データのストレージ暗号化に FIPS 140-2 認証済みの暗号モジュールが使用されます。 バックアップを含むデータは、クエリの実行中に作成された一時ファイルを除き、ディスク上で暗号化されます。 このサービスでは、Azure ストレージ暗号化に含まれる AES 256 ビット暗号が使用され、キーはシステムによって管理されます。 ストレージの暗号化は常にオンになっており、無効にすることはできません。


## <a name="network-security"></a>ネットワークのセキュリティ
Azure Database for MySQL サーバーへの接続は、最初にリージョン ゲートウェイ経由でルーティングされます。 サーバーの IP アドレスは保護されていますが、ゲートウェイにはパブリックにアクセス可能な IP があります。 ゲートウェイの詳細については、[接続アーキテクチャに関する記事](concepts-connectivity-architecture.md)をご覧ください。  

新しく作成された Azure Database for MySQL サーバーには、すべての外部接続をブロックするファイアウォールが備わっています。 ゲートウェイに到達しますが、サーバーへの接続は許可されません。 

### <a name="ip-firewall-rules"></a>IP ファイアウォール規則
IP ファイアウォール規則では、各要求の送信元 IP アドレスに基づいてサーバーへのアクセス権を付与します。 詳細については、[ファイアウォール規則の概要](concepts-firewall-rules.md)に関するページを参照してください。

### <a name="virtual-network-firewall-rules"></a>仮想ネットワーク ファイアウォールの規則
仮想ネットワーク サービス エンドポイントにより、Azure バックボーンを介して仮想ネットワーク接続が拡張されます。 仮想ネットワークの規則を使用して、仮想ネットワーク内の選択したサブネットからの接続を許可するように、Azure Database for MySQL サーバーを有効にすることができます。 詳細については、[仮想ネットワーク サービス エンドポイントの概要](concepts-data-access-and-security-vnet.md)に関するページを参照してください。

### <a name="private-ip"></a>プライベート IP
Private Link を使用すると、プライベート エンドポイントを経由して Azure 内の Azure Database for MySQL に接続できます。 Azure Private Link は基本的に、プライベート仮想ネットワーク (VNet) 内に Azure サービスを提供します。 PaaS リソースには、VNet 内のその他のリソースと同様に、プライベート IP アドレスを使用してアクセスできます。 詳細については、「[Private Link の概要](concepts-data-access-security-private-link.md)」を参照してください

## <a name="access-management"></a>アクセス管理

Azure Database for MySQL サーバーを作成するときに、管理者ユーザーの資格情報を指定します。 この管理者は、追加の MySQL ユーザーを作成するために使用できます。


## <a name="threat-protection"></a>脅威の防止

サーバーにアクセスしたり悪用したりしようとする、通常とは異なる、害を及ぼす可能性のある試行を示す異常なアクティビティを検出する [Advanced Threat Protection](concepts-data-access-and-security-threat-protection.md) にオプトインできます。

[監査ログ](concepts-audit-logs.md)を使うと、データベースのアクティビティを追跡できます。 


## <a name="next-steps"></a>次のステップ
- [IP](concepts-firewall-rules.md) または[仮想ネットワーク](concepts-data-access-and-security-vnet.md)のファイアウォール規則を有効にする