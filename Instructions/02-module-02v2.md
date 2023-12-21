---
lab:
  title: 探索電腦視覺
---

# 探索電腦視覺

> **注意** 若要完成此實驗室，您需要一個具備[系統管理存取權](https://azure.microsoft.com/free?azure-portal=true)的 Azure 訂用帳戶。

「電腦視覺」** 認知服務會使用預先定型的機器學習模型來分析影像，並擷取其相關資訊。

例如，假設虛構零售業者「Northwind Traders」** 已決定實作「智慧商店」，由 AI 服務監視商店，以識別需要協助的客戶，並指示員工協助他們。 使用電腦視覺服務，可以分析整間商店的攝影機拍攝的影像，以提供其拍攝內容有意義的說明。

在此實驗室中，您將使用簡單的命令列應用程式，查看電腦視覺服務運作情形。 真實世界的解決方案也適用相同準則與功能，例如網站或手機應用程式。

## 建立 Azure AI 服務資源

您可以建立 [電腦視覺]**** 資源或 [認知服務]**** 資源，使用電腦視覺服務。

如果您尚未建立此資源，請在 Azure 訂閱中建立 **[Azure AI 語言服務]** 資源。

1. 在另一個瀏覽器索引標籤中，開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. **按一下 &#65291;建立資源 ** 按鈕並搜尋 * Azure AI 服務 * 。 選取 ** [建立 ** ** Azure AI 服務 ** 方案]。 系統會帶您前往頁面來建立 Azure AI 服務資源。 使用下列設定來設定  ：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：選擇任何可用的區域**。
    - **名稱**：*輸入唯一名稱*。
    - **定價層**:標準 S0
    - **核取此方塊表示我已閱讀並了解下列所有條款**：選取。

1. 檢閱並建立資源，然後等候部署完成。 接著，移至所部署的資源。

1. 檢視認知服務資源的 [金鑰與端點]**** 頁面。 您需要有端點和金鑰，才能從用戶端應用程式連線。

## 執行 Cloud Shell

為了測試電腦視覺服務的功能，我們會使用在 Azure 上 Cloud Shell 中執行的簡單命令列應用程式。

1. 在 Azure 入口網站中，選取頁面頂端在搜尋方塊右邊的 **[>_]** (Cloud Shell**) 按鈕。 這會在入口網站底部開啟 Cloud Shell 窗格。

    ![按一下頂端搜尋方塊右側的圖示來啟動 Cloud Shell](media/analyze-images-computer-vision-service/powershell-portal-guide-1.png)

1. 第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 選取 [PowerShell]****。 若未看到此選項，請略過該步驟。  

1. 如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂用帳戶，然後選取 [建立儲存體]****。 然後等候一分鐘左右，讓系統建立儲存體。

    ![按一下確認以建立儲存體。](media/analyze-images-computer-vision-service/powershell-portal-guide-2.png)

1. 請確認 [Cloud Shell] 窗格左上方指出的殼層類型已切換為 [PowerShell]**。 若其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    ![如何尋找左側下拉式功能表來切換至 PowerShell](media/analyze-images-computer-vision-service/powershell-portal-guide-3.png)

1. 等候 PowerShell 啟動。 您應該會在 Azure 入口網站中看到下列畫面：  

    ![等候 PowerShell 啟動。](media/analyze-images-computer-vision-service/powershell-prompt.png)

## 設定和執行用戶端應用程式

既然您已擁有 Cloud Shell 環境，接下來，您可以執行簡單的應用程式，使用電腦視覺服務來分析影像。

1. 在命令殼層中，輸入下列命令以下載範例應用程式，並將其儲存至名為 ai-900 的資料夾。

    ```PowerShell
    git clone https://github.com/MicrosoftLearning/AI-900-AIFundamentals ai-900
    ```

    > **提示** 若您已在另一個實驗室中使用此命令來複製 *ai-900* 存放庫，則可跳過此步驟。

1. 檔案會下載到名為 **ai-900** 的資料夾。 現在我們要查看 Cloud Shell 儲存體中的所有檔案，並使用這些檔案。 在殼層中輸入下列命令：

    ```PowerShell
    code .
    ```

    請注意此命令如何開啟編輯器，如下圖：

    ![程式碼編輯器。](media/analyze-images-computer-vision-service/powershell-portal-guide-4.png)

1. 在左側的 [檔案]**** 窗格中，展開 [ai-900]****，然後選取 analyze-image.ps1****。 此檔案包含一些使用電腦視覺服務來分析影像的程式碼，如下所示：

    ![編輯器包含程式碼來分析影像](media/analyze-images-computer-vision-service/analyze-image-code.png)

1. 您不用太過顧慮程式碼，重要的是它需要端點 URL，以及 [認知服務] 資源其中一個金鑰。 從 Azure 入口網站資源的 [金鑰和端點]**** 頁面複製上述資訊，並貼到程式碼編輯器中，分別取代 **YOUR_KEY** 和 **YOUR_ENDPOINT** 預留位置值。

    > **提示** 使用 [金鑰和端點]**** 與 [編輯器]**** 窗格時，您可能必須使用分隔線來調整螢幕區域。

    在貼上金鑰和端點值後，程式碼的前兩行應會類似下列內容：

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. 在編輯器窗格右上方，使用 [...]**** 按鈕開啟功能表，並選取 [儲存]**** 以儲存變更。

    範例用戶端應用程式會使用電腦視覺服務，分析以下由 Northwind Traders 商店攝影機所拍攝的影像：

    ![影像：父母在店裡使用手機相機拍攝小孩的照片](media/analyze-images-computer-vision-service/store-camera-1.jpg)

1. 在 PowerShell 窗格中，輸入下列命令來執行程式碼：

    ```PowerShell
    cd ai-900
    ./analyze-image.ps1 store-camera-1.jpg
    ```

1. 檢閱影像分析的結果，包括：
    - 描述影像的建議標題。
    - 影像中所識別物件的清單。
    - 與影像相關「標籤」的清單。

1. 現在讓我們嘗試另一個影像：

    ![影像：在超市中拿著購物籃的人](media/analyze-images-computer-vision-service/store-camera-2.jpg)

    若要分析第二個影像，請輸入下列命令：

    ```PowerShell
    ./analyze-image.ps1 store-camera-2.jpg
    ```

1. 檢閱第二張影像的影像分析結果。

1. 讓我們再試一張：

    ![影像：推著購物車的人](media/analyze-images-computer-vision-service/store-camera-3.jpg)

    若要分析第三張影像，請輸入以下命令：

    ```PowerShell
    ./analyze-image.ps1 store-camera-3.jpg
    ```

1. 檢閱第三張影像的影像分析結果。

## 深入了解

此簡單的應用程式只說明電腦視覺服務的部分功能。 若要深入了解此服務的功能，請參閱[電腦視覺頁面](https://azure.microsoft.com/products/ai-services?activetab=pivot:visiontab)。

