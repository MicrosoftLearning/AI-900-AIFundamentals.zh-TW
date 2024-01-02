---
lab:
  title: 探索表單辨識
---

# 探索表單辨識

> **注意** 若要完成此實驗室，您需要一個具備[系統管理存取權](https://azure.microsoft.com/free?azure-portal=true)的 Azure 訂用帳戶。

在電腦視覺的人工智慧 (AI) 領域中，光學字元辨識 (OCR) 通常用於讀取印刷或手寫文件。 通常只會從文件中將文字擷取成可用來進一步處理或分析的格式。

更進階的 OCR 案例是從表單擷取資訊，例如採購單或發票，以及語意了解表單中欄位所代表的內容。 **表格辨識器**服務是特別針對這種 AI 問題所設計。

表格辨識器會使用定型的機器學習模型，從發票、收據等影像中擷取文字。 雖然其他電腦視覺模型可以擷取文字，但表格辨識器也會擷取文字的結構，例如資料表中的索引鍵/值組和資訊。 如此一來，您不必將表單中的項目手動輸入到資料庫中，而是可以自動擷取原始檔案中文字之間的關聯性。 

為了測試表格辨識器服務的功能，我們會使用 Cloud Shell 中執行的簡單命令列應用程式。 真實世界的解決方案也適用相同準則與功能，例如網站或手機應用程式。

## 建立 *Azure AI 服務*資源

您可以藉由建立 **表格辨識器 資源或 **Azure AI 服務資源，來使用 表格辨識器** 服務**。

如果您尚未建立此資源，請在 Azure 訂閱中建立 **Azure AI 服務**資源。

1. 在另一個瀏覽器索引標籤中，開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. 按一下 **＋建立資源 **按鈕並搜尋  * Azure AI 服務 *。 選取**建立** **Azure AI 服務**方案。 系統會帶您前往建立 Azure AI 服務資源的頁面。 使用下列設定對其進行設定：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：選擇任何可用的區域**。
    - **名稱**：*輸入唯一名稱*。
    - **定價層**:標準 S0
    - **核取此方塊表示我已閱讀並了解下列所有條款**：選取。

1. 檢閱並建立資源，然後等候部署完成。 接著，移至所部署的資源。

1. 檢視 Azure AI 服務資源的**金鑰與端點**頁面。 您需要有端點和金鑰，才能從用戶端應用程式連線。

## 執行 Cloud Shell

為了測試表格辨識器服務的功能，我們會使用 Azure Cloud Shell 中執行的簡單命令列應用程式。 

1. 在 Azure 入口網站中，選取頁面頂端在搜尋方塊右邊的 **[>_]** (Cloud Shell**) 按鈕。 這會在入口網站底部開啟 Cloud Shell 窗格。 

    ![按一下頂端搜尋方塊右側的圖示來啟動 Cloud Shell](media/analyze-receipts/powershell-portal-guide-1.png)

1. 第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 選取 [PowerShell]****。 若未看到此選項，請略過該步驟。  

1. 如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂用帳戶，然後選取 [建立儲存體]****。 然後等候一分鐘左右，讓系統建立儲存體。

    ![按一下確認以建立儲存體。](media/analyze-receipts/powershell-portal-guide-2.png)

1. 請確認 [Cloud Shell] 窗格左上方指出的殼層類型已切換為 [PowerShell]**。 若其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    ![如何尋找左側下拉式功能表來切換至 PowerShell](media/analyze-receipts/powershell-portal-guide-3.png) 

1. 等候 PowerShell 啟動。 您應該會在 Azure 入口網站中看到下列畫面：  

    ![等候 PowerShell 啟動。](media/analyze-receipts/powershell-prompt.png) 

## 設定和執行用戶端應用程式

現在您已擁有自訂模型，即可執行使用表格辨識器服務的簡單用戶端應用程式。

1. 在命令殼層中，輸入下列命令以下載範例應用程式，並將其儲存至名為 ai-900 的資料夾。

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    >**提示** 若您已在另一個實驗室中使用此命令來複製 *ai-900* 存放庫，則可跳過此步驟。

1. 檔案會下載到名為 **ai-900** 的資料夾。 現在我們要查看 Cloud Shell 儲存體中的所有檔案，並使用這些檔案。 在殼層中輸入下列命令：

    ```PowerShell
    code .
    ```

    請注意此命令如何開啟編輯器，如下圖： 

    ![程式碼編輯器。](media/analyze-receipts/powershell-portal-guide-4.png)

1. 在左側的 [檔案]**** 窗格中，展開 **ai-900**，然後選取 **form-recognizer.ps1**。 此檔案包含一些程式碼，會使用表格辨識器服務來分析收據中的欄位，如下所示：

    ![編輯器包含程式碼來分析收據中的欄位。](media/analyze-receipts/recognize-receipt-code.png)

1. 不要太擔心程式代碼的詳細數據，重要的是它需要端點 URL 和 Azure AI 服務資源的其中一個密鑰。 從 Azure 入口網站資源的 [金鑰和端點]**** 頁面複製上述資訊，並貼到程式碼編輯器中，分別取代 **YOUR_KEY** 和 **YOUR_ENDPOINT** 預留位置值。

    > **提示** 使用 [金鑰和端點]**** 與 [編輯器]**** 窗格時，您可能必須使用分隔線來調整螢幕區域。

    在貼上金鑰和端點值後，程式碼的前兩行應會類似下列內容：

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. 在編輯器窗格右上方，使用 [...]**** 按鈕開啟功能表，並選取 [儲存]**** 以儲存變更。 接著再次開啟功能表，並選取 [關閉編輯器]****。 現在您已設定金鑰和端點，即可使用資源來分析收據中的欄位。 在此情況下，您將使用表格辨識器的內建模型來分析虛構 Northwind Traders 零售公司的收據。

    範例用戶端應用程式會分析下列影像：

    ![這是收據的影像。](media/analyze-receipts/receipt.jpg)

1. 在 [PowerShell] 窗格中，輸入下列命令來執行程式碼以讀取文字：

    ```PowerShell
    cd ai-900
    ./form-recognizer.ps1
    ```

1. 檢閱所傳回的結果。 知悉表格辨識器能夠解譯表單中的資料、正確識別商家地址和電話號碼，以及交易日期和時間，還有商品明細、小計、稅金和總金額。

## 深入了解

此簡單的應用程式只說明部分電腦視覺服務的表單辨識器功能。 若要深入了解這項服務的功用，請參閱[表單辨識器頁面](https://docs.microsoft.com/azure/applied-ai-services/form-recognizer/overview)。

