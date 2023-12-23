---
lab:
  title: 探索臉部辨識
---

# 探索臉部辨識

> **注意** 若要完成此實驗室，您需要一個具備[系統管理存取權](https://azure.microsoft.com/free?azure-portal=true)的 Azure 訂用帳戶。

電腦視覺解決方案通常需要人工智慧 (AI) 解決方案，才能偵測人臉。 例如，假設零售公司 Northwind Traders 想要知道客戶站在商店中的哪個位置，以便提供最佳協助。 若想達成此目標，其中一個方法是判斷影像中是否有任何臉部，如果有，則識別臉部周圍的週框座標。

為了測試臉部服務的功能，我們會使用 Cloud Shell 中執行的簡單命令列應用程式。 真實世界的解決方案也適用相同準則與功能，例如網站或手機應用程式。

## 建立 [臉部 API]** 資源

您可以藉由建立 [臉部]**** 資源來使用臉部服務。

如果您尚未建立此資源，請在 Azure 訂用帳戶中建立 [臉部 API]**** 資源。

1. 在另一個瀏覽器索引標籤中，開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. 按一下 [＋建立資源]**** 按鈕，搜尋 [臉部]**，然後使用下列設定建立 [臉部]**** 資源：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：選擇任何可用的區域**。
    - **名稱**：*輸入唯一名稱*。
    - **定價層**：免費 F0

1. 檢閱並建立資源，然後等候部署完成。 接著，移至所部署的資源。

1. 檢視 [金鑰和端點]**** 頁面以查看您的臉部資源。 您需要有端點和金鑰，才能從用戶端應用程式連線。

## 執行 Cloud Shell

為了測試臉部服務的功能，我們會使用 Azure Cloud Shell 中執行的簡單命令列應用程式。 

1. 在 Azure 入口網站中，選取頁面頂端在搜尋方塊右邊的 **[>_]** (Cloud Shell**) 按鈕。 這會在入口網站底部開啟 Cloud Shell 窗格。 

    ![按一下頂端搜尋方塊右側的圖示來啟動 Cloud Shell](media/create-face-solutions/powershell-portal-guide-1.png)

1. 第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 選取 [PowerShell]****。 若未看到此選項，請略過該步驟。  

1. 如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂用帳戶，然後選取 [建立儲存體]****。 然後等候一分鐘左右，讓系統建立儲存體。

    ![按一下確認以建立儲存體。](media/create-face-solutions/powershell-portal-guide-2.png)       

1. 請確定 Cloud Shell 窗格左上方所指出的殼層類型已切換為 *PowerShell*。 若其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。

    ![如何尋找左側下拉式功能表來切換至 PowerShell](media/create-face-solutions/powershell-portal-guide-3.png) 

1. 等候 PowerShell 啟動。 您應該會在 Azure 入口網站中看到下列畫面：  

    ![等候 PowerShell 啟動。](media/create-face-solutions/powershell-prompt.png)

## 設定和執行用戶端應用程式

現在您已擁有自訂模型，即可執行使用臉部服務的簡單用戶端應用程式。

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

    ![程式碼編輯器。](media/create-face-solutions/powershell-portal-guide-4.png) 

1. 在左側的 [檔案]**** 窗格中，展開 **ai-900**，然後選取 **find-faces.ps1**。 此檔案包含一些使用臉部服務來偵測及分析影像中臉部的程式碼，如下所示：

    ![編輯器包含的程式碼能偵測影像中的臉部](media/create-face-solutions/find-faces-code.png)

1. 無須顧慮程式碼的細節，重要的是需要有端點 URL，以及臉部資源的其中一個金鑰。 從 Azure 入口網站資源的 [金鑰和端點]**** 頁面複製上述資訊，並貼到程式碼編輯器中，分別取代 **YOUR_KEY** 和 **YOUR_ENDPOINT** 預留位置值。

    > **提示** 使用 [金鑰和端點]**** 與 [編輯器]**** 窗格時，您可能必須使用分隔線來調整螢幕區域。

    在貼上金鑰和端點值後，程式碼的前兩行應會類似下列內容：

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."    
    $endpoint="https..."
    ```

1. 在編輯器窗格右上方，使用 [...]**** 按鈕開啟功能表，並選取 [儲存]**** 以儲存變更。 接著再次開啟功能表，並選取 [關閉編輯器]****。

    範例用戶端應用程式會使用臉部服務，分析下列由 Northwind Traders 商店相機所拍攝的影像：

    ![影像：父母在店裡使用手機相機拍攝小孩的照片](media/create-face-solutions/store-camera-1.jpg)

1. 在 PowerShell 窗格中，輸入下列命令來執行程式碼：

    ```PowerShell
    cd ai-900
    ./find-faces.ps1 store-camera-1.jpg
    ```

1. 檢閱傳回的資訊，其中包含影像中臉部的位置。 臉部的位置左上方會標示座標，並以*周框方塊*表示寬度和高度，如下所示：

    ![影像：臉部用框線標記的人](media/create-face-solutions/store-camera-1-face.jpg)

    >**注意** 傳回個人可識別特徵的臉部服務功能會受到限制。 如需詳細資訊，請參閱https://azure.microsoft.com/blog/responsible-ai-investments-and-safeguards-for-facial-recognition/。

1. 現在讓我們嘗試另一個影像：

    ![影像：拿著購物籃的人](media/create-face-solutions/store-camera-2.jpg)

    若要分析第二個影像，請輸入下列命令：

    ```PowerShell
    ./find-faces.ps1 store-camera-2.jpg
    ```

1. 檢閱第二個影像的臉部分析結果。

1. 讓我們再試一張：

    ![影像：推著購物車的人](media/create-face-solutions/store-camera-3.jpg)

    若要分析第三張影像，請輸入以下命令：

    ```PowerShell
    ./find-faces.ps1 store-camera-3.jpg
    ```

1. 檢閱第三個影像的臉部分析結果。

## 深入了解

這個簡單的應用程式只展示了臉部服務的一些功能。 若要深入了解這項服務的功用，請參閱[人臉識別 API 頁面](https://azure.microsoft.com/en-us/products/cognitive-services/vision-services)。
