---
lab:
  title: 探索認知服務
---

# <a name="explore-cognitive-services"></a>探索認知服務

> **注意** 若要完成此實驗室，您需要一個具備[系統管理存取權](https://azure.microsoft.com/free?azure-portal=true)的 Azure 訂用帳戶。

Azure 認知服務封裝常用的 AI 功能，分為四大類：視覺、語音、語言和決策服務。 在此練習中，您將看一下其中一項決策服務，以大致瞭解如何在軟體應用程式中佈建和使用認知服務資源。

您在此練習中要探索的特定認知服務是「異常偵測器」。 異常偵測器用來分析一段時間的資料值，以及偵測可能表示有問題或情況需要進一步調查的任何異常值。 例如，溫度控制貯存設備中的感應器可能每分鐘監視溫度，並記錄測量的值。 您可以使用異常偵測器服務來分析記錄的溫度值，並標幟明顯超出正常預期溫度範圍的任何值。

為了測試異常偵測服務的功能，我們會使用在 Cloud Shell 中執行的簡單命令列應用程式。 真實世界的解決方案也適用相同準則和功能，例如網站或手機應用程式。

> **注意** 本練習的目標是要大致瞭解認知服務的佈建和使用方式。 異常偵測器只是舉例，此練習不可能讓您澈底了解異常偵測！

## <a name="create-an-anomaly-detector-resource"></a>建立*異常偵測器*資源

首先，在 Azure 訂用帳戶中建立**異常偵測器**資源：

1. 在另一個瀏覽器索引標籤中，開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. 按一下 [&#65291;建立資源] 按鈕，搜尋「異常偵測器」，然後使用下列設定建立**異常偵測器**資源：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取現有資源群組或建立新的資源群組*。
    - **區域**：選擇任何可用的區域。
    - **名稱**：*輸入唯一名稱*。
    - **定價層**：免費 F0

1. 檢閱並建立資源。 等候部署完成，然後移至部署的資源。

1. 檢視異常偵測器資源的 [金鑰和端點] 頁面。 您需要有端點和金鑰，才能從用戶端應用程式連線。

## <a name="run-cloud-shell"></a>執行 Cloud Shell

為了測試異常偵測器服務的功能，我們會使用在 Azure 的 Cloud Shell 中執行的簡單命令列應用程式。

1. 在 Azure 入口網站中，選取頁面頂端在搜尋方塊右邊的 **[>_]** (Cloud Shell) 按鈕。 這會在入口網站底部開啟 Cloud Shell 窗格。

    ![按一下頂端搜尋方塊右側的圖示來啟動 Cloud Shell](media/anomaly-detector/powershell-portal-guide-1.png)

1. 第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 選取 [PowerShell]。 如果沒有看到此選項，請略過該步驟。  

1. 如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂用帳戶，然後選取 [建立儲存體]。 然後，請等候一分鐘左右，讓系統建立儲存體。

    ![按一下確認以建立儲存體。](media/anomaly-detector/powershell-portal-guide-2.png)

1. 請確定 Cloud Shell 窗格左上方所指出的殼層類型已切換為 *PowerShell*。 如果其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    ![如何尋找左側下拉式功能表來切換至 PowerShell](media/anomaly-detector/powershell-portal-guide-3.png)

1. 等候 PowerShell 啟動。 您應該會在 Azure 入口網站中看到下列畫面：  

    ![等候 PowerShell 啟動。](media/anomaly-detector/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>設定和執行用戶端應用程式

現在您已擁有 Cloud Shell 環境，接下來可執行簡單的應用程式，以使用異常偵測器服務來分析資料。

1. 在命令殼層中，輸入下列命令以下載範例應用程式，並將其儲存至名為 ai-900 的資料夾。

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**提示** 若您已在另一個實驗室中使用此命令來複製 *ai-900* 存放庫，則可跳過此步驟。

1. 檔案會下載至名為 **ai-900** 的資料夾。 現在我們想要查看 Cloud Shell 儲存體中的所有檔案，並使用這些檔案。 在殼層中輸入下列命令：

     ```PowerShell
    code .
    ```

    請注意此命令如何開啟編輯器，情況如下圖： 

    ![程式碼編輯器。](media/anomaly-detector/powershell-portal-guide-4.png)

1. 在左側的 [檔案] 窗格中，展開 **ai-900**，並選取 **detect-anomalies.ps1**。 此檔案包含一些使用異常偵測服務的程式碼，如下所示：

    ![編輯器包含程式碼以偵測異常](media/anomaly-detector/detect-anomalies-code.png)

1. 無須顧慮程式碼的細節，重要的是需要有端點 URL，以及異常偵測器資源的其中一個金鑰。 從資源的 [金鑰和端點] 頁面 (應該仍在瀏覽器頂端) 複製上述資訊，並貼到程式碼編輯器中，分別取代 **YOUR_KEY** 和 **YOUR_ENDPOINT** 預留位置值。

    > **提示** 使用 [金鑰和端點] 與 [編輯器] 窗格時，您可能必須使用分隔線來調整螢幕區域。

    在貼上金鑰和端點值之後，程式碼的前兩行應該會類似下列內容：

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. 在編輯器窗格右上方，使用 [...] 按鈕開啟功能表，然後選取 [儲存] 以儲存變更。 然後再次開啟功能表，並選取 [關閉編輯器]。

    請記得，異常偵測是一種人工智慧技術，可用於判斷數列中的值是否在預期的參數內。 範例用戶端應用程式會使用您的異常偵測器服務，以分析包含一系列日期/時間和數值的檔案。 應用程式應會傳回結果，並指出每個時間點數值是否在預期的參數內。

1. 在 PowerShell 窗格中，輸入下列命令來執行程式碼：

    ```PowerShell
    cd ai-900
    .\detect-anomalies.ps1
    ```

1. 檢閱結果並注意結果中的最後一個資料行為 **True** 或 **False**，顯示各日期/時間的記錄值是否視為異常。 請考慮如何在實際情況下使用這項資訊。 若偵測到冰箱溫度或壓力和異常值，應用程式可能會觸發哪些動作？  

## <a name="learn-more"></a>深入了解

這個簡單的應用程式只展示了異常偵測器服務的一些功能。 若要深入了解這項服務的功能，請參閱[異常偵測器頁面](https://azure.microsoft.com/services/cognitive-services/anomaly-detector/)。

## <a name="clean-up"></a>清理

建議您在專案結束後確認是否還需要您所建立的資源。 資源若繼續執行，您將必須付費。 

如果要繼續「AI 基本概念」的其他課程模組，您可以將資源保留在其他實驗室中使用。

如果您已完成學習，您可以從 Azure 訂用帳戶中刪除整個資源群組或個別資源：

1. 在 [Azure 入口網站](https://portal.azure.com/)的 [資源群組] 頁面中，開啟在建立資源時所指定的資源群組。

2. 按一下 [刪除資源群組]、輸入資源群組名稱以確認要刪除，然後選取 [刪除]。 您也可以選取資源、按一下三個點狀的圖示以查看更多選項，然後按一下 [刪除] 來刪除個別資源。