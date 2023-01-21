---
lab:
  title: 探索翻譯
---

# <a name="explore-translation"></a>探索翻譯

> **注意** 若要完成此實驗室，您需要一個具備[系統管理存取權](https://azure.microsoft.com/free?azure-portal=true)的 Azure 訂用帳戶。

人類文明發展的其中一個推動力，就是人們能夠彼此溝通。 溝通是人類大多數努力成果的關鍵。

人工智慧 (AI) 可翻譯不同語言的文字或語音來協助簡化溝通，協助排除跨國家/地區和文化之間的溝通障礙。

為了測試翻譯工具服務的功能，我們會使用 Cloud Shell 中執行的簡單命令列應用程式。 真實世界的解決方案也適用相同準則和功能，例如網站或手機應用程式。

## <a name="create-a-cognitive-services-resource"></a>建立「認知服務」資源

您可以建立「翻譯工具」資源或「認知服務」資源，以使用翻譯工具服務。

如果您尚未建立上述資源，請在 Azure 訂閱中建立**認知服務**資源。

1. 在另一個瀏覽器索引標籤中，開啟位於 [https://portal.azure.com](https://portal.azure.com?azure-portal=true) 的 Azure 入口網站，並使用您的 Microsoft 帳戶登入。

1. 選取 [&#65291;建立資源] 按鈕，搜尋「認知服務」，然後使用下列設定建立**認知服務**資源：
    - **訂用帳戶**：*您的 Azure 訂用帳戶*。
    - **資源群組**：*選取或建立具有唯一名稱的資源群組*。
    - **區域**：選擇任何可用的區域。
    - **名稱**：輸入唯一名稱。
    - **定價層**:標準 S0
    - **核取此方塊表示我已閱讀並了解下列所有條款**：選取。

1. 檢閱並建立資源，然後等候部署完成。 接著，移至所部署的資源。

1. 檢視認知服務資源的 [金鑰和端點] 頁面。 您需要金鑰和位置，才能從用戶端應用程式連線。

### <a name="get-the-key-and-location-for-your-cognitive-services-resource"></a>取得認知服務資源的金鑰和位置

1. 等候部署完成。 接下來，移至您的認知服務資源，在 [概觀] 頁面上選取管理服務金鑰的連結。 您需要金鑰和位置，才能從用戶端應用程式連線到認知服務資源。

1. 檢視資源的 [金鑰和端點] 頁面。 您需要「位置/區域」和「金鑰」，才能從用戶端應用程式連線。

> **注意** 若要使用翻譯工具服務，您並不需要使用認知服務端點。 系統會提供專用於翻譯工具服務的全域端點。 

## <a name="run-cloud-shell"></a>執行 Cloud Shell

為了測試翻譯工具服務的功能，我們會使用 Azure Cloud Shell 中執行的簡單命令列應用程式。 

1. 在 Azure 入口網站中，選取頁面頂端在搜尋方塊右邊的 **[>_]** (Cloud Shell) 按鈕。 這會在入口網站底部開啟 Cloud Shell 窗格。

    ![按一下頂端搜尋方塊右側的圖示來啟動 Cloud Shell](media/translate-text-and-speech/powershell-portal-guide-1.png)

1. 第一次開啟 Cloud Shell 時，系統可能會提示您選擇要使用的殼層類型 (*Bash* 或 *PowerShell*)。 選取 [PowerShell]。 如果沒有看到此選項，請略過該步驟。  

1. 如果系統提示您為 Cloud Shell 建立儲存體，請確定您已指定訂用帳戶，然後選取 [建立儲存體]。 然後，請等候一分鐘左右，讓系統建立儲存體。

    ![按一下確認以建立儲存體。](media/translate-text-and-speech/powershell-portal-guide-2.png)

1. 請確定 Cloud Shell 窗格左上方所指出的殼層類型已切換為 *PowerShell*。 如果其類型為 *Bash*，請使用下拉式功能表切換為 *PowerShell*。 

    ![如何尋找左側下拉式功能表來切換至 PowerShell](media/translate-text-and-speech/powershell-portal-guide-3.png) 

1. 等候 PowerShell 啟動。 您應該會在 Azure 入口網站中看到下列畫面：  

    ![等候 PowerShell 啟動。](media/translate-text-and-speech/powershell-prompt.png)

## <a name="configure-and-run-a-client-application"></a>設定和執行用戶端應用程式

現在您已擁有自訂模型，即可執行使用翻譯服務的簡單用戶端應用程式。

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

    ![程式碼編輯器。](media/translate-text-and-speech/powershell-portal-guide-4.png)

1. 在左側的 [檔案] 窗格中，展開 ai-900，然後選取 **translator.ps1**。 此檔案包含一些使用翻譯工具服務的程式碼：

    ![包含使用翻譯工具服務程式碼的編輯器](media/translate-text-and-speech/translate-code.png)

1. 您不用太過顧慮程式碼的細節，重要的是它需要區域/位置，以及認知服務資源的其中一個金鑰。 從 Azure 入口網站資源的 [金鑰和端點] 頁面複製上述資訊，並貼到程式碼編輯器中，分別取代 **YOUR_KEY** 和 **YOUR_LOCATION** 預留位置值。

    在貼上金鑰和位置值之後，程式碼的前幾行應該會類似下列內容：

    ```PowerShell
    $key="1a2b3c4d5e6f7g8h9i0j...."
    $location="somelocation"
    ```

1. 在編輯器窗格右上方，使用 [...] 按鈕開啟功能表，然後選取 [儲存] 以儲存變更。 然後再次開啟功能表，並選取 [關閉編輯器]。

    範例用戶端應用程式會使用翻譯工具服務來執行數種工作：
    - 將英文的文字翻譯成法文、義大利文和中文。
    - 將英文的音訊翻譯成法文的文字

    使用下列影片播放程式來聆聽應用程式要處理的輸入音訊：

    <div class="embeddedvideo"><iframe src="https://www.microsoft.com/videoplayer/embed/RWORN0" frameborder="0" allowfullscreen="true" data-linktype="external"></iframe></div>


    > **注意** 實際應用程式可以接受來自麥克風的輸入，並將回應傳送給喇叭，但在此簡單範例中，我們會使用音訊檔案中預先錄製的輸入。

1. 在 Cloud Shell 窗格中，輸入下列命令來執行程式碼：

    ```PowerShell
    cd ai-900
    ./translator.ps1
    ```

1. 檢閱輸出。 您是否看到文字從英文翻譯成法文、義大利文和中文？  您是否看到英文音訊 "hello" 翻譯成法文文字？

## <a name="learn-more"></a>深入了解

這個簡單的應用程式只展示了翻譯工具服務的一些功能。 若要深入了解這項服務的功用，請參閱[翻譯工具頁面](https://docs.microsoft.com/azure/cognitive-services/translator/translator-overview)。