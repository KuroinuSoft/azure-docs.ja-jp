---
title: データのラベル付けプロジェクトを作成する
titleSuffix: Azure Machine Learning
description: ラベル付けプロジェクトを作成して実行し、機械学習用のデータにタグを付ける方法について説明します。
author: lobrien
ms.author: laobri
ms.service: machine-learning
ms.topic: tutorial
ms.date: 11/04/2019
ms.openlocfilehash: 864cccc4629140754a326823cbaebd7ad8933d3d
ms.sourcegitcommit: aee08b05a4e72b192a6e62a8fb581a7b08b9c02a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2020
ms.locfileid: "75765071"
---
# <a name="create-a-data-labeling-project-and-export-labels"></a>データのラベル付けプロジェクトを作成してラベルをエクスポートする 

多くの場合、機械学習プロジェクトで大量のデータにラベルを付けることは困難です。 画像の分類やオブジェクトの検出など、Computer Vision コンポーネントを使用するプロジェクトでは、通常、何千もの画像のラベルが必要になります。
 
[Azure Machine Learning](https://ml.azure.com/) を使用すると、ラベル付けプロジェクトの作成、管理、監視を一元的に行うことができます。 これを使用して、ラベル付けタスクを効率的に管理するためにデータ、ラベル、チーム メンバーを調整します。 Machine Learning では、画像の分類 (複数ラベルまたは複数クラス) のほか、境界ボックスと組み合わせたオブジェクトの識別がサポートされています。

Machine Learning では、進行状況を追跡し、未完了のラベル付けタスクのキューを管理します。 ラベラーは、参加するにあたって Azure アカウントは必要ありません。 自分の Microsoft アカウントまたは [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) での認証が済むと、時間が許す範囲でラベル付けを行うことができます。

Machine Learning では、プロジェクトの開始と停止、メンバーやチームの追加と削除、進行状況の監視を行います。 ラベル付きのデータは、COCO 形式または Azure Machine Learning データセットとしてエクスポートできます。

> [!Important]
> 現在サポートされているのは、画像分類とオブジェクト識別のラベル付けプロジェクトのみです。 加えて、Azure BLOB データストア内の画像データにアクセスできることが必要です。 (既存のデータストアがない場合は、プロジェクトの作成時に画像をアップロードすることができます。) 

この記事では、次の方法について学習します。

> [!div class="checklist"]
> * プロジェクトの作成
> * プロジェクトのデータと構造を指定する
> * プロジェクトに参加するチームとメンバーを管理する
> * プロジェクトを実行して監視する
> * ラベルをエクスポートする


## <a name="prerequisites"></a>前提条件

* ローカル ファイルまたは Azure Storage 内にある、ラベル付け対象のデータ。
* 適用するラベルのセット。
* ラベル付けに関する指示。
* Azure サブスクリプション。 Azure サブスクリプションがない場合は、開始する前に[無料アカウント](https://aka.ms/AMLFree)を作成してください。
* Machine Learning ワークスペース。 [Azure Machine Learning ワークスペースを作成する](how-to-manage-workspace.md)方法に関するページを参照してください。

## <a name="create-a-labeling-project"></a>ラベル付けプロジェクトを作成する

ラベル付けプロジェクトは、Azure Machine Learning から管理します。 **[Labeling projects]\(ラベル付けプロジェクト\)** ページを使用して、プロジェクトとメンバーを管理します。 プロジェクトには 1 つまたは複数のチームが割り当てられ、チームには 1 人以上のユーザーが割り当てられます。

データが既に Azure Blob Storage 内にある場合は、ラベル付けプロジェクトを作成する前に、それをデータストアとして使用できるようにする必要があります。 詳細については、「[データストアの作成と登録](https://docs.microsoft.com/azure/machine-learning/how-to-access-data#create-and-register-datastores)」を参照してください。

プロジェクトを作成するには、 **[プロジェクトの追加]** を選択します。 プロジェクトに適切な名前を付け、 **[ラベル付けタスクの種類]** を選択します。

![ラベル付けプロジェクト作成ウィザード](./media/how-to-create-labeling-projects/labeling-creation-wizard.png)

* クラスのセットから "*1 つ以上*" のラベルを画像に適用する場合は、プロジェクトに対して **[Image Classification Multi-label]\(イメージ分類複数ラベル\)** を選択します。 たとえば、犬の写真には "*犬*" と "*日中*" の両方のラベルが付けられる可能性があります。
* クラスのセットから "*1 つのクラス*" だけを画像に適用する場合は、プロジェクトに対して **[イメージ分類の複数クラス]** を選択します。
* 画像内の各オブジェクトにクラスと境界ボックスを割り当てる場合は、プロジェクトに対して **[オブジェクト ID (四角形領域)]** を選択します。

続行する準備ができたら、 **[次へ]** を選択します。

## <a name="specify-the-data-to-label"></a>ラベル付けの対象データを指定する

対象のデータが含まれるデータセットを既に作成済みの場合は、 **[既存のデータセットを選択します]** ボックスの一覧から選択します。 または、 **[Create a dataset]\(データセットの作成\)** を選択して、既存の Azure データストアを選択するか、ローカル ファイルをアップロードします。

### <a name="create-a-dataset-from-an-azure-datastore"></a>Azure データストアからデータセットを作成する

多くの場合は、ローカル ファイルをアップロードするだけでかまいません。 ただし、[Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) には、大量のデータをより高速かつ堅牢に転送する方法が用意されています。 既定のファイル移動方法としては、Storage Explorer をお勧めします。

Azure Blob Storage に既に格納済みのデータからデータセットを作成するには:

1. **[Create a dataset]\(データセットの作成\)**  >  **[From datastore]\(データストアから\)** の順に選択します。
1. データセットに**名前**を割り当てます。
1. **[データセットの種類]** として **[ファイル]** を選択します。  
1. データストアを選択します。
1. データがお使いの Blob Storage 内のサブフォルダーにある場合は、 **[参照]** を選択してパスを選択します。
    * 選択したパスのサブフォルダー内にあるすべてのファイルを含めるには、パスの末尾に "/**" を追加します。
    * 現在のコンテナーとそのサブフォルダー内にあるすべてのデータを含めるには、"* */* .*" を追加します。
1. データセットの説明を入力します。
1. **[次へ]** を選択します。
1. 詳細を確認します。 **[戻る]** を選択して設定を変更するか、 **[作成]** を選択してデータセットを作成します。

### <a name="create-a-dataset-from-uploaded-data"></a>アップロードしたデータからデータセットを作成する

データを直接アップロードするには:

1. **[Create a dataset]\(データセットの作成\)**  >  **[From local files]\(ローカル ファイルから\)** の順に選択します。
1. データセットに**名前**を割り当てます。
1. **[データセットの種類]** として [ファイル] を選択します。
1. *省略可能:* **[詳細設定]** を選択して、データストア、コンテナー、およびデータへのパスをカスタマイズします。
1. **[参照]** を選択し、アップロードするローカル ファイルを選択します。
1. データセットの説明を入力します。
1. **[次へ]** を選択します。
1. 詳細を確認します。 **[戻る]** を選択して設定を変更するか、 **[作成]** を選択してデータセットを作成します。

データは、Machine Learning ワークスペースの既定の BLOB ストア ("workspaceblobstore") にアップロードされます。

## <a name="specify-label-classes"></a>ラベル クラスを指定する

**[ラベル クラス]** ページで、データを分類するためのクラスのセットを指定します。 これは慎重に行ってください。適切なクラスを選択できるかどうかが、ラベラーの制約さと速さに影響します。 たとえば、植物や動物の属や種を略さずに使用するのではなく、フィールド コードを使用したり属を省略したりします。

ラベルは 1 行に 1 つずつ入力します。 新しい行を追加するには、 **[+]** ボタンを使用します。 ラベルの数が 3 または 4 以上 10 未満の場合は、名前の前に数字 ("1: "、"2: ") を付けることで、ラベラーが数字キーを使用して作業を高速化できるようになります。

## <a name="describe-the-labeling-task"></a>ラベル付けタスクを説明する

ラベル付けタスクをわかりやすく説明することが重要です。 **[ラベル付けの手順]** ページで、ラベル付けの手順に関する外部サイトへのリンクを追加できます。 指示は、タスク指向で、対象ユーザーに適したものにします。 次の質問を考慮してください。

* どのようなラベルが表示され、どのような方法で選択しますか。 参照する参照テキストはありますか。
* 適切なラベルが見あたらない場合はどうすればよいですか。
* 適切に見えるラベルが複数ある場合はどうすればよいですか。
* どのような信頼度しきい値をラベルに適用する必要がありますか。 確実にわからない場合は、"最善の推測" で選択させますか。
* 対象のオブジェクトが部分的にオクルージョンされている場合、または重なっている場合は、どうすればよいですか。
* 対象のオブジェクトが画像の端によってクリップされている場合は、どうすればよいですか。
* ラベルを送信した後に間違いに気付いた場合はどうすればよいですか。

境界ボックスについては、次のような重要な質問があります。

* このタスクでは境界ボックスはどのように定義されていますか。 完全にオブジェクトの内側に配置すべきですか、それとも外側に配置するべきですか。 できるだけ近くなるようにトリミングする必要がありますか、それともある程度の余白は許容されますか。
* 境界ボックスを定義する際にラベラーがどの程度の注意と一貫性を適用することを期待しますか。

>[!NOTE]
> ラベラーは最初の 9 つのラベルを 1 から 9 の数字キーを使用して選択できることを必ず明記してください。

## <a name="initialize-the-labeling-project"></a>ラベル付けプロジェクトを初期化する

ラベル付けプロジェクトが初期化された後、プロジェクトのいくつかの部分は変更できなくなります。 タスクの種類やデータセットを変更することはできません。 ラベルや、タスクの説明の URL は変更 "*できます*"。 プロジェクトを作成する前に、設定を慎重に確認してください。 プロジェクトを送信すると、 **[Labeling]\(ラベル付け\)** ホーム ページに戻り、プロジェクトが **[Initializing]\(初期化中\)** と表示されます。 このページが自動的に更新されることはありません。 そのため、しばらくしてからページを手動で更新すると、プロジェクトの状態が **[Created]\(作成済み\)** と表示されます。

## <a name="manage-teams-and-people"></a>チームとユーザーを管理する

作成した各ラベル付けプロジェクトには、既定で、自分がメンバーである新しいチームが作成されます。 ただし、チームはプロジェクト間で共有することもできます。 また、プロジェクトには複数のチームを設定できます。 チームを作成するには、 **[チーム]** ページで **[チームを追加]** を選択します。

メンバーは、 **[People]\(メンバー\)** ページで管理します。 メンバーの追加と削除には、メール アドレスを使用します。 各ラベラーは、お使いの Microsoft アカウントまたは Azure Active Directory (使用している場合) を使用して認証を行う必要があります。  

メンバーを追加した後、そのメンバーを 1 つ以上のチームに割り当てることができます。 **[チーム]** ページに移動し、チームを選択した後、 **[Assign people]\(メンバーの割り当て\)** または **[Remove people]\(メンバーの削除\)** を選択します。

チームにメールを送信するには、チームを選択して **[チームの詳細]** ページを表示します。 このページで **[Email team]\(チームへのメール送信\)** を選択して、チーム全員のアドレスが設定されたメールの下書きを開きます。

## <a name="run-and-monitor-the-project"></a>プロジェクトを実行して監視する

プロジェクトを初期化すると、Azure によって実行が開始されます。 メインの **[Labeling]\(ラベル付け\)** ページでプロジェクトを選択して、 **[プロジェクトの詳細]** に移動します。 **[ダッシュボード]** タブに、ラベル付けタスクの進行状況が表示されます。

**[データ]** タブでは、データセットを表示して、ラベル付けされたデータを確認できます。 間違ってラベル付けされたデータが表示された場合は、それを選択して **[拒否]** を選択することで、ラベルを削除し、データをラベルなしのキューに戻すことができます。

プロジェクトに対するチームの割り当てまたは割り当て解除を行うには、 **[チーム]** タブを使用します。

プロジェクトを一時停止または再開するには、 **[一時停止]** / **[開始]** ボタンを選択します。 データにラベルを付けることができるのは、プロジェクトが実行されているときだけです。

**[Project details]\(プロジェクトの詳細\)** ページで **[Label data]\(データのラベル付け\)** を選択することにより、データに直接ラベルを付けることができます。

## <a name="export-the-labels"></a>ラベルをエクスポートする

いつでも、Machine Learning の実験用にラベル データをエクスポートできます。 画像のラベルは、[COCO 形式](http://cocodataset.org/#format-data)または Azure Machine Learning データセットとしてエクスポートできます。 ラベル付けプロジェクトの **[プロジェクトの詳細]** ページにある **[エクスポート]** ボタンを使用します。

COCO ファイルは、Azure Machine Learning ワークスペースの既定の BLOB ストアにある *export/coco* 内のフォルダーに作成されます。 エクスポートした Azure Machine Learning データセットには、Machine Learning の **[データセット]** セクションでアクセスできます。 また、データセットの詳細ページには、Python からラベルにアクセスするためのサンプル コードも表示されます。

![エクスポートされたデータセット](./media/how-to-create-labeling-projects/exported-dataset.png)

## <a name="next-steps"></a>次のステップ

* [画像の分類またはオブジェクトの検出](how-to-label-images.md)のために、画像にラベルを付けます
* [Azure Machine Learning と Machine Learning Studio (クラシック)](compare-azure-ml-to-studio-classic.md) について学習します
