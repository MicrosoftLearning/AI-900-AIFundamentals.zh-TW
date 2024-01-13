---
lab:
  title: 探索光學字元辨識
---

# 探索光學字元辨識

> **注意** 若要完成此實驗室，您需要一個具備[系統管理存取權](https://azure.microsoft.com/free?azure-portal=true)的 Azure 訂用帳戶。

常見的電腦視覺挑戰是偵測及解譯影像中的文字。 這種處理通常稱為 *光學字元辨識* (OCR)。 Microsoft 的讀取 API 可讓您存取 OCR 功能。 

為了測試讀取 API 的功能，我們將使用在 Cloud Shell 中執行的簡單命令列應用程式。 真實世界的解決方案也適用相同準則與功能，例如網站或手機應用程式。

## 使用 Azure AI 視覺服務讀取影像中的文字

**Azure AI 視覺**服務提供 OCR 工作的支援，包括：

- 針對較大型文件最佳化的**讀取** API。 您可以非同步方式使用此 API，並可將 API 用於列印和手寫文字。

## 建立 *Azure AI 服務*資源

您可以藉由建立 **電腦視覺 資源或 **Azure AI 服務資源，來使用 Azure AI 視覺服務****。

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

為了測試自訂視覺服務的功能，我們會使用在 Azure 上的 Cloud Shell 中執行的簡單命令列應用程式。

1. 在 Azure 入口網站中，選取頁面頂端在搜尋方塊右邊的 **[>_]** (Cloud Shell**) 按鈕。 這會在入口網站底部開啟 Cloud Shell 窗格。 

    ![按一下頂端搜尋方塊右側的圖示來啟動 Cloud Shell](media/read-text-computer-vision/powershell-portal-guide-1.png)

1. 第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 選取 [PowerShell]****。 若未看到此選項，請略過該步驟。  

1. 如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂用帳戶，然後選取 [建立儲存體]****。 然後等候一分鐘左右，讓系統建立儲存體。

    ![按一下確認以建立儲存體。](media/read-text-computer-vision/powershell-portal-guide-2.png)

1. 請確認 [Cloud Shell] 窗格左上方指出的殼層類型已切換為 [PowerShell]**。 若其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    ![如何尋找左側下拉式功能表來切換至 PowerShell](media/read-text-computer-vision/powershell-portal-guide-3.png) 

1. 等候 PowerShell 啟動。 您應該會在 Azure 入口網站中看到下列畫面：  

    ![等候 PowerShell 啟動。](media/read-text-computer-vision/powershell-prompt.png) 

## 設定和執行用戶端應用程式

現在您已擁有自訂模型，即可執行使用 OCR 服務的簡單用戶端應用程式。

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

    ![程式碼編輯器。](media/read-text-computer-vision/powershell-portal-guide-4.png)

1. 在左側的 [檔案]**** 窗格中，展開 **ai-900**，然後選取 **ocr.ps1**。 此檔案包含一些使用電腦視覺服務來偵測及分析影像中文字的程式碼，如下所示：

    ![編輯器包含程式碼來分析影像中的文字。](media/read-text-computer-vision/ocr-code.png)

1. 不要太擔心程式代碼的詳細數據，重要的是它需要端點 URL 和 Azure AI 服務資源的其中一個密鑰。 從 Azure 入口網站資源的 [金鑰和端點]**** 頁面複製上述資訊，並貼到程式碼編輯器中，分別取代 **YOUR_KEY** 和 **YOUR_ENDPOINT** 預留位置值。

    > **提示** 使用 [金鑰和端點]**** 與 [編輯器]**** 窗格時，您可能必須使用分隔線來調整螢幕區域。

    在貼上金鑰和端點值後，程式碼的前兩行應會類似下列內容：

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. 在編輯器窗格右上方，使用 [...]**** 按鈕開啟功能表，並選取 [儲存]**** 以儲存變更。 接著再次開啟功能表，並選取 [關閉編輯器]****。 既然您已設定金鑰和端點，您可以使用 Azure AI 服務資源從影像擷取文字。

    讓我們使用**讀取** API。 在此案例中，您有虛構 Northwind Traders 零售公司的廣告影像，其中包含一些文字。

    範例用戶端應用程式會分析下列影像：

    ![Northwind Traders 雜貨店廣告的影像。](media/read-text-computer-vision/advert.jpg)

1. 在 [PowerShell] 窗格中，輸入下列命令來執行程式碼以讀取文字：

    ```PowerShell
    cd ai-900
    ./ocr.ps1 advert.jpg
    ```

1. 檢閱影像中找到的詳細資料。 影像中找到的文字會組織成區域、行和字的階層式結構，而程式碼會讀取這些內容來擷取結果。

    請注意，文字的位置左上方會標示座標，並以*周框方塊*表示寬度和高度，如下所示：

    ![影像文字加框的影像](media/read-text-computer-vision/lab-05-bounding-boxes.png)

1. 現在讓我們嘗試另一個影像：

    ![打字信的影像。](media/read-text-computer-vision/letter.jpg)

    若要分析第二個影像，請輸入下列命令：

    ```PowerShell
    ./ocr.ps1 letter.jpg
    ```

1. 檢閱第二個影像的分析結果。 其也應該傳回文字和文字的周框方塊。

## 深入了解

這個簡單的應用程式只說明電腦視覺服務的部分 OCR 功能。 若要深入了解這項服務的功用，請參閱 [OCR 頁面](https://docs.microsoft.com/azure/cognitive-services/computer-vision/overview-ocr)。
