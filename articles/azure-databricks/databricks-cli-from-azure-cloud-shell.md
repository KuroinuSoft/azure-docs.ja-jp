---
title: 'Azure Cloud Shell からの Databricks CLI の使用 '
description: Azure Cloud Shell から Databricks CLI を使用して Azure Databricks で操作を実行する方法を説明します。
services: azure-databricks
author: mamccrea
ms.reviewer: jasonh
ms.service: azure-databricks
ms.workload: big-data
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: mamccrea
ms.openlocfilehash: efb0d3222bfd98b15502163979425d47fa459e07
ms.sourcegitcommit: c62a68ed80289d0daada860b837c31625b0fa0f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73605714"
---
# <a name="use-databricks-cli-from-azure-cloud-shell"></a>Azure Cloud Shell からの Databricks CLI の使用

Azure Cloud Shell から Databricks CLI を使用して Databricks で操作を実行する方法を説明します。

## <a name="prerequisites"></a>前提条件

* Azure Databricks ワークスペースおよびクラスター。 手順については、[Azure Databricks のクイックスタート](quickstart-create-databricks-workspace-portal.md)に関するページをご覧ください。 

* Databricks に個人用アクセス トークンを設定します。 手順については、[トークンの管理](/azure/databricks/dev-tools/api/latest/authentication)に関するページをご覧ください。

## <a name="use-the-azure-cloud-shell"></a>Azure Cloud Shell の使用

1. [Azure Portal](https://portal.azure.com) にログインします。
 
2. 右上隅で **Cloud Shell** のアイコンをクリックします。

   ![Cloud Shell の起動](./media/databricks-cli-from-azure-cloud-shell/launch-azure-cloud-shell.png "Azure Cloud Shell を起動する")

3. Cloud Shell 環境として **[Bash]** を選択してください。 次のスクリーンショットに示すようにドロップダウン リストから選択できます。

   ![Cloud Shell 環境として Bash を選択](./media/databricks-cli-from-azure-cloud-shell/select-bash-for-shell.png "Bash を選びます") 

4. Databricks CLI をインストールする仮想環境を作成します。 次のスニペットでは、`databrickscli` という仮想環境を作成しています。

       virtualenv -p /usr/bin/python2.7 databrickscli

5. 作成した仮想環境に切り替えます。

       source databrickscli/bin/activate

6. Databricks CLI をインストールします。

       pip install databricks-cli

7. 前提条件の一部として作成していたはずのアクセス トークンを使用して、Databricks に対する認証を設定します。 次のコマンドを使用します。

       databricks configure --token

    次のプロンプトが表示されます。

    * まず、Databricks ホストを入力するように求められます。 `https://eastus2.azuredatabricks.net` の形式で値を入力します。 ここでは、**米国東部 2** が、Azure Databricks ワークスペースが作成された Azure リージョンです。

    * 次に、トークンを入力するように求められます。 前に作成したトークンを入力します。

これらの手順を完了すると、Azure Cloud Shell から Databricks CLI の使用を開始できます。

## <a name="use-databricks-cli"></a>Databricks CLI の使用

Databricks CLI の使用を開始できます。 たとえば、次のコマンドを実行すると、ワークスペース内にあるすべての Databricks クラスターを一覧表示できます。

    databricks clusters list

また、次のコマンドを使用すると、Databricks ファイルシステム (DBFS) にアクセスできます。

    databricks fs ls


コマンドの完全なリファレンスについては、「[Databricks CLI](/azure/databricks/dev-tools/databricks-cli)」をご覧ください。


## <a name="next-steps"></a>次の手順

* Azure CLI について詳しくは、[Azure CLI の概要](../cloud-shell/overview.md)に関するページをご覧ください。
* Azure CLI のコマンド一覧を確認するには、[Azure CLI リファレンス](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)のページをご覧ください。
* Databricks CLI のコマンド一覧を確認するには、[Databricks CLI](/azure/databricks/dev-tools/databricks-cli) のページをご覧ください。


